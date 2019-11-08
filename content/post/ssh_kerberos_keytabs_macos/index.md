---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "SSH + Kerberos + Keytabs on MacOS"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2019-11-08T00:05:49-05:00
lastmod: 2019-11-08T00:05:49-05:00
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

    
Kerberos is a convenient way to authenticate and obtain access to remote machines via SSH. Instead of typing your password every time you want to access a remote computer, you can type your password only once and obtain a Kerberos ticket, which serves as a ‘passport’ and saves typing effort during subsequent connections.

However, Kerberos tickets usually expire in 24 hours, so you still need to type (and therefore remember) your password at least once a day. Kerberos keytab files make the authentication process even more convenient. With keytabs, you type your password once, it gets encrypted according to the chosen encryption method, and then the encrypted password in the keytab file can be used to obtain a Kerberos ticket, which will subsequently grant access to the remote machine. Never type your password again! 

But be careful to make the keytab file readable only by you, the owner, as anyone with a read access to a keytab file will automatically have access to the remote machine as well (though they still won’t know your password, since it’s encrypted).

To get SSH with Kerberos + keytabs working, it’s a long and harrowing road… But let’s start with the first step.

**Get SSH + Kerberos + Keytabs working:**

1. Obtain correct SSH binary. If you have MacOS Sierra, it comes with an updated version of OpenSSH that drops some options that support Kerberos authentication (the most important being `GSSAPITrustDNS`). What's necessary here is to find an SSH binary from El Capitan and then copy it to your `/usr/local/bin` folder, and make sure that the `$PATH` variable points first to that folder, before pointing to `/usr/bin` (where the native SSH binary lives), so that it will be picked up first by the system.

2. Adjust Kerberos configuration. This is a complicated process but you can just copy the right `krb5.conf` to your system, placing it in `/etc/krb5.conf`. Here is mine: {{% staticref "files/krb5.conf" %}}krb5.conf{{% /staticref %}}.

3. Enable Kerberos authentication in SSH config. For each remote network you want to connect to (e.g. Fermilab, CLASSE, CERN), edit the file `~/.ssh/config` to be similar to this one: {{% staticref "files/config" %}}config{{% /staticref %}}. It’s important to have the `GSSAPI\*` options and the `PreferredAuthentications` option like in the file, to allow Kerberos authentication.

4. Make a keytab file with your encrypted password. This step is to create a keytab file containing your password that will be fed to the kinit command in order to obtain a Kerberos ticket. On MacOS X (which comes with the Heimdal flavor of Kerberos, and not MIT’s) the command to add a password for CERN’s account is:
    
    ```
    $ ktutil -k ~/keytab add -p user@CERN.CH -e arcfour-hmac-md5 -V 3
    ```
    
    MacOS will complain about the chosen encryption but it’s the only one that kinit supports for automation of CERN’s network connection (as far as I know). Other encryptions also contain a “salt” that `ktutil` doesn’t handle well (see https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=698534 and https://serverfault.com/questions/620521/kerberos-ktutil-what-kinds-of-encryption-are-available). The equivalent command for a CLASSE entry would be: 

    ```
    $ ktutil -kt ~/keytab add -p user@CLASSE.CORNELL.EDU -e aes256-cts-hmac-sha1-96 -V 1
    ```

    You can also make your keytab file when logged in to one of the remote machines. For example, if you are on a lxplus machine, you can create a keytab file with a different version of the Kerberos tools (MIT’s one): 

    ```
    $ ktutil 
    addent -password -p user@CERN.CH -k 3 -e arcfour-hmac-md5
    (type your password)
    wkt keytab
    quit
    ```

    (for more info see here https://kb.iu.edu/d/aumh). Now the keytab file in your home directory contains your encrypted passwords for access to CERN’s and CLASSE’s networks.
5. Use the keytab file to authenticate to `kinit`. The command `$ kinit —afslog -kt ~/keytab user@CERN.CH` or `$ kinit -ky ~/keytab user@CLASSE.CORNELL.EDU` should now grant you Kerberos tickets without having to type your password. Note that you could include this command in (start-up) scripts, so that you always have a connection on. Neat!
6. SSH to remote machine as usual. For example, `ssh user@lxplus.cern.ch` or `ssh user@lnx201.classe.cornell.edu`. Again your password shouldn’t be asked anymore.
7. Remember to set the permissions of the keytab file to read-only by you! Anyone with read access to this file could log in to your accounts, so make sure it can only be readable by you.

More (partial) info: http://linux.web.cern.ch/linux/docs/kerberos-access.shtml
