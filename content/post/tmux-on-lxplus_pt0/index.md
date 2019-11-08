---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Tmux on lxplus - first part"
subtitle: ""
summary: ""
authors: []
tags: ["technical notes"]
categories: ["technical notes"]
date: 2019-10-28T00:34:43-04:00
lastmod: 2019-10-28T00:34:43-04:00
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

(This is actually a prequel to ["Tmux on lxplus"]({{< ref "/post/tmux-on-lxplus/index.md" >}}), despite being uploaded after it)

The tmux version on CERN's lxplus is very old, 1.8. Since version 2.0 tmux has a host of neat new features, which makes it worth the pain of installing it locally. Here are the steps I took to get tmux 2.3 running on my lxplus setup.

* Download everything (tmux requires libevent and ncurses)

        $ mkdir -p $HOME/tmux_tmp
        $ mkdir -p $HOME/local
        $ cd $HOME/tmux_tmp
        $ wget https://github.com/tmux/tmux/archive/2.3.tar.gz
        $ wget https://github.com/downloads/libevent/libevent/libevent-2.0.19-stable.tar.gz
        $ wget ftp://ftp.gnu.org/gnu/ncurses/ncurses-5.9.tar.gz

* Install libevent

        $ tar zxvf libevent-2.0.19-stable.tar.gz
        $ cd libevent-2.0.19-stable
        $ ./configure —-prefix=$HOME/local —-disable-shared
        $ make
        $ make install
        $ cd ..

After the make command you might get some errors related to building the man or documentation, but you can ignore it and move on to make install.

* Install ncurses

        $ tar zxvf ncurses-5.9.tar.gz
        $ cd ncurses-5.9
        $ export CPPFLAGS=“-P"
        $ ./configure —-prefix=$HOME/local —-enable-symlinks
        $ make
        $ make install
        $ cd ..

Here again you might get some errors while compiling, but they seem to be all related to the man command so you should be able to ignore them. The export CPPFLAGS line is to avoid another compilation error (see here: https://stackoverflow.com/questions/37475222/ncurses-6-0-compilation-error-error-expected-before-int). —enable-symlinks is also required to avoid yet another error (see here: http://lists.bestpractical.com/pipermail/shipwright/2010-June/000029.html).

* Install tmux

        $ tar xzvf 2.3.tar.gz
        $ cd tmux-2.3
        $ ./autogen.sh
        $ mkdir -p build; cd build
        $ ../configure CFLAGS="-I$HOME/local/include -I$HOME/local/include/ncurses" LDFLAGS="-L$HOME/local/lib -L$HOME/local/include/ncurses -L$HOME/local/include" CPPFLAGS="-I$HOME/local/include -I$HOME/local/include/ncurses" --prefix=$HOME/tmux_tmp/tmux-2.3
        $ make
        $ cp tmux $HOME/local/bin

* Clean up

        $ rm -rf $HOME/tmux_tmp

* Add local bin to $PATH

        $ export PATH=$HOME/local/bin:$PATH
(ideally add this line to ~/.bash_profile so it gets executed every time)

Done! Now just source the bash_profile again and run tmux!

Source: adapted from tmux_local_install.sh script at https://gist.github.com/ryin/3106801 

(See lxplus version from https://gist.github.com/pablodecm/151e90af9787e8340562)
