---
title: "An Update on My Use of Obsidian"
tags:
  - obsidian
last_modified_at: '2022-08-25'
---
I have been using [Obsidian](https://obsidian.md) daily for almost 2 years now. It is a great tool and I continue to learn new ways to use it. I recently had a major breakthrough on my use of tags and links so I decided to write an update on my usage and methodologies.

> 📝 Check out my [CSS snippets]({% post_url 2022-03-14-obsidian-css%}) as well.

## What I put in Obsidian
Everything. Currently I have 5 sections, META, Life, IT, Hobbies, and Objects. Some people would break this out into multiple vaults, but I am leveraging [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to break some things out for use in other places.

My work vault contains Meta, Documentation, IT, Projects, Tickets, and Issues.

### Meta
My META section holds my "periodics" which would be Daily, Weekly, Monthly, etc notes, I really only do Daily though. I have a dream to use Weekly, Monthly, Quarterly, and Yearly notes more to summarize my life and work for reflection and personal improvement. I also keep my Templates and master Project files in META.

### Life
In Life I hold Career, Property, Vehicle, Recipes, Travel Plans, etc information. Obsidian was a great tool when I was job searching. I had notes for every position I was interested in linked to every company with details on their benefits etc. I also try to keep some kind of record on who I talk to, their position, and their contact information. 

If you do not already, pre-planning out interviews by jotting down every question you want to ask is a great way to stay engaged and ensure you do not forget anything important you wanted to clarify.

### IT
My IT directory is actually a git submodule, I sync it to its own repository so I can clone it into the vault I use at work. Being able to centralize all of my IT knowledge between my work and homelab without contaminating my work/life separation is amazing.

### Hobbies
I have several hobbies, [homelabbing](/homelab), keyboards, 3d printing, gaming, etc. I also store my notes on r/TS here. A bulk of this is notes, and documentation for my homelab, but having a central place to put stuff from all of my other hobbies has really come in handy.

### Objects
My Objects directory is something I need to think about more. Currently it holds people and companies that I reference anywhere else in the vault. Does it belong in META? I don't know.

## Organization
I am using a heavily abbreviated [Johnny Decimal System (JDS)](https://johnnydecimal.com/) based system to organize my files. My directory names are actually "00 META", "10 Life", "20 IT" etc. Inside of each I have top level numbered directories: "20 META", "21 Systems", "22 Tools" but after that it degrades. 

I stick to a hard rule of only 3 directories and I do no more than 10 child directories under any top level parent, but do not number the grandchildren. Inside of "21 Systems" are "Linux", "Windows", and "Containers". This has been working well for me, so far.

<img src="/assets/images/2022-08-25-update-on-obsidian/JDS0.png" alt="JDS layout" width="200"/>

This ended up being too long for one post, so I will continue talking about my methodology in a [future post]().
