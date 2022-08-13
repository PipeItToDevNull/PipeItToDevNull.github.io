---
title: "Obsidian CSS Snippets"
tags:
  - obsidian
last_modified_at: '2022-08-13'
---
I have not written a full post on how I use [Obsidian](https://obsidian.md/) yet but I talked about it in the [first post]({% post_url 2021-12-29-publishing-pages-obsidian%}) here. I plan to write more in the future but for the mean time I just wanted to put my main edits online for others who may care enough to find them.

Obsidian uses "snippets" of css to compliment/overwrite the various larger themes that you can apply to the product. Below are the ones I have made/gathered and a brief description of what they do.

To use snippets in Obsidian write a file called `<name>.css` to `.obsidian/snippets` then go to the "Appearance" section and refresh then select the file that appears with the toggle.

* TOC 
{:toc}

### Folder Colours
This is an intensive but pretty edit. You need to make a section at the bottom for every folder by name. 

![folders.png](/assets/images/2022-03-14-obsidian-css/folders.png)

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 folders.css %}

### Graph edits
This is a method to change the colour of "attachments" in the graph view. You can investigate and find other node names to change as well.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 graph.css %}

### Hide meta-data header in preview
This hides the "Meta Data" header caused by FrontMatter when in the Reading view

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 meta-data.css %}

### Highlighter 
I expanded this [existing snippet](https://github.com/deathau/obsidian-snippets/blob/main/realistic-highlight.css) to add additional colours.

![highlighter.png](/assets/images/2022-03-14-obsidian-css/highlighter.png)

To use the highlighter functions see below:
```
==Yellow==
<mark class='pink'>pink</mark>
<mark class='green'>green</mark>
<mark class='blue'>blue</mark>
<mark class='red'>red</mark>
```

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 highlighter.css %}

### Require hovering to see scrollbars
I did not want to fully hide scrollbars with a plugin like [Hider](https://github.com/kepano/obsidian-hider) but I also didnt want to see them all the time. I found this snippet somewhere that makes them hide until you hover over them.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 scrollbars.css %}

### More Checkboxes
I wanted to have more than just checkmarks possible in my checkboxes and after much struggling I arrived at this nice solution that works for Live Preview and Read view in Minimal theme (only).

Sadly with Minimal 5.1.8 Kepano added his own checkmarks that make these render incorrectly. These are now for historical reference and inspiration of other tweakers.

![checkboxes](/assets/images/2022-03-14-obsidian-css/checkboxes.png)

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 checkboxes.css %}

### Strike Through Checks
A consolation script from the above, this brings back only strike throughs to Minimal now that I don't need the bulk of my new checkmarks.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 strike-checks.css %}

### Minimal edits
Kepano really wants you to use the [Minimal Settings](https://github.com/kepano/obsidian-minimal-settings) and [Style Settings](https://github.com/kepano/obsidian-style-settings) plugins for managing minimal, but I started out and continue to use CSS to get my changes made. This handles Headers, base color (makes it Nord) and minor edits to the Title of pages.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 minimal-edits.css %}

### Do not colour internal links
I made this for someone else and kept it around for reference. It removes the colour from (sets it to white) internal links. It also strips formatting from H1 where they were using internal links.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 plain-links.css %}

### Lean Links
This is a larger edit, it makes unresolved links red, and removes the underline from internal links. The large block at the top is needed to add the line back in Minimal. Due to the way external links work you cannot add it to only external links.

I also remove the hovering arrow icon from external links.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 links.css %}
### Nord calendar
These are some minor colour edits to the Calendar plugin.

![calendar.png](/assets/images/2022-03-14-obsidian-css/calendar.png)

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 nord-calendar.css %}

### Nord code colour
This is a method to change the colour on inline code and code blocks.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 nord-code.css %}

### Tag multi colours
I copied this for someone to make some minor edits and keep it for reference. It is a method to colour named tags to accomplish various things.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 tag-colour-multi.css %}

### Tag same colour
This, like the above, is for reference. It changes the colour of all pill tags.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 tag-colour-single.css %}

### Embed Fixes
Hides H1,H2, and H3 headers in Embeds, something that bugs me when I embed notes. This is copied from the forums then modified for myself.

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 embeds.css %}

### Hide Comments in Live Preview

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 comments.css %}

### Red Pin for Pinned Tabs
This changes the color of the Pin icon present when a page is pinned. 

{% gist 7b10691ec3da7fe2a1f1b2cfb6426763 red-pin.css %}