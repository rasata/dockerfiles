# about minimum2scp/ruby-full image

 * based on minimum2scp/ruby (see https://github.com/minimum2scp/dockerfiles/tree/master/ruby)
 * mruby package installed
 * ruby 2.0.0-p481, ruby 2.1.2, ruby 2.2.0-dev is installed by rbenv

## ssh login to container

ssh login to container:

```
ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no debian@<container IP address>
```

or use published port:

```
ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no -p <published ssh port> debian@localhost
```

 * user "debian" is available
 * password is "debian"
 * user "debian" can use sudo command without password
 * `id debian`: `uid=2000(debian) gid=2000(debian) groups=2000(debian),4(adm),27(sudo)`

## processes

```
UID        PID  PPID  C STIME TTY      STAT   TIME CMD
root         1     0  0 03:25 ?        Ss     0:00 init [2]  
root        38     1  0 03:25 ?        Ssl    0:00 /usr/sbin/rsyslogd
root        63     1  0 03:25 ?        Ss     0:00 /usr/sbin/cron
root        74     1  0 03:25 ?        Ss     0:00 /usr/sbin/sshd
root        81    74  0 03:27 ?        Ss     0:00  \_ sshd: debian [priv]
debian      83    81  0 03:27 ?        S      0:00      \_ sshd: debian@pts/0
debian      84    83  0 03:27 pts/0    Ss     0:00          \_ -bash
debian     135    84  0 03:27 pts/0    R+     0:00              \_ ps -ef fww
```

## ports

| port         | process              | comment                                       |
|:-------------|:------------------   |:------------------------------------------    |
| TCP/22       | sshd                 | invoked by init                               |
| TCP/80       | nginx                | disabled autostart                            |
| TCP/9001     | supervisord          | disabled autostart                            |

## about rbenv

### rbenv versions, and default ruby

rbenv gloabl (/opt/rbenv/version) is not defined, and some rubies are built.

```
$ rbenv versions
* system (set by /opt/rbenv/version)
  2.0.0
  2.0.0-p481
  2.1.2
  2.2.0
  2.2.0-dev
$ ls -l /opt/rbenv/versions
total 8
lrwxrwxrwx 1 root root 10 Sep  7 17:39 2.0.0 -> 2.0.0-p481
drwxr-xr-x 1 root root 36 Sep  7 17:39 2.0.0-p481
drwxr-xr-x 1 root root 36 Sep  7 17:45 2.1.2
lrwxrwxrwx 1 root root  9 Sep  7 17:52 2.2.0 -> 2.2.0-dev
drwxr-xr-x 1 root root 36 Sep  7 17:52 2.2.0-dev
```

