---
title: "Obsidian CSS Snippets"
tags:
  - obsidian
last_modified_at: '2022-03-21'
---
I have not written a full post on how I use [Obsidian](https://obsidian.md/) yet but I talked about it in the [first post]({% post_url 2021-12-29-publishing-pages-obsidian%}) here. I plan to write more in the future but for the mean time I just wanted to put my main edits online for others who may care enough to find them.

Obsidian uses "snippets" of css to compliment/overwrite the various larger themes that you can apply to the product. Below are the ones I have made/gathered and a brief description of what they do.

To use snippets in Obsidian write a file called `<name>.css` to `.obsidian/snippets` then go to the "Appearance" section and refresh then select the file that appears with the toggle.

* TOC 
{:toc}

### Folder Colours
This is an intensive but pretty edit. You need to make a section at the bottom for every folder by name. 

![folders.png](/assets/images/2022-03-14-obsidian-css/folders.png)

```css
.theme-dark {
    /*Darker Color for 2*/
    --f-f: #3b4252;
    --f-r: #bf616a;
    --f-o: #d08770;
    --f-y: #ebcb8b;
    --f-g: #a3be8c;
    --f-p: #b48ead;
    --f-sg: #8fbcbb;
    --f-lb: #88c0d0;
    --f-frst: #81a1c1;
    --f-b: #5e81ac;
}

.theme-light {
    /*Darker Color for 1*/
    --f-f: #3b4252;
    --f-r: #bf616a;
    --f-o: #d08770;
    --f-y: #ebcb8b;
    --f-g: #a3be8c;
    --f-p: #b48ead;
    --f-sg: #8fbcbb;
    --f-lb: #88c0d0;
    --f-frst: #81a1c1;
    --f-b: #5e81ac;
}
/*00 Meta*/
.nav-folder-title[data-path="00 Meta"] {
    color: var(--f-f);
    background: var(--f-r) !important;
    border-bottom: 2px solid var(--f-r);
}
.nav-folder-title[data-path*="00 Meta"],
.nav-folder-title[data-path*="00 Meta"] + .nav-folder-children,
.nav-file-title[data-path*="00 Meta"] {
    border-left: 3px solid var(--f-r);
    margin-left: 8px;
}
.nav-folder-title[data-path*="00 Meta"]:hover,
.nav-folder-title[data-path*="00 Meta"] + .nav-folder-children:hover,
.nav-file-title[data-path*="00 Meta"]:hover {
    border-color: var(--f-r);
}

/*10 Life*/
.nav-folder-title[data-path="10 Life"] {
    color: var(--f-f);
    background: var(--f-o) !important;
    border-bottom: 2px solid var(--f-o);
}
.nav-folder-title[data-path*="10 Life"],
.nav-folder-title[data-path*="10 Life"] + .nav-folder-children,
.nav-file-title[data-path*="10 Life"] {
    border-left: 3px solid var(--f-o);
    margin-left: 8px;
}
.nav-folder-title[data-path*="10 Life"]:hover,
.nav-folder-title[data-path*="10 Life"] + .nav-folder-children:hover,
.nav-file-title[data-path*="10 Life"]:hover {
    border-color: var(--f-o);
}

/*20 IT*/
.nav-folder-title[data-path="20 IT"] {
    color: var(--f-f);
    background: var(--f-y) !important;
    border-bottom: 2px solid var(--f-y);
}
.nav-folder-title[data-path*="20 IT"],
.nav-folder-title[data-path*="20 IT"] + .nav-folder-children,
.nav-file-title[data-path*="20 IT"] {
    border-left: 3px solid var(--f-y);
    margin-left: 8px;
}
.nav-folder-title[data-path*="20 IT"]:hover,
.nav-folder-title[data-path*="20 IT"] + .nav-folder-children:hover,
.nav-file-title[data-path*="20 IT"]:hover {
    border-color: var(--f-y);
}

/*30 Hobbies*/
.nav-folder-title[data-path="30 Hobbies"] {
    color: var(--f-f);
    background: var(--f-g) !important;
    border-bottom: 2px solid var(--f-g);
}
.nav-folder-title[data-path*="30 Hobbies"],
.nav-folder-title[data-path*="30 Hobbies"] + .nav-folder-children,
.nav-file-title[data-path*="30 Hobbies"] {
    border-left: 3px solid var(--f-g);
    margin-left: 8px;
}
.nav-folder-title[data-path*="30 Hobbies"]:hover,
.nav-folder-title[data-path*="30 Hobbies"] + .nav-folder-children:hover,
.nav-file-title[data-path*="30 Hobbies"]:hover {
    border-color: var(--f-g);
}

/*40 Objects*/
.nav-folder-title[data-path="40 Objects"] {
    color: var(--f-f);
    background: var(--f-p) !important;
    border-bottom: 2px solid var(--f-p);
}
.nav-folder-title[data-path*="40 Objects"],
.nav-folder-title[data-path*="40 Objects"] + .nav-folder-children,
.nav-file-title[data-path*="40 Objects"] {
    border-left: 3px solid var(--f-p);
    margin-left: 8px;
}
.nav-folder-title[data-path*="40 Objects"]:hover,
.nav-folder-title[data-path*="40 Objects"] + .nav-folder-children:hover,
.nav-file-title[data-path*="40 Objects"]:hover {
    border-color: var(--f-p);
}

/*50 Company*/
.nav-folder-title[data-path="50 Company"] {
    color: var(--f-f);
    background: var(--f-lb) !important;
    border-bottom: 2px solid var(--f-lb);
}
.nav-folder-title[data-path*="50 Company"],
.nav-folder-title[data-path*="50 Company"] + .nav-folder-children,
.nav-file-title[data-path*="50 Company"] {
    border-left: 3px solid var(--f-lb);
    margin-left: 8px;
}
.nav-folder-title[data-path*="50 Company"]:hover,
.nav-folder-title[data-path*="50 Company"] + .nav-folder-children:hover,
.nav-file-title[data-path*="50 Company"]:hover {
    border-color: var(--f-lb);
}

/*Github Pages*/
.nav-folder-title[data-path="GithubPages"] {
    color: var(--f-f);
    background: var(--f-frst) !important;
    border-bottom: 2px solid var(--f-frst);
}
.nav-folder-title[data-path*="GithubPages"],
.nav-folder-title[data-path*="GithubPages"] + .nav-folder-children,
.nav-file-title[data-path*="GithubPages"] {
    border-left: 3px solid var(--f-frst);
    margin-left: 8px;
}
.nav-folder-title[data-path*="GithubPages"]:hover,
.nav-folder-title[data-path*="GithubPages"] + .nav-folder-children:hover,
.nav-file-title[data-path*="GithubPages"]:hover {
    border-color: var(--f-frst);
}
```

### Graph edits
This is a method to change the colour of "attachments" in the graph view. You can investigate and find other node names to change as well.
```css
/* https://forum.obsidian.md/t/is-there-a-way-to-change-the-color-of-the-nodes-in-graph-view/8271 */
.theme-dark .graph-view.color-fill-attachment {
        color: #d8dee9;
}
```

### Hide meta-data header in preview
This hides the "Meta Data" header caused by FrontMatter when in the Reading view
```css
.frontmatter-container {
    display: none;      
}
```

### Hide URL Icon
When using external links in Obsidian they have an arrow denoting such, this hides it.
```css
body .external-link {    
  background-image: none;
  padding-right: 0px;    
}
```

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

```css
body{
  --fluro-yellow-rgb: 255, 255, 0;
  --fluro-pink-rgb: 255, 0, 255;  
  --fluro-blue-rgb: 0, 255, 255;
  --fluro-green-rgb: 0, 255, 0;
  --fluro-red-rgb: 255, 0, 0;
  --text-highlight-rgb: var(--fluro-yellow-rgb);
}

mark.yellow{ --text-highlight-rgb: var(--fluro-yellow-rgb); }
mark.pink{ --text-highlight-rgb: var(--fluro-pink-rgb); }
mark.blue{ --text-highlight-rgb: var(--fluro-blue-rgb); }
mark.green{ --text-highlight-rgb: var(--fluro-green-rgb); }
mark.red{ --text-highlight-rgb: var(--fluro-red-rgb); }

.markdown-preview-view mark {
  margin: 0 -0.4em;
  padding: 0.1em 0.4em;
  border-radius: 0.8em 0.3em;
  background: transparent;
  background-image: linear-gradient(105deg,
    transparent 0,
    transparent 0.3em,
    rgba(var(--text-highlight-rgb), 0.7) 0.5em,
    rgba(var(--text-highlight-rgb), 0.4) 1.6em,
    rgba(var(--text-highlight-rgb), 0.4) calc(100% - 1.4em),
    rgba(var(--text-highlight-rgb), 0.7) calc(100% - 0.5em),
    transparent calc(100% - 0.3em),
    transparent 100%);
  -webkit-box-decoration-break: clone;
  box-decoration-break: clone;
  text-shadow: 0 0 0.75em var(--background-primary-alt);
}

.cm-s-obsidian span.cm-highlight {
  padding:0.1em 0;
  background: rgba(var(--text-highlight-rgb), 0.4);
  -webkit-box-decoration-break: clone;
  box-decoration-break: clone;
  text-shadow: 0 0 0.75em var(--background-primary-alt);
}

.cm-s-obsidian span.cm-formatting-highlight{
  margin: 0 0 0 -0.4em;
  padding: 0.1em 0 0.1em 0.4em;
  border-radius: 0.8em 0 0 0.4em;
  background: none;
  background-image: linear-gradient(105deg,
    transparent 0,
    transparent 0.3em,
    rgba(var(--text-highlight-rgb), 0.7) 0.5em,
    rgba(var(--text-highlight-rgb), 0.4) 1.6em);
  -webkit-box-decoration-break: clone;
  box-decoration-break: clone;
}
.cm-s-obsidian .cm-highlight+span.cm-formatting-highlight {
  margin: 0 -0.4em 0 0;
  padding: 0.1em 0.4em 0.1em 0;
  border-radius: 0 0.4em 0.8em 0;
  background: none;
  background-image: linear-gradient(105deg,
    rgba(var(--text-highlight-rgb), 0.4) calc(100% - 1.4em),
    rgba(var(--text-highlight-rgb), 0.7) calc(100% - 0.5em),
    transparent calc(100% - 0.3em),
    transparent 100%);
  -webkit-box-decoration-break: clone;
  box-decoration-break: clone;
}
```

### Require hovering to see scrollbars
I did not want to fully hide scrollbars with a plugin like [Hider](https://github.com/kepano/obsidian-hider) but I also didnt want to see them all the time. I found this snippet somewhere that makes them hide until you hover over them.

```css
::-webkit-scrollbar {
    visibility: hidden;
    background-color: transparent;
    width: 10px;
}

::-webkit-scrollbar-thumb {
    visibility: hidden;
}

::-webkit-scrollbar:hover {
    visibility: initial;
}

::-webkit-scrollbar-thumb:hover {
    visibility: initial;
}
```

### Minimal Checkboxes
I wanted to have more than just checkmarks possible in my checkboxes and after much struggling I arrived at this nice solution that works for Live Preview and Read view in Minimal theme (only).

Sadly with Minimal 5.1.8 Kepano added his own checkmarks that make these render incorrectly. These are now for historical reference and inspiration of other tweakers.

![checkboxes](/assets/images/2022-03-14-obsidian-css/checkboxes.png)

```css
/* nord colors from another snippet
.theme-dark {
    --f-f: #3b4252;
    --f-r: #bf616a;
    --f-o: #d08770;
    --f-y: #ebcb8b;
    --f-g: #a3be8c;
    --f-p: #b48ead;
    --f-sg: #8fbcbb;
    --f-lb: #88c0d0;
    --f-frst: #81a1c1;
    --f-b: #5e81ac;
}
*/

/* Checkbox things */
/* bring back strikethrough for completed tasks */
body:not(.minimal-strike-lists) .markdown-preview-view ul > li[data-task="x"].task-list-item.is-checked {
    text-decoration: line-through;
}
.markdown-source-view.mod-cm6 .HyperMD-task-line[data-task="x"] span {
    text-decoration: line-through;
}

/*
    ? mark boxes
*/
/* this only controls the text */
.markdown-preview-view li[data-task='?'] > .task-list-item-checkbox:checked::before,
.markdown-source-view.mod-cm6 .HyperMD-task-line[data-task="?"] span {
    text-decoration: none;
}
/* this controls the checkbox image */
input[data-task='?'].task-list-item-checkbox:checked,
.markdown-preview-view li[data-task='?'] > .task-list-item-checkbox:checked::before {
    border: var(--f-y);
    background-color: var(--f-y) !important;
    background-image: url('https://api.iconify.design/el/question.svg?color=white') !important;
}
/* preview */
.markdown-preview-view li[data-task='?'] > input[type=checkbox]:checked {
    border: var(--f-y);
    background-color: var(--f-y) !important;
    background-image: url('https://api.iconify.design/el/question.svg?color=white') !important;
}

/*
    > mark boxes
*/
/* this only controls the text */
.markdown-source-view.mod-cm6 .HyperMD-task-line[data-task=">"] span {
    text-decoration: none;
}
/* this controls the checkbox image */
/* https://icon-sets.iconify.design/mdi/arrow-right-thick/ */
input[data-task='>'].task-list-item-checkbox:checked,
.makdown-preview-view li[data-task='>'] > .task-list-item-checkbox:checked::before {
    border: var(--f-o);
    background-color: var(--f-o) !important;
    background-image: url('https://api.iconify.design/mdi/arrow-right-thick.svg?color=white') !important;
}
/* preview */
.markdown-preview-view li[data-task='>'] > input[type=checkbox]:checked {
    border: var(--f-o);
    background-color: var(--f-o) !important;
    background-image: url('https://api.iconify.design/mdi/arrow-right-thick.svg?color=white') !important;
}

/*
    - mark boxes
*/
/* this only controls the text */
.markdown-source-view.mod-cm6 .HyperMD-task-line[data-task="-"] span {
    text-decoration: none;
}
/* this controls the checkbox image */
/* https://icon-sets.iconify.design/mdi/close-thick/ */
input[data-task='-'].task-list-item-checkbox:checked,
.markdown-preview-view li[data-task='-'] > .task-list-item-checkbox:checked::before {
    border: var(--f-r);
    background-color: var(--f-r) !important;
    background-image: url('https://api.iconify.design/mdi/close-thick.svg?color=white') !important;
}
/* preview */
.markdown-preview-view li[data-task='-'] > input[type=checkbox]:checked {
    border: var(--f-r);
    background-color: var(--f-r) !important;
    background-image: url('https://api.iconify.design/mdi/close-thick.svg?color=white') !important;
}

/*
    ! mark boxes
*/
/* this only controls the text */
.markdown-source-view.mod-cm6 .HyperMD-task-line[data-task="!"] span {
    text-decoration: none;
}
/* this controls the checkbox image */
/* https://icon-sets.iconify.design/mdi/exclamation-thick/ */
input[data-task='!'].task-list-item-checkbox:checked,
.markdown-preview-view li[data-task='!'] > .task-list-item-checkbox:checked::before {
    border: var(--f-lb);
    background-color: var(--f-lb) !important;
    background-image: url('https://api.iconify.design/mdi/exclamation-thick.svg?color=red') !important;
}
/* preview */
.markdown-preview-view li[data-task='!'] > input[type=checkbox]:checked {
    border: var(--f-lb);
    background-color: var(--f-lb) !important;
    background-image: url('https://api.iconify.design/mdi/exclamation-thick.svg?color=red') !important;
}
```

### Minimal edits
Kepano really wants you to use the [Minimal Settings](https://github.com/kepano/obsidian-minimal-settings) and [Style Settings](https://github.com/kepano/obsidian-style-settings) plugins for managing minimal, but I started out and continue to use CSS to get my changes made. This handles Headers, base color (makes it Nord) and minor edits to the Title of pages.

```css
:root {

  /*----------------------------------------------------------------

  Colors

  Most colors in this theme are driven from the following values,
  meaning that the backgrounds, borders, and various shades are
  automatically generated for you.

  - Base color is used for the backgrounds, text and borders.
  - Accent color is used for links and some interactive elements.

  The colors use HSL (hue, saturation, lightness)

  - Hue (0-360 degrees):0 is red, 120 is green, and 240 is blue
  - Saturation (0-100%):0% is desaturated, 100% is full saturation
  - Lightness (0-100%):0% is black, 100% is white

  */

  --base-h:220;       /* Base hue */
  --base-s:16%;      /* Base saturation */
  --base-d:22%;   /* Base lightness Dark Mode  - 0 is black */
  /* As of 4.4.8 you also need to define --base-l in .theme-dark below otherwise a 15% overwrites it */
  --base-l:22%;     /* Base lightness Light Mode  - 100 is white */
  --accent-h:210;   /* Accent hue */
  --accent-s:34%;   /* Accent saturation */
  --accent-d:63%;   /* Accent lightness Dark Mode */
  --accent-l:63%;   /* Accent lightness Light Mode */

  --h1:2.00em;
  --h2:1.75em;
  --h3:1.50em;
  --h4:1.25em;
  --h5:1.00em;
  --h6:1.00em;

  --h1-weight:600;
  --h2-weight:600;
  --h3-weight:500;
  --h4-weight:500;
  --h5-weight:500;
  --h6-weight:400;

  --h1-variant:normal;
  --h2-variant:normal;
  --h3-variant:normal;
  --h4-variant:normal;
  --h5-variant:small-caps;
  --h6-variant:small-caps;

  --h1-color:var(--text-normal);
  --h2-color:var(--text-normal);
  --h3-color:var(--text-normal);
  --h4-color:var(--text-normal);
  --h5-color:var(--text-normal);
  --h6-color:var(--text-muted);

  --font-normal:12px;
  --font-small:10px;
  --font-smaller:9px;
  --font-smallest:8px;
  --font-title:1em;

  --font-monospace:"Hack Nerd Font";
}

.theme-dark {
    --base-l:22%;
}

/* Title fix */
.view-header-title {
  color: var(--text-faint) !important;
  font-weight: var(--weight-normal);
}

.view-header-title-container {
  padding-left: 1em;
  margin: 0;
}
```

### Do not colour internal links
I made this for someone else and kept it around for reference. It removes the colour from (sets it to white) internal links. It also strips formatting from H1 where they were using internal links.

```css
.cm-hmd-internal-link .cm-underline {
  color: white;
  opacity: 100;
}
.markdown-preview-view .internal-link {
  color: white;
  opacity: 100;
}
:root {
  h1:text-decoration: none;
}
```

### Do not underline internal links
I like this, it removes underlining from internal links and leaves just the colour intact.

```css
.cm-hmd-internal-link .cm-underline {
  text-decoration: none !important;  
}
.markdown-preview-view .internal-link {
  text-decoration: none !important;
}
```

### Nord calendar
These are some minor colour edits to the Calendar plugin.

![calendar.png](/assets/images/2022-03-14-obsidian-css/calendar.png)

```css
/* obsidian-calendar-plugin */
/* https://github.com/liamcain/obsidian-calendar-plugin */

#calendar-container {
  --color-background-heading: transparent;
  --color-background-day: transparent;
  --color-background-weeknum: transparent;
  --color-background-weekend: transparent;

  --color-dot: #81a1c1;
  --color-arrow: var(--text-muted);
  --color-button: var(--text-muted);

  --color-text-title: var(--text-normal);
  --color-text-heading: var(--text-normal);
  --color-text-day: var(--text-normal);
  --color-text-today: var(--interactive-accent);
  --color-text-weeknum: #ebcb8b;
}
```

### Nord inline code colour
This is a method to change the colour on inline code. `This kind of code`
```css
/* This makes code blocks a better color, red is default */
.cm-s-obsidian .HyperMD-codeblock {
    color: #8FBCBB;
    background-color: #2E3440;
    padding: 3px;
}
.cm-s-obsidian span.cm-inline-code {
    color: #8FBCBB;
    background-color: #2E3440;
    padding: 3px;
}
.markdown-preview-view code {
    color: #8FBCBB;
    background-color: #2E3440;
    padding: 3px;
}
```

### Red unresolved links
I want every link I make to exist, so I make any that don't exist bright red.
```css
.is-unresolved .cm-hmd-internal-link .cm-underline {
  color: FireBrick;
  opacity: 100;
}
.markdown-preview-view .internal-link.is-unresolved {
  color: FireBrick;
  opacity: 100;
}
```

### Tag multi colours
I copied this for someone to make some minor edits and keep it for reference. It is a method to colour named tags to accomplish various things.

```css
/* Colour tag pills based on name in LP and Read modes */
/* https://forum.obsidian.md/t/meta-post-common-css-hacks/1978/13 */       
/* There is extra code I removed from this snippet that is in the source */

/* Obsidian */
.tag[href^="#obsidian"] {
  background-color: #4d3ca6;
}
.cm-s-obsidian span.cm-hashtag.cm-tag-obsidian {
  background-color: #4d3ca6;
}

/* Important */
.tag[href^="#important"] {
  background-color: red;
}
.cm-s-obsidian span.cm-hashtag.cm-tag-important {
  background-color: red;
}

/* Complete */
.tag[href^="#complete"] {
  background-color: green;
}
.cm-s-obsidian span.cm-hashtag.cm-tag-complete {
  background-color: green;
}

/* InProgress */
.markdown-preview-view .tag[href^="#inprogress"] {
  background-color: orange;
}
.cm-s-obsidian span.cm-hashtag.cm-tag-inprogress {
  background-color: orange;
}
```

### Tag same colour
This, like the above, is for reference. It changes the colour of all pill tags.

```css
.cm-s-obsidian div:not(.cm-active) > .cm-hashtag {
  background-color: #027aff;
  color: #ffffff;
  font-size: 14px;
  text-align: center;
}

.tag:not(.token) {
  background-color: #027aff;
  border: none;
  color: #ffffff;
  font-size: 14px;
  text-align: center;
  display: inline-block;
  margin: 0px 3px;
  cursor: pointer;
}
.tag:not(.token):hover {
  color: #ffffff;
  background-color: #5E839A;
}
```

### Embed Fixes
Hides H1 headers in Embeds, something that bugs me when I embed notes. This is copied from the forums then modified for myself.

```css
/*
    clean-embeds-all.css snippet                                                                                                                                                                                                                                                                                                                      Removes title, link, padding, margins from embeds,
    so they really look like the same note.                                                                                                                                                                                                                                                                                                           This will not require a `cssclass` to be set but work for _all_ notes.
    Derived from the `clean-embeds.css` snippet.                                                                                                                                                                                                                                                                                                      2021-08-24 Matthias C. Hormann (Moonbase59)
    2022-07-14 PipeItToDevNull                                                                                                                                                                                                                                                                                                                        TODO: Find out how to correct PDF export. L/R margins & vspace too large on embeds.                                                                                                                                                                                                                                                               Source: https://www.reddit.com/r/ObsidianMD/comments/rm3viu/can_someone_give_me_the_css_snippet_to_do_that/                                                                                                                                                                                                                                       Note: To make something appear in Live Preview add a ".cm-s-obsidian <tag>," section that matches the ".markdown-preview-view"                                                                                                                                                                                                                */                                                                                                                                                                                                                                                                                                                                                /* remove title and the table from the "Metatable" plugin */
.cm-s-obsidian .markdown-embed-title,
.markdown-preview-view .markdown-embed-title,
.markdown-preview-view .obsidian-metatable {
  display: none;
}                                                                                                                                                                                                                                                                                                                                                 /* remove H1 from embed */
.cm-s-obsidian .markdown-embed h1,
.markdown-preview-view .markdown-embed h1 {
  display: none;
}                                                                                                                                                                                                                                                                                                                                                 /* Hover to see a box and link to the embeded note */
/* change background on hover, to exactly see whatâ?Ts embedded */
.cm-s-obsidian .markdown-embed:hover,
.cm-s-obsidian .file-embed:hover,
.markdown-preview-view .markdown-embed:hover,
.markdown-preview-view .file-embed:hover {
  background-color: var(--background-secondary) !important;
}

/* remove border and scroll */
/* unfortunately needs !important for some themes */
/* this makes the embed in-line but it won't work in full-preview =( , exports fine though*/
/* the above is a Minimal specific issue, default works fine */
.cm-s-obsidian .markdown-embed,
.cm-s-obsidian .file-embed,
.markdown-preview-view .markdown-embed,
.markdown-preview-view .file-embed {
  border: none !important;
  padding: 0 !important;
  margin: 0 !important;
}

/* don't know what this does */
.cm-s-obsidian .markdown-embed-content,
.markdown-preview-view .markdown-embed-content,
.markdown-preview-view .markdown-embed-content > .markdown-preview-view {
  max-height: unset;
  padding: 0 !important; /* !important for "Pisum" theme */
  margin: 0;
  border: 0;
}

/* remove <br> between internal embeds */
.markdown-preview-section div > br {
  display: none;
}


/* remove vertical space added by markdown-preview-sizer */
 div.markdown-preview-sizer.markdown-preview-section {
  min-height: unset !important;
  padding-bottom: 0 !important;
}

/* special considerations for printing (PDF export) */
@media print {

  /* remove frontmatter box if "Show frontmatter" was enabled */
  /* Also remove metadata table from "Metatable" plugin */
  pre.frontmatter,
  .obsidian-metatable {
    display: none;
  }
}
```

### Hide Comments in Live Preview
```css
.is-live-preview .cm-comment {
    display: none;
}
```