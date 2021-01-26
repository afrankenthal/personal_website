---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Kerberos and SSH Keys with macOS Keychain"
subtitle: ""
summary: ""
authors: []
tags: ["technical notes"]
categories: ["technical notes"]
date: 2021-01-25T21:04:07-05:00
lastmod: 2021-01-25T21:04:07-05:00
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

[Previously]({{< relref "/post/ssh_kerberos_keytabs_macos/index.md" >}}) I have discussed how to get SSH, Kerberos, and keytabs working together on macOS. But there is an easier way on macOS to work with both SSH keys and Kerberos keytabs in a password-less (but still safe) world. 

## SSH key passphrases

Since macOS Sierra 10.12.2, Apple offers some SSH configuration options that can automatically add SSH key passphrases to its "Keychain Access", which manages all passwords, keys, and certificates. Once you enter the passphrase to an existing SSH key, it will be stored in the Keychain and automatically retrieved when the key needs to be used again. To enable this behavior, in your `~/.ssh/config` file, add:

```bash
Host *
   AddKeysToAgent yes
   UseKeychain yes
   IdentityFile ~/.ssh/id_rsa
```

The `~/.ssh/id_rsa` location is the standard one for RSA keys, but your mileage may vary. The `UseKeychain` option makes sure the passphrases are added to the Keychain, and `AddKeysToAgent` adds the relevant (e.g. RSA) key to the SSH key agent. You can test that this works easily if you have configured a GitHub or GitLab account to use SSH keys. Then just type (for example):

```bash
$ ssh -T git@github.com
```

The first time this command runs the passphrase should be asked for. But subsequent calls will not, since the passphrase will be retrieved from the Keychain automatically.

Sources: https://apple.stackexchange.com/a/264974, https://developer.apple.com/library/archive/technotes/tn2449/_index.html

## Kerberos with Keychain Access

It turns out that Kerberos on macOS (since maybe 10.9) has a "hidden" option where you can invoke the Keychain too. If you type:

```bash
$ kinit --keychain principal@REALM
```

(where principal is your Keberos username and REALM the realm where you want to connect) then macOS will ask for your Keberos password the first time and store it in the Keychain. Subsequent kinit invocations will automatically retrieve the password from the Keychain (even if you don't use the `--keychain` option), so you don't have to type it ever again! In my opinion this is a much easier solution than the cumbersome way to retrieve proper Kerberos + keytab authentication described in my [previous post]({{< relref "/post/ssh_kerberos_keytabs_macos/index.md" >}}), though of course keytabs work across OS's while this is a macOS solution only.

Additionally, you can use this [Kerberos Ticket Autorenewal](https://hamstergene.github.io/macapps/ticket-renewer/) app to automatically renew your existing tickets, up to the maximum ticket renewability time window defined by the realm (typically a week or so).

Source: https://superuser.com/a/950769