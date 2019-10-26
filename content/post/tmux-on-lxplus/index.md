---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Tmux on lxplus"
subtitle: ""
summary: ""
authors: []
tags: []
categories: ["technical notes"]
date: 2019-10-19T23:14:25-04:00
lastmod: 2019-10-19T23:14:25-04:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Lxplus comes with native tmux installed. However, the native version is 1.8 which is very old. CERN has no plans to update its tmux version, but it is possible to install your own tmux locally (see here).

When using my local tmux, I was running into a strange issue. I was able to create a new session and detach and reattach to it successfully while in the _same_ ssh session. But after logging out of lxplus and then back in, when trying to reattach to the tmux session, I got this error:

> open terminal failed: missing or unsuitable terminal: xterm-256color

After a year I have finally traced the problem to the root cause, with this very helpful reference:

https://www.mail-archive.com/tmux-users@lists.sourceforge.net/msg01272.html

The issue is the 'terminfo database entry can’t be found for “xterm”’. The solution is simple: just export in bash the terminfo location before starting the tmux session:

    $ export TERMINFO=/usr/share/terminfo
    $ cd ~/programs/tmux
    $ ./tmux new

Then after a new SSH session run the export command again and attach to the tmux session (actually, might not need the export command when reattaching):

    $ export TERMINFO=/usr/share/terminfo
    $ cd ~/programs/tmux
    $ ./tmux a

You can also just copy the export command to the .bashrc file.

More details about diagnostics: I think the problem might be that I accidentally used some native libraries to compile the local tmux (in /usr/lib/ and /usr/lib64) which was seen from running ‘ldd ./tmux’, though I’m not sure. Could also be that the ncurses version used was different than the local one I downloaded. Not really sure, but in any case exporting the TERMINFO info solves it.
