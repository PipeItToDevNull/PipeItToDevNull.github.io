---
title:  "Themeing my code and Gist blocks in Jekyll"
tags:
  - jekyll
---
While the default code blocks are OK in this theme (Minimal Mistakes) I wanted something more "me" that blended better into the Dark skin. The [official docs](https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/) have section on Style Sheets and that is where I started, but there is no Nord theme so I ended up putting together my own. 

```
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

Adding a Gist into a page is pretty simple `{% gist <gist id> [filename.ps1] %}` but they appear as very blinding white blobs and that just will not do. 

![normalGist.png](/assets/images/normalGist.png)

I had to google around a bit but eventually found [another blog post](https://codersblock.com/blog/customizing-github-gists/) on how to get these gists looking better. 