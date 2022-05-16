---
title: "Using Signed RDP Certificates"
tags:
  - windows_server
  - windows_ca
  - powershell
last_modified_at: '2022-05-16'
---
One of the most ubiquitous actions a sysadmin does is accepting the untrusted certificates we are presented with daily when opening RDP to a server. I believe training this behaviour is a horrible practice that Microsoft should discourage more forcefully. I decided to see what I could do about it in my lab.

There are two solutions available, the first is to trust all of the self-signed certificates from each server at a domain level. If you have 2 or 3 servers that may work but it does not scale well and is not an automated solution. Your second option is to issue certificates from your internal CA through GPO and that is the option we are going to explore.

I found numerous sources and hit a couple of issues but the docs below should be a solid baseline for anyone else to explore the idea of issuing out signed RDP certificates to all of their servers.

## Documentation
* TOC 
{:toc}

## Default Configuration
Windows server by default uses self signed certificates to secure RDP, this makes sense. The settings that control the issuance are located at `HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server`. The most relevant key on the server is `HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\SelfSignedCertStore`

## Creating a RDP Certificate Template
*The following images and most of the content is from [this source](https://www.darkoperator.com/blog/2015/3/26/rdp-tls-certificate-deployment-using-gpo) I am copying it for the sake of preservation and my personal notes. Review his work instead if you prefer. His notes are from 2015 but they still seem relevant and worked for me on Server 2019 and Windows 10.*

*Any deviation is marked in \[Brackets\]. My work picks back up at [Applying the Policy](#applying-the-policy)*

### In your CA
1. Open the **Certificate Authority** management console, Right-Clicking on **Certificate Templates** and selecting **Manage**

    ![CA image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114101.png)

2. Select **Computer** template and Right-Click on it selecting **Duplicate Template**

    ![CA image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114219.png)

3. \[In the compatibility settings I chose Server 2019 and Windows 10\] so as to make sure my connection uses stronger encryption algorithms and ciphers. This will vary depending on your network if you are forced to keep end of life versions of Windows or not.

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114336.png)

4. Navigate to the **General** Tab and set a **Display Name** and **Template Name.** I recommend using the same and with no spaces. Had once a weird bug where on Windows 2008 it would enroll a new certificate again and again if a space was in the display name.

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114522.png)

5. On the **Extensions** tab we click on **Edit** to modify the extensions for the certificate that will be issued.   
   
    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114545.png)

6. We now select **Client Authentication** and click **Remove**. Many tutorial I see out there follow blindly the recommendations on others to also remove Server Authentication, this will break compatibility on none Windows platforms using the Microsoft Remote Desktop Client.
   
    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114619.png)

7. After removing the Client Authentication policy we now click on **Add** and in the window that appears we click on **New** to create a new policy specific for use of RDP TLS.

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114722.png)

8. We provide the policy a name, in the example I give it a name of **Remote Desktop Authentication** and provide a **Object Identifier** of **1.3.6.1.4.1.311.54.1.2** this will identify the certificate as one that can be used to authenticate a RDP server.

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114738.png)

9. Under the **Security** tab we need to identify those systems that can enroll using this template. Domain Computers is already present and with the **Enroll** permission but if you also plan to enable RDP on Domain Controllers add the Domain Controllers group and ensure the Enroll permission is selected. \[Do not remove Authenticated users from this or any other certificate template. I found this generates [cryptic errors](https://www.pkisolutions.com/the-requested-template-is-not-supported-by-this-ca-error-0x80094800/) when trying to enroll in the certificate\]

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114836.png)

10. If you have computers that are not able to enroll using the certificate template a quick way to identify it is a permission issue is to look in the **Event Viewer** and look under the **System Windows Log** for events with ID **1064** from the source **TerminaServices-RemoteConnectionManager**.

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114909.png)

11. Go in to the Certificate Authority management console and select under the CA  C**ertificate Template**, **right click** and select **New -> Certificate Template to Issue**

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114931.png)

12. Select the certificate template you just created and click **OK**

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514114951.png)

### In GPO
1. Create or select an existing GPO and editing it. In the Group Policy Object Select **Computer Configuration -> Policies -> Administrative Template -> Windows Components -> Remote Desktop Services -> Remote Desktop Session Host -> Security** and select  **Server authentication certificate template.**

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514115623.png)

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514115632.png)

2. Click on E**nable** and under **Certificate Template Name** we enter the name of the certificate template we made available for enrollment and click on **OK**.

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514115705.png)

