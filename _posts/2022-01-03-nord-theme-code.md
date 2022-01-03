---
title:  "Theming my code and Gist blocks in Jekyll"
tags:
  - jekyll
---
While the default code blocks are OK in this theme (Minimal Mistakes) I wanted something more "me" that blended better into the Dark skin. The [official docs](https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/) have section on Style Sheets and that is where I started, but there is no Nord theme so I ended up putting together my own. 

```css
/* Nord code */                
$base00: #3b4252; /* grey */   
$base01: #bf616a; /* red */    
$base02: #a3be8c; /* green */                                                                                             
$base03: #ebcb8b; /* yellow */
$base04: #81a1c1; /* middle blue */
$base05: #b48ead; /* purple */
$base06: #88c0d0; /* light blue */
$base07: #e5e9f0; /* white */
$base08: #5e81ac; /* blue */
$base09: #94545d; /* dark red */
$base0a: #809575; /* dark green */
$base0b: #b29e75; /* dark yellow */
$base0c: #68809a; /* dark blue */
$base0d: #8c738c; /* dark purple */
$base0e: #6d96a5; /* vim normal blue */
$base0f: #aeb3bb; /* grey */
$fg0: #d8dee9; /* white */
$bg0: #2e3440; /* dark bg */
```

This is less than perfect and doesn't look the best but it gets the job done.

Once I started adding larger blocks of code that actually took effort to write I thought I wanted them to be a bit independent of my post. I ended up finding [Github Gists](https://docs.github.com/en/github/writing-on-github/editing-and-sharing-content-with-gists/creating-gists). Gists are basically a pastebin server ran by Github that are quick to make, reference or share. Its a permanent, version controlled and can hold one or more files in each "gist". It is all around a great solution to random files or scripts that done deserve a repo.

Adding a Gist into a page is pretty simple {% raw %}`{% gist <gist id> [filename.ps1] %}`{% endraw %} but they appear as very blinding white blobs and that just will not do. 

![normalGist.png](/assets/images/normalGist.png)

I had to google around a bit but eventually found [another blog post](https://codersblock.com/blog/customizing-github-gists/) on how to get these gists looking better. The main point to take away from this is that different parts of the code have non-sensical names like `.pl-mdt` or `.pl-s` and you just need to play around with the inspect tool to see what looks good. For what it is worth, I tried to match Vim colours where I could.

Below you will find the end result of my tinkering.

```css
/* gist themeing */
/* https://codersblock.com/blog/customizing-github-gists/ */
body .gist .gist-file {
  margin-bottom: 0;
  border: 0;
  border-radius: 0;
}

body .gist .gist-data {
  border-bottom: none;
  border-radius: 4px;
  background-color: $bg0;
}

body .gist .blob-wrapper {
  border-radius: 0;
}

body .gist .highlight {
  background-color: transparent;
  font-family: 'Droid Sans Mono', monospace;
  font-size: 14px;
}

body .gist .highlight td {
  padding: 5px 15px !important;
  line-height: 1;
  font-family: inherit;
  font-size: inherit;
  color: $fg0
}

body .gist tr:first-child td {
  padding-top: 15px !important;
}

body .gist tr:last-child td {
  padding-bottom: 15px !important;
}

body .gist .blob-num {
  color: $base03;
  background-color: $base00;
  pointer-events: none;
}
/* hide the banner */
body .gist .gist-meta {
  display: none;
}

body .gist .pl-ent,
body .gist .pl-v {
     color: $base03;
}
body .gist .pl-mh,
body .gist .pl-mh .pl-en,
body .gist .pl-sr .pl-cce {
     color: $base01;
}
body .gist .pl-pds,
body .gist .pl-s,
body .gist .pl-s1,
body .gist .pl-s1 .pl-pse .pl-s2,
body .gist .pl-s1 .pl-v {
     color: $base05;
}
body .gist .pl-s1 .pl-s2,
body .gist .pl-smi,
body .gist .pl-smp,
body .gist .pl-stj,
body .gist .pl-vo,
body .gist .pl-vpf {
     color: $base0e;
}
body .gist .pl-s3,
body .gist .pl-sc {
     color: $base07;
}
body .gist .pl-sr,
body .gist .pl-sr .pl-sra,
body .gist .pl-sr .pl-sre,
body .gist .pl-src {
     color: $base06;
}
body .gist .pl-mdht,
body .gist .pl-mi1 {
     color: $base08;
     background: rgba(0, 64, 0, .5);
}
body .gist .pl-id,
body .gist .pl-ii,
body .gist .pl-md,
body .gist .pl-mdhf {
     color: $base0f;
     background: $base01;
}
body .gist .highlight-source-js .pl-st {
     color: $base04;
}
body .gist .highlight-source-css .pl-s3 {
     color: $base04;
}
body .gist .highlight-text-html-basic .pl-ent {
     color: $base04;
}
body .gist .pl-c,
body .gist .pl-c span,
body .gist .pl-mq {
     color: $base08;
}
body .gist .pl-c1,
body .gist .pl-sv,
body .gist .pl-mb {
     color: $base02;
}
body .gist .pl-e,
body .gist .pl-k,
body .gist .pl-mdh,
body .gist .pl-mdr,
body .gist .pl-ml,
body .gist .pl-mm,
body .gist .pl-mo,
body .gist .pl-mp,
body .gist .pl-mr,
body .gist .pl-ms,
body .gist .pl-st,
body .gist .pl-mi {
     color: #d08770;
}
```