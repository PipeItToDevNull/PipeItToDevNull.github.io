---
title:  "Windows Media Player randomly opening (in XenCenter console)"
tags:
  - xencenter
---
# 2022-01-30-wmp-xencenter
I was troubleshooting a server that was not liking RDP, so I was interacting with it via the XenCenter console. For some reason this server (Server 2016) kept opening Windows Media Player every few minutes. I googled the issue of course and a top hit is malware, I doubted that was my issue so I kept digging. 

I eventually found [a post](https://superuser.com/questions/232426/windows-media-center-opens-up-by-itself-sometimes) that mentioned "multi media keys" as a possible culprit. The light bulb went off in my head and I realized I had [Caffeine](https://caffeine.en.lo4d.com/windows) running on my host. I killed it and did some more testing, lo and behold it was the culprit.

This does not affect anything in RDP or SSH, it appears to be specific to XenCenter consoles (at least mine) which is currently version 8.2.4.7594.