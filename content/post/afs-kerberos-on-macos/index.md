---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "AFS + Kerberos on MacOS"
subtitle: ""
summary: ""
authors: []
tags: ["technical notes"]
categories: ["technical notes"]
date: 2019-11-08T00:05:50-05:00
lastmod: 2019-11-08T00:05:50-05:00
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

CERN provides AFS access to its remote machines. When you log in via SSH you are directed to your own personal folder in the AFS filesystem. It turns out you can mount the remote AFS filesystem on your local machine and "skip" the SSH step, treating the folder as if it were local (SSHFS-style). Once you have [SSH + Kerberos + keytab files]({{< ref "/post/ssh_kerberos_keytabs_macos" >}}) configured, you can use the steps below to install and use AFS on MacOS.

**Steps to install and use AFS on MacOS:**

1. Visit this website to download and install OpenAFS: https://www.auristor.com/openafs/client-installer/. OpenAFS will mount the AFS filesystem locally on the Mac.
2. The installation will ask for a default cell name. For CERN, this is cern.ch.
3. You should have a Kerberos configuration file (`krb5.conf`) already updated from using SSH + Kerberos at CERN. It should have the right configuration to accept AFS tickets. If not follow [this post]({{< ref "/post/ssh_kerberos_keytabs_macos" >}}) to get it done.
4. Make sure to include the option `—afslog` in your `kinit` command if you want to use AFS. After you obtain a Kerberos ticket, run the command `aklog`, which should you grant you an AFS token. Type `tokens` to check if this worked.
5. You should now have an AFS token. You should also have an AFS folder at `/afs/cern.ch/user/u/username` that you can navigate as if it were a local folder.

For more info on AFS at CERN, see https://gist.github.com/OmeGak/9530124, and http://akorneev.web.cern.ch/akorneev/howto/openafs.txt. For AFS on Macs, see http://computing.help.inf.ed.ac.uk/afs-mac-os-x and http://blog.encomiabile.it/2014/12/26/openafs-and-mac-os-x-yosemite/.
