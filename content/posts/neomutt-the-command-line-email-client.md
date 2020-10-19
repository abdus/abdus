---
title: "NeoMutt: the Command Line Email Client"
date: 2020-09-03T14:07:39+05:30
draft: true
meta:
  image: # url to image. Important for blog listing and seo
  description: # overrides .Summary
featured: false # feature a post in homepage
tableofcontents: true # whether to generate ToC
tags: []
categories: []
---

Mutt is a command line email client which can connect to IMAP/POP3 and SMTP
protocols as well as read emails from local directories.

So, how do I stumbled upon it? I am trying to optimize my workflow. Having to
click around a GUI-based email client isn't my thing. So, I look for
alternatives.

Why Mutt? because Mutt features a keybinding which is similar to Vim. This
means, a single set of shortcuts would work pretty much [everywhere](#).
Although I am using NeoMutt, things are pretty much same in both.

> All mail clients suck. This one just sucks less.

Here I am going to document how I set-up Mutt from Scratch!

## Install

Mutt and NeoMutt is available in official repositories of most of the Linux
distribution. I am using Arch Linux, so I just needed to run
`sudo pacman -Syu neomutt`. You don't need to install additional packages to
get Mutt working.

One more thing, I am using NeoMutt to get access to some extra features Mutt
does not provide by default. There is not much differences in UI and
functionalities.

## Config files

Neomutt stores system-wide config inside `XDG_CONFIG_DIR`(which is essentially
`/etc/xdg/neomutt`). For per-user configs, Neomutt uses one of the following
locations:

- `~/.muttrc`
- `~/.mutt/muttrc`
- `~/.config/mutt/muttrc`
- `~/.neomuttrc`
- `~/.neomutt/neomuttrc`
- `~/.config/neomutt/muttrc`

A Mutt config file generally includes a couple of sections. Let's start with
the ones which are essential.

### The 'user' configs

```bash
set realname = 'YOUR NAME'
set from = 'YOUR EMAIL'
set use_from = yes
set signature = "~/.mutt/signature"
```

First three fields are pretty much self-explanatory. The `signature` is a text
file which contains my email signature and will be appended to emails I compose.

This `signature` field can store commands as well. For example: setting it to
`set signature = "fortune |"` would print a random* message as my signature.
Notice that pipe character(`|`) at the end. This tells Mutt that the value is
a command, and not a filepath.

---

\* for this to work, a package called `fortune-mod` is needs to be installed

---

### IMAP config

IMAP/POP3 protocol is used to read remote mailboxes. The primary difference
between IMAP and POP3 is: POP3 stores emails locally and delete them from
server. IMAP is just the opposite. Following is how to configure IMAP:

```bash
set imap_user = 'EMAIL ADDRESS'
set imap_authenticators="oauthbearer"
set imap_keepalive = 300
set mail_check = 120
unset imap_passive  # open a new IMAP connection automatically
set imap_oauth_refresh_command="OAUTH_HANDLER_COMMAND"
```

Again, there is not many things to explain in this section (except for that 
`imap_oauth_refresh_command`). Since GMail(GSuite) discourages creating **app
passwords** and allowing **less secure apps**, I am using a method called
**OAuth2** to authenticate my address. More information on how to connect to
GMail with OAuth2 is [available here](https://github.com/google/gmail-oauth2-tools/wiki/OAuth2DotPyRunThrough)

If you are using password-based authentication, you can mention a field called
`imap_password` and put your password as its value. Otherwise leave it blank.
Mutt would as you for a password everytime you try to login.

FYI, IMAP stands for Internet Message Access Protocol and POP3 stands for 
Post Office Protocol.

### SMTP config

Simple Mail Transfer Protocol, a.k.a SMTP, is the protocol used for sending
emails. (yes, we have two different protocols for sending and accessing email).

```bash
set smtp_url = "smtp://SMTP_URL:587"
set ssl_starttls = yes
set ssl_force_tls = yes
set smtp_authenticators="oauthbearer"
set smtp_oauth_refresh_command="OAUTH_HANDLER_COMMAND"
```

Here, `ssl_force_tls` and `ssl_force_tls` are responsible for enforceing a TLS
connection as it's more secure.


### Sidebar

I have a sidebar for accessing all my GMail folders easily. You don't have to
enable one if you don't want to. Just skip the following config block.

```bash
set sidebar_visible
set sidebar_format = "%B%?F? [%F]?%* %?N?%N/?%S"
set mail_check_stats
bind index,pager B sidebar-toggle-visible
```

Setting `sidebar_visible` would render the sidebar window(or whatever you call
it).

`mail_check_stats` basically fetches email stats (example: read/unread etc).

### Remote Folders

Note that `mail_check_stats`. This is extremely important if you are enabling
sidebar or want to access remote folders within Mutt. I wasted couple of hours
to find out why Mutt was unable to find my remote folders :/
Remote mailboxes can be controlled using `mailboxes` as well.

And the last line is a keybinding responsible for toggling view of sidebar.


## Signature

## Colors

## Keybindings

## Rendering HTML Emails

## Encrypting/Signing Messages

## Aliases
