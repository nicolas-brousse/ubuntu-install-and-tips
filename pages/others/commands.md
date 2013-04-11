---
layout: page
title: Generic and useful commands
---

List crontab content of all user:  
`for user in $(cut -f1 -d: /etc/passwd); do crontab -u $user -l; done`

### DNS

- `dig domain.tld`
- `dig @ns.server.tld domain.tld`: ask ns.server.tld to know domain.tld dns informations
- `dig -x XXX.XXX.XXX.XXX`: domain reverse

### Network

- `netstat -atnpu`: port stats

### Mysql

- `mysqldump -u root --password="password" --all-databases | gzip> all_databases_dump.sql.gz`: Dump all Mysql databases
- `mysql < dump.sql`: Resore databases from a sql file
- `mysql database_name < dump.sql`: Resore a database from a sql file


### PostgreSQL




### Users/groups

- `adduser --groups group_name user_name`: Create user
- `adduser --system --no-create-home [--disabled-password] [--disabled-login] [--shell /bin/bash] --home-dir / --groups group_name user_name`: Create system user
- `adduser group_name user_name`: Add a user into a group

### Get data from an other server

Run this command from on new server.  
`ssh remote.srv.tld "cd /data/;tar zcf - files" | tar zxf -`  
This command recursively copies /data/files from remote.srv.tld to local server a lot faster on slow network.

[Source](http://www.tonido.com/blog/index.php/2009/04/09/network-file-transfer-with-on-the-fly-compression/)

### Regular synchronization

```
# --delete: remove files they are in remote but not in source

# r: recursive
# a: archive
# z: compression
# e: protocol `ssh`

# source destination

rsync --delete -raze "ssh" remote.server.tld:/path/to/rsync/ /path/to/rsync/
```

### Others

- `du -hs /path/to/folder`: Get folder size
- `df -h`: Get disks size

- `iptables -L -n -v`

- `su user_name -c 'command to execute'`: execute a command with `user_name` user
- `ssh -f remote.server.tld -L local_port:localhost:remote_port -N`: open an ssh tunnel

- `find . -name ".svn" -exec rm -rf {} \;`: remove `.svn` directories

- `tar cfz archive.tar.gz target_dir_or_file`: archive and compress file or directory into tar.gz
- `tar xfz archive.tar.gz /path/to/unarchive`: unarchive a tar.gz file


## Tools

- rkhuntuer: root kit hunter
