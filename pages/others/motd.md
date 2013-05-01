---
layout: page
title: Message of the day
---


## Get RVM latest version

Create `/etc/update-motd.d/92-rvm` file with this content:

```bash
#!/bin/sh

printf "\nRVM version %s (latest: %s)\n\n" "$(rvm --version | awk -F '|' '/^r/ {sub("^rvm ", "", $1); sub(" (.+).+", "", $1); print $1}')" "$(curl --silent https://raw.github.com/wayneeseguin/rvm/stable/VERSION)"
```


---------------------------------
sources:

- http://askubuntu.com/questions/100052/modify-the-ssh-welcome-message-to-include-system-ip-address
- https://wiki.ubuntu.com/UpdateMotd#Design
