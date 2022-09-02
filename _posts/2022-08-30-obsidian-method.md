---
title: "My Obsidian Methods and Habits"
tags:
  - obsidian
last_modified_at: '2022-09-01'
---
In a [previous post]({% post_url 2022-08-25-update-on-obsidian%}) I talked about what I store in Obsidian and how I organize it, now I want to talk a little about how I work in Obsidian. I use Obsidian differently at work and home; work is a lot of tasking, projects, tickets, etc while at home Obsidian is much more for documentation. 

## Dataview
I just started getting into dataview, and it has changed my life. I mostly use this at work but have a small project section in my home vault. Currently I have a "Projects" directory with "Active", "Inactive", and "Complete" sub directories where I place a file for every project I am working on. At work I also do this for Tickets and Issues (anything big enough to track but not a ticket or a project).

I gather all of my projects, tickets, and tasks into one file called "Dashboard" using Dataview and later embed sections from that where I require them. For each area I track "Active {thing}" and "Active {thing} Tasks". Doing this with data view is very simple:

Active Projects
    
    ```dataview
    list from "00 Meta/03 Projects/Active"
    ````
    
Active Project Tasks

    
    ```dataview
    task from "00 Meta/03 Projects/Active"
    GROUP BY file.link
    ```
    

These two parts together make a handy overview of all projects I have and any tasks that are present inside.

![dashboard view](/assets/images/2022-08-30-obsidian-method/dashboard-view.png)

This file can get massive, quick. I mostly use it as a place to keep all of my Dataview and pull headers out of it into my daily notes or anywhere else I please. This is certainly rudimentary use of Dataview, but it has helped me be a bit more organized. Before this I would track tasks in daily notes, and project files, without any centralization. It could get messy. A goal of mine is to not duplicate data, so being able to pull data with Dataview then embed it somewhere else is great.

## Daily Notes
My longest used and most required tool in Obsidian has to be Daily Notes. My templates help me to track my daily tasks and having a place to log my day helps to keep things moving. In addition to basic Daily Notes for tracking small things, whenever I am working on an Issue, Ticket or Project I try to log their specific events, ideas, tasks into their respective files. At the bottom of each is a section resembling:

```markdown
## Daily Log
### [[[2022-08-30]]]
- Did thing
- [ ] Need to do thing
```

Using another Dataview query, I embed this small log into my Daily note. I am able to look back on any day to see what occurred without separating tasking from the associated project.

My complete Daily Note template:

{% raw %}

    # Daily
    ## Projects
    ![[Dashboard#Active Projects]]
    
    ---
    ## Morning
    - [ ] Check Tickets
    
    ---
    ## Linked Tasks
    ```dataview
    task from ""
    WHERE contains(text, "/{/{date:YYYY-MM-DD/}/}")
    GROUP by file.link
    ```
    
    ---
    ## Notes
    -  
    
    ```dataview
    TASK FROM "30 Projects" OR "40 Tickets" OR "50 Issues"
    WHERE contains(string(section), "{{date:YYYY-MM-DD}}")
    Group by file.link
    ``` 
    
    ---
    ## Evening Tasks
    - [ ] Timesheet

{% endraw %}

`## Linked Tasks` is my ingenious method of tracking future tasking in my vault. If I have a task in my Daily Note on Friday that says "Got UPS battery, change it on [[2022-08-30]]" I want to make sure I see it on the 30th. I could duplicate it to both days, or even split it, but those are just bad ideas. Instead I use a data view to scrape for any tasks with the present date. 

I write every project's, ticket's, and issue's, daily logs into their respective files. To assimilate all of those into my Daily Note I embed the date header:

```markdown
### [[Project Name]]
![[Project Name#2022-08-30]]
```

All together a formatted Daily Note can look like:

![dailt-note-example](/assets/images/2022-08-30-obsidian-method/daily-note-example.png)