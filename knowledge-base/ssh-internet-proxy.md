---
title: Proxying the Internet via SSH
description: 
published: true
date: 2020-06-01T09:43:55.695Z
tags: tech, ssh, linux, proxy, proxychains
---

I recently had to setup some bits and pieces on a remote system which by default had very restricted access to the internet.  For the most part thats fine, but in my particular case, I found it was mostly impossible to setup the various systems as I needed them.

I ended up working around the issue in the end, by proxying internet access to the machine via my SSH connection, and using proxychains on the remote endpoint, to temporarily get access to the information I needed.

The long and short was the following command: `<machine-with-internet>$ ssh -D 1080 localhost -t ssh -R 1080:localhost:1080 <machine-no-internet>`

This sets up a SOCKS proxy on your machine with internet, then forwards that proxy via your SSH connection to the remote system.

From there, if you can get hold of `proxychains` (in the repos for most linuxes), then using a command from the remote box that accesses the internet via your machine is as simple as: `proxychains <your command>`.

Source: https://unix.stackexchange.com/a/116897