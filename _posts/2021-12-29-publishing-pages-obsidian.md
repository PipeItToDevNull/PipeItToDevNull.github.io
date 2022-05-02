---
title: "Publishing to Github Pages with Obsidian"
tags:
  - obsidian
  - github
last_modified_at: '2022-05-02'
---
## Reasons
I used to host a personal [Bookstack](https://www.bookstackapp.com/) and [still host one](https://rtech.support) for r/Techsupport but I realized that putting all of my notes into a public cloud was a waste of my time due to the various delays while editing, moving, and the need to manually alter/consider permissions on a shelf/page/book level.

Since dropping Bookstack I have been using [Obsidian](https://obsidian.md/) for my personal notes and syncing them between devices using the [Obsidian Git plugin](https://github.com/denolehov/obsidian-git). This has worked wonderfully but of course I cannot host *anything* publicly with it, I do not want my main Obsidian repo being public and even if they were readable plain markdown is not the best presentation.

## Github Pages
[Github Pages](https://docs.github.com/en/pages) is a way to publish a static site directly out of a gihub repo. Edit your markdown files, push a change, and then Jekyll CI/CD pipeline will rebuild it in a few minutes and publish the new result. This simple push-build method jives very well with how I already use Obsidian, I decided to give it a shot. 

I use my [personal gitea](https://git.dev0.sh) instance to host my main Obsidian repo so I added my [GitHubPages](https://github.com/PipeItToDevNull/Dev0-Pages) repo a submodule (which is a supported configuration with the Git plugin) and started pushing documents.

## Issues
### Page links not working
2022-02-10 As I have learned more, these links are a bad method and using [post URLS](https://mademistakes.com/mastering-jekyll/how-to-link/) is a much better method

~~For some reason Jekyll was not replacing links to files with HTML properly, it was leaving `.md` links in place and offering to download that file rather than linking to the `.html` version. It *was* generating the HTML files though as we could navigate to them manually by replacing `.md` with `.html` in the page.~~

~~This was due to links using `%20` for spaces instead of a literal whitespace.  My resolution is to omit spaces from all page names and to change from using WikiLinks to Markdown links. Using Markdown links and relative paths for everything is likely best anyway since it will be more "universal" and prevent issues if I ever leave Obsidian.~~


