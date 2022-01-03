---
title:  "Theming my code and Gist blocks in Jekyll"
tags:
  - jekyll
---
While the default code blocks are OK in this theme (Minimal Mistakes) I wanted something more "me" that blended better into the Dark skin. The [official docs](https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/) have section on Style Sheets and that is where I started, but there is no Nord theme so I ended up putting together my own. 

{% gist 02003efef6bfe1f81d13767b734224f1 nord-style.css} 

This is less than perfect and doesn't look the best but it gets the job done.

Once I started adding larger blocks of code that actually took effort to write I thought I wanted them to be a bit independent of my post. I ended up finding [Github Gists](https://docs.github.com/en/github/writing-on-github/editing-and-sharing-content-with-gists/creating-gists). Gists are basically a pastebin server ran by Github that are quick to make, reference or share. Its a permanent, version controlled and can hold one or more files in each "gist". It is all around a great solution to random files or scripts that done deserve a repo.

Adding a Gist into a page is pretty simple {% raw %}`{% gist <gist id> [filename.ps1] %}`{% endraw %} but they appear as very blinding white blobs and that just will not do. 

![normalGist.png](/assets/images/normalGist.png)

I had to google around a bit but eventually found [another blog post](https://codersblock.com/blog/customizing-github-gists/) on how to get these gists looking better. The main point to take away from this is that different parts of the code have non-sensical names like `.pl-mdt` or `.pl-s` and you just need to play around with the inspect tool to see what looks good. For what it is worth, I tried to match Vim colours where I could.

Below you will find the end result of my tinkering.

{% gist 02003efef6bfe1f81d13767b734224f1 nord-gist.css}