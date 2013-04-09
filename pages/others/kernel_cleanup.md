---
layout: page
title: Cleaning up old Ubuntu kernels from /boot
---

Get your kernel version

```bash
$ uname -a
```

List the kernel into /boot:

```bash
$ sudo dpkg -l linux-image-\* | grep ^ii
```

Uninstall the old kernel:

```bash
$ sudo apt-get purge linux-image-3.0.0-16-generic
```

**WARNING: Don't remove the current kernel version!!**


-------------------------------
source: [http://blog.niftysnippets.org/2012/06/cleaning-up-old-ubuntu-kernels-from.html?m=1](http://blog.niftysnippets.org/2012/06/cleaning-up-old-ubuntu-kernels-from.html?m=1)