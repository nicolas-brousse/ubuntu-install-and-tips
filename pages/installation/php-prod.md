---
layout: page
title: Fresh install PHP PROD server
---

__See [common installation]({{ site.baseurl }}/pages/installation/common) and configuration before.__  
Do this operation with **root** user.

## Apt-get

```bash
$ apt-get install mysql-server
$ apt-get install libapache2-mod-php5
```
```bash
$ apt-get install php-apc php5-cli php5-curl php5-dev php5-gd php5-imagick php5-intl php5-mcrypt php5-xsl
```

## Configure php.ini

```ini
; Defines the default timezone used by the date functions
; http://php.net/date.timezone
date.timezone = Europe/Paris
```


## NewRelic

TODO