3. To have the server use TLS 1.0 (I know TLS 1.0 is not the most secure) we select **Require use of specific layer for remote (RDP) connection** 

    > ❗ If you have TLS 1.2 configured this setting will enforce TLS 1.2 not SSL 1.0 [source](https://docs.microsoft.com/en-US/troubleshoot/windows-server/remote/incorrect-tls-use-rdp-with-ssl-encryption)

    ![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514115951.png)

### Optional GPO Settings
While under security settings I would also recommend enabling NLA since this and TLS will break most public RDP brute forcing tools. Select **Require user authentication for remote connections by using Network Level Authentication** and double click on it. On the properties screen select **Enable** and click on **OK.**

Also since we do not want users to simply accept and always trust connections since this defeats the purpose of all this settings we ensure that clients always validate the server certificate.  We select **Computer Configuration -> Policies -> Administrative Templates -> Windows Components -> Remote Desktop Settings -> Remote Desktop Connection Client** We double click on **Configure Authentication for Client.** Select **Enable** and set the Option to **Warn me if authentication fails**

If Remote Desktop is not enabled on another GPO you will need to go in to **Connections** under **Remote Desktop Session Host** and enable **Allow users to connect remotely by using Remote Desktop Service**.

![CA Image](/assets/images/2022-05-14-using-signed-rdp-certificates/Pasted image 20220514120047.png)

## Applying the Policy
Now that GPO is configured you can run `gpupdate /force` on a server, it should pull the certificate into its personal store at `Cert:\LocalMachine\My\`. To start using the newly requested certificate you must reboot the server or run `Restart-Service -Name TermService -Force`.

Once you run the above or reboot you can validate the configuration with the following function. This function will compare the certificate in use to the certificate that was requested. If they match you are using a signed cert.

<!--
https://gist.github.com/PipeItToDevNull/62e4ab3e8ee3594f35ce161bba7904e7
-->
{% gist 62e4ab3e8ee3594f35ce161bba7904e7 Check-RdpCertificate.ps1 %}

## Removing the Default Self-Signed Certificate
You will notice that the above function most likely returns "A Self-Signed RdpCertificate is present" this is because Windows does not remove nor does it stop generating the self-signed certificate located at `Cert:\LocalMachine\Remote Desktop\`. 

If you do not mind having an unused certificate you can leave this alone and forget about it, but if you need to appease security scanners that check for self-signed certificates then you will need to take further action.

Windows will generate a self-signed certificate at every boot, and every time TermService gets restarted, deleting the cert does nothing for you. I found 2 solutions to this but both are incredibly hacky and may introduce new issues.

#### Change the CertStore location to an invalid path in the registry
1. Open `HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations`
2. Change "SelfSignedCertStore" to "NULL" or any other invalid path
3. Delete the certificate from `Cert:\LocalMachine\Remote Desktop\` and restart the "TermService"

#### Remove SYSTEM permissions from the CertStore location
1. Open `HKLM:\SOFTWARE\Microsoft\SystemCertificates\Remote Desktop` 
2. Choose "Permissions..."
    ![[Pasted image 20220514123102.png]]
3. Select "SYSTEM" and tick "Deny" on Full Control
    ![[Pasted image 20220514123209.png]]
4. Delete the certificate from `Cert:\LocalMachine\Remote Desktop\` and restart the "TermService"

## Updates
### Using Traditional "Server Authentication" Certificates
I found that the "Remote Desktop Authentication" Extended Key Usage is only required when using GPO. The "Server Authentication" attribute also works but you must manually set the certificate to be used by thumbprint on the host.

> The "Enhanced Key Usage" extension has a value of either "Server Authentication" or "Remote Desktop Authentication" (1.3.6.1.4.1.311.54.1.2). Certificates with no "Enhanced Key Usage" extension can be used as well. [source](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/configuring-remote-desktop-certificates/ba-p/247007)

The command for this would be `wmic /namespace:\\root\CIMV2\TerminalServices PATH Win32_TSGeneralSetting Set SSLCertificateSHA1Hash="THUMBPRINT"
`, the source above has a much messier implementation but according [this redddit post](https://www.reddit.com/r/sysadmin/comments/izoyyy/force_remote_desktop_to_use_an_established/) and a couple other sources I saw this command is all you need.

### Verifying Certificates in Use
You can query a server with OpenSSL to see what cert is truly in use.

`openssl.exe s_client -showcerts -connect localhost:3389`

## References
* [RDP TLS Certificate Deployment Using GPO (darkoperator.com)](https://www.darkoperator.com/blog/2015/3/26/rdp-tls-certificate-deployment-using-gpo)
* [Securing RDP Connections with Trusted SSL/TLS Certificates](http://woshub.com/securing-rdp-connections-trusted-ssl-tls-certificates/)
* [The Requested Template is not Supported by this CA (Error 0x80094800) - PKI Solutions Inc.](https://www.pkisolutions.com/the-requested-template-is-not-supported-by-this-ca-error-0x80094800/)
* [Prevent remote desktop from generating a self-signed certificate - Microsoft Q&A](https://docs.microsoft.com/en-us/answers/questions/204015/prevent-remote-desktop-from-generating-a-self-sign.html)
* [(67) Force Remote Desktop to use an established certificet - NOT a self-signed : sysadmin (reddit.com)](https://www.reddit.com/r/sysadmin/comments/izoyyy/force_remote_desktop_to_use_an_established/)
* [What are the steps to stop Windows 10 systems from generating/regenerating a RDP self-signed certificate? (microsoft.com)](https://social.technet.microsoft.com/Forums/security/en-US/bb8ece84-7592-4ed3-b133-b45ab850e5de/what-are-the-steps-to-stop-windows-10-systems-from-generatingregenerating-a-rdp-selfsigned?forum=winserversecurity)
* [Configuring Remote Desktop certificates](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/configuring-remote-desktop-certificates/ba-p/247007)
