---
layout: page
title: Capistrano configuration
---

adduser --system --shell /bin/sh --gecos 'Deployer manager' --disabled-password deployer

passwd -l deploy

adduser deployer rvm

adduser deployer ssh-login

Look : http://www.capistranorb.com/documentation/getting-started/authentication-and-authorisation/
