---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Pyxrootd bindings on macOS"
subtitle: ""
summary: ""
authors: []
tags: ["technical notes"]
categories: ["technical notes"]
date: 2019-10-19T23:21:01-04:00
lastmod: 2019-10-19T23:21:01-04:00
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

The homebrew version of xrootd doesn’t come with python bindings for some reason. The python bindings are needed for reading remote ROOT files with python/uproot (not needed for C++ ROOT).

Adapted from: https://github.com/lgray/coffeandbacon/blob/master/setup_lcg.sh

    # issue with python3 bindings, see https://sft.its.cern.ch/jira/browse/SPI-1198
    wget https://github.com/xrootd/xrootd/archive/v4.8.3.tar.gz 
    tar zxf v4.8.3.tar.gz && rm -f v4.8.3.tar.gz 
    cp xrd_setup.py xrootd-4.8.3/bindings/python/ 
    pushd xrootd-4.8.3/bindings/python/ 
    python xrd_setup.py install
    popd
    rm -rf xrootd-4.8.3 

Check whatever version of xrootd you have and substitute the numbers above. You can find the xrd_setup.py file {{% staticref "files/xrd_setup.py" %}}here{{% /staticref %}}.

(Or from: https://github.com/lgray/coffeandbacon/blob/master/xrd_setup.py)

My pyxrootd ended up installed here:

    /usr/local/lib/python3.7/site-packages/pyxrootd-4.8.3-py3.7-macosx-10.12-x86_64.egg/

To check open up python3 and try to import pyxroot.
