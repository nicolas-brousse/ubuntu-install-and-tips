---
layout: page
title: Gitolite installation
---

```bash
$ apt-get install git-core
```

With **root** user:

```bash
$ adduser \
    --system \
    --shell /bin/sh \
    --gecos 'git version control' \
    --group \
    --disabled-password \
    --home /var/git \
    git
```

Switch to **git** user:

```bash
$ su - git
```

```bash
$ cd /var/git
$ mkdir bin
$ gitolite/install -ln
```


`vi /var/git/.bashrc`

```bash
export PATH=$PATH:$HOME/bin

```

`source .bashrc`

```bash
$ gitolite setup -pk yourPubKey.pub
```

-------------------------------
sources:

- [http://gitolite.com/gitolite/qi.html](http://gitolite.com/gitolite/qi.html)
