# Server group "Alloy steel"

## All servers - install and base setup
- lvm-based partitioning with separate boot, root, var, tmp, log, opt(home) and swap with various secure mount options
- apt setup, dpkg remount /tmp with exec
- base setup timezone, locales, environment, motd, issue
- working environment for main and servcraft users, dotfiles, ssh, authorized keys, rrsync keys
- install base pkgs like vm-tools, net-tools, vim, curl, rsync, zip etc.
- network setup, resolv.conf, mailname
- iptables, default deny policy, iptables-restore, bad packets, icmp flood, ssh bruteforce protection
- custom kernel options, sysctl, grub
- rsyslog rules
- logrotate rules
- sudoers setup
- sshd restrictions, tcp wrappers
- aliases

## carbon
net
```
  85.143.104.130, 10.20.0.10
  + mx.misis.ru
  ssh tcp/22
  httpd tcp/80 tcp/443
  smtpd tcp/25 tcp/587
  dovecot tcp/4190(sieve) tcp/143(imap) tcp/110(pop3) tcp/993(imaps) tcp/995(pop3s)
  postgres tcp/5432
```
- web server (nginx)
    - mail.misis.ru
    - list.misis.ru
- smtp server (postfix)
- pop3/pop3s/imap4/imap4s server (dovecot)
- antispam server (rspamd)
- antivirus server (clamd)
- mailing lists server (\*mlist)
- rdbms server (postgresql)
    - vmail
    - roundcube
    - sogo
- dns server (bind9) cache only, nonrecursive
- memcached server
- redis server
- rrd graphing tool (cacti)
- rrd mail statistics (mailgraph)
- rrd mqueue statistics (queuegraph)
- rrd dns statistics (bindgraph)
- postfix log summarizer (pflogsumm)
- mail web interface (roundcube)
- collaboration server (sogo)
- mail admin cli (\*mxop)
- ssh server
- local backup (\*bur)

```
0,,,,0,globals,pgsql
,,,,0,vmail,pgsql
,,,,0,rcube,pgsql
,,,,0,sogo,pgsql
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,root,,,/root/
,,,,0,home,,,/home/
,,,,0,libredis,,,/var/lib/redis/
,,,,0,librspamd,,,/var/lib/rspamd/
0,0,,,0,libmailman,,,/var/lib/mailman/
0,0,,,0,libsogo,,,/var/lib/sogo/
0,0,,,0,libmailgraph,,,/var/lib/mailgraph/
0,0,,,0,libqueuegraph,,,/var/lib/queuegraph/
0,0,,,0,libbindgraph,,,/var/lib/bindgraph/
0,0,,,0,usrlocal,,,/usr/local/
```

## iron
net
```
  85.143.104.132(173), 10.20.0.2(8)
  + ns.misis.ru
  ssh tcp/22
  httpd tcp/80 tcp/443
  named udp/53 tcp/53
  dhcpd udp/67
  ntpd udp/123
  iperf udp/5201
  rsyslog udp/514
  tftpd udp/69
  flow-capture udp/10.20.0.2:9014
  mysql tcp/3306
```
- web server (apache)
    - noc.misis.ru
    - net.misis.ru
    - lg.misis.ru
    - autodiscover.misis.ru
    - autoconfig.misis.ru
    - mailapi.misis.ru
    - mtcm.misis.ru
    - billing.mtcm.ru
    - stat.mtcm.ru
    - speedtest3.misis.ru
    - st3.misis.ru
- network admin web interface and command line tools and utils (\*scripts, a lot of)
- billing (\*scripts)
- com clients billing interface (\*scripts)
- looking glass (\*scripts)
- email gateway (\*scripts)
- telegram bot (\*scripts)
- mail admin rest-like api (\*scripts)
- autoconfig email services for microsoft, mozilla and apple schemes
- netflow collector (flow-tools)
- netflow processor (\*scripts)
- cisco configs backup (\*scripts)
- cisco configs monitor (rancid)
- network asset management (racktables)
- network uptime tracker with reports (\*ipinger)
- rsyslog hub
- php-fpm server
- rdbms server (mysql)
    - billing
    - racktables
    - cacti
- dns server (bind9) split horizon (internet, direct, filtered), master
- dhcp server
- ntp server
- ftps server
- tftp server
- network speed test server (iperf3)
- admin network macs monitor (arpwatch)
- rrd graphing tool (cacti)
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,mysql,mysql
,,,,0,billing,mysql
,,,,0,racktables,mysql
,,,,0,cacti,mysql
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,root,,,/root/
,,,,0,home,,,/home/
,,,,0,usrlocal,,,/usr/local/
,,,,0,varwww,,,/var/www/,--exclude=cacti/
,,,,0,rancid,,,/var/lib/rancid/
,,,,0,tftp,,,/opt/tftp/
,,,,0,adm,,,/opt/adm/,--exclude=log/ --exclude=var/cache/ --exclude=var/ipinger/
,,,,0,CA,,,/opt/CA/
,,,,0,cacti,,,/opt/cacti/,--exclude=log/
,,,,0,feed,,,/opt/feed/
,,,,0,tgsend,,,/opt/tgsend/
,,,,0,lg.misis.ru,,,/opt/lg.misis.ru/
,,,,0,mailapi,,,/opt/mailapi/
,,,,0,mtcm.misis.ru,,,/opt/mtcm.misis.ru/
,,,,0,mtcm.ru,,,/opt/mtcm.ru/
,,,,0,mylap.net,,,/opt/mylap.net/
,,,,0,net.misis.ru,,,/opt/net.misis.ru/
,,,,0,racktables,,,/opt/racktables/
,,,,0,adminer,,,/opt/adminer/
```

## copper
net
```
  85.143.104.131(157), 85.143.106.97(107), 10.20.0.1(7)
  + ns.misa.ac.ru ntp.misis.ru
  ssh tcp/22
  httpd tcp/80 tcp/443
  named udp/53 tcp/53
  dhcpd udp/67
  ntpd udp/123
  iperf udp/5201
  rsyslog udp/514
  bgpd tcp/179
  charon udp/4500 udp/68 udp/500
  nprobe udp/55562
```
- web server (nginx)
    - speedtest.misis.ru
    - st.misis.ru
- misis man users database and router (\*argus)
- misis man gateway, router, firewall, nat, pat (\*argus)
- cisco admins tools (\*ccmd, tftp, telnet, ssh)
- netflow emitter (iptables module)
- bgp server (quagga)
- rsyslog hub (all of cisco switches and routers)
- dns server (bind9) split horizon (intranet, filtered, internet), slave
- dns cache
- dhcp server
- ntp server
- vpn ikev2 server (strongswan)
- vpn ssl server (openssh)
- network speed test server (iperf3)
- synchronized dns and dhcp servers restarter
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
```

## chrome
net
```
  85.143.106.3, 10.20.0.3
  + ns2.misis.ru
  ssh tcp/22
  httpd tcp/80 tcp/443
  named udp/53 tcp/53
  dhcpd udp/67
  ntpd udp/123
  iperf udp/5201
```
- web server (nginx)
    - help.misis.ru
    - box.misis.ru
    - speedtest2.misis.ru
    - st2.misis.ru
- issue tracking, service desk, knowledge base (glpi)
- asset inventory (fusioninventory)
- collaboration server (owncloud)
- php-fpm server
- rdbms server (mysql)
    - glpi
    - fusioninventory
    - owncloud
- dns server (bind9) split horizon (intranet, filtered, internet), slave
- ntp server
- network speed test server (iperf3)
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,mysql,mysql
,,,,0,glpidb,mysql
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,root,,,/root/
,,,,0,home,,,/home/
,,,,0,glpi,,,/opt/glpi/
,,,,0,varwww,,,/var/www/
0,0,,,0,usrlocal,,,/usr/local/
```

## zinc
net
```
  85.143.104.133, 10.20.0.20
  ssh tcp/22
```
- backup hub (\*bur)
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,root,,,/root/
,,,,0,home,,,/home/
0,0,,,0,usrlocal,,,/usr/local/
```

## wolfram
net
```
  85.143.106.6, 10.20.0.6
  ssh tcp/22
  postgres tcp/5432
```
- r&d
- rdbms server (postgresql)
- rdbms server (mysql)
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,root,,,/root/
,,,,0,home,,,/home/
0,0,,,0,usrlocal,,,/usr/local/
```

## nickel
net
```
  85.143.106.4
  ssh tcp/22
  httpd tcp/80 tcp/443
```
- reverce proxy
    - api.misis.ru
    - print.misis.ru
    - vf.misis.ru
    - mc.misis.ru
- web redirector
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,root,,,/root/
,,,,0,home,,,/home/
0,0,,,0,usrlocal,,,/usr/local/
```

## vanadium
net
```
  85.143.104.155
  ssh tcp/22
  httpd tcp/80 tcp/443
```
- directum rx frontend
- reverce proxy
    - drx.misis.ru
- web redirector
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,root,,,/root/
,,,,0,home,,,/home/
0,0,,,0,usrlocal,,,/usr/local/
```

## cobalt
net
```
  85.143.106.5
  ssh tcp/22
  httpd tcp/80 tcp/443
  postgres tcp/5432
```
- docker server
    - web server (nginx + dockergen)
        - git.misis.ru
        - docker.misis.ru
    - git server (gitea)
    - docker registry
- rdbms server (postgresql)
- mysql server
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,root,,,/root/
,,,,0,home,,,/home/
,,,,0,git,,,/opt/git/,--exclude=gitea/log/ --exclude=gitea/sessions/
0,0,,,0,usrlocal,,,/usr/local/
```

## tin
net
```
  10.20.39.37
  + razr.misis.ru
  ssh tcp/22
  httpd tcp/80 tcp/443
  containers tcp/3000:5000
```
- lk devel app server
- docker server
    - web server (nginx + dockergen)
        - lk-test.misis.ru
        - alk-test.misis.ru
        - edu-test.misis.ru
        - anketa-test.misis.ru
    - application servers for each developer
- build and deploy system (\*doper)
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,docker,,,/opt/docker/
,,,,0,localbin,,,/usr/local/bin/
0,0,,,0,root,,,/root/
0,0,,,0,home,,,/home/
```

## lead
net
```
  10.20.39.38
  + rendr.misis.ru
  ssh tcp/22
  httpd tcp/80 tcp/443
  apps tcp/3000:5000
```
- lk prod app server
- docker server
    - application servers
        - login.misis.ru lk.misis.ru www.login www.lk
        - lk-new.misis.ru
        - alk.misis.ru
        - alk-new.misis.ru
        - edu.misis.ru
        - edu-new.misis.ru
        - anketa.misis.ru www.anketa
        - anketa-new.misis.ru
        - pay-test.misis.ru
- build and deploy system (\*doper)
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,docker,,,/opt/docker/
,,,,0,localbin,,,/usr/local/bin/
0,0,,,0,root,,,/root/
0,0,,,0,home,,,/home/
```

## zirconium
net
```
  10.20.39.35
  ssh tcp/22
  postgres tcp/5432
```
- lk devel database
- rdbms server (postgresql)
    - portal_development
    - sandboxes
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
0,,,,0,globals,pgsql
,,,,0,portal_development,pgsql
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,localbin,,,/usr/local/bin/
0,0,,,0,root,,,/root/
0,0,,,0,home,,,/home/
```

## selenium
net
```
  10.20.39.36
  ssh tcp/22
  postgres tcp/5432
```
- lk prod database
- rdbms server (postgresql)
    - portal_production
    - portal_test
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
0,,,,0,globals,pgsql
,,,,0,portal_production,pgsql
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,localbin,,,/usr/local/bin/
0,0,,,0,root,,,/root/
0,0,,,0,home,,,/home/
```

## antimony
net
```
  85.143.106.23
  ssh tcp/22
  httpd tcp/80 tcp/443
```
- lk frontend
- reverce proxy
    - login.misis.ru lk.misis.ru www.login www.lk
    - lk-new.misis.ru
    - alk.misis.ru
    - alk-new.misis.ru
    - edu.misis.ru
    - edu-new.misis.ru
    - anketa.misis.ru www.anketa
    - anketa-new.misis.ru
- web redirector
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,root,,,/root/
,,,,0,home,,,/home/
0,0,,,0,usrlocal,,,/usr/local/
```

## cerium
net
```
  10.20.39.49
  ssh tcp/22
  postgres tcp/5432
```
- directum rx database
- rdbms server (postgresql)
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
0,,,,0,globals,pgsql
,,,,0,drx,pgsql
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,localbin,,,/usr/local/bin/
0,0,,,0,root,,,/root/
0,0,,,0,home,,,/home/
```

## beryllium
net
```
  10.20.39.50
  ssh tcp/22
```
- directum rx docker
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,localbin,,,/usr/local/bin/
0,0,,,0,root,,,/root/
0,0,,,0,home,,,/home/
```

## niobium
net
```
  10.20.39.51
  ssh tcp/22
```
- directum rx elasticsearch
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
,,,,0,burself,,,/opt/bur/,--include=*.bur --exclude=*
,,,,0,etc,,,/etc/
,,,,0,localbin,,,/usr/local/bin/
0,0,,,0,root,,,/root/
0,0,,,0,home,,,/home/
```


---
## razr
net
```
  10.1.0.247
  ssh tcp/22
  httpd tcp/80 tcp/443
  postgres tcp/5432
  containers tcp/3000:5000
```
- docker server
    - web server (nginx + dockergen)
        - lk-test.misis.ru
        - alk-test.misis.ru
        - edu-test.misis.ru
        - anketa-test.misis.ru
        - application servers for each developer
- build and deploy system (\*doper)
- rdbms server (postgresql)
    - portal_development
    - sandbox
    - dev_\*
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
0,,,,0,globals,pgsql
,0,0,0,,portal_development,pgsql
,,,,0,etc,,,/etc/
,,,,0,docker,,,/opt/docker/
,,,,0,localbin,,,/usr/local/bin/
0,0,,,0,root,,,/root/
0,0,,,0,home,,,/home/
```

## rendr
net
```
  85.143.106.13
  ssh tcp/22
  httpd tcp/80 tcp/443
  postgres tcp/5432
  containers tcp/3000:5000
```
- docker server
    - web server (nginx + dockergen)
        - login.misis.ru lk.misis.ru www.login www.lk
        - lk-new.misis.ru
        - alk.misis.ru
        - alk-new.misis.ru
        - edu.misis.ru
        - edu-new.misis.ru
        - anketa.misis.ru www.anketa
        - anketa-new.misis.ru
        - pay-test.misis.ru
        - application servers
- build and deploy system (\*doper)
- rdbms server (postgresql)
    - portal_production
    - portal_test
- ssh server
- smtp smarthost (postfix)
- local backup (\*bur)

```
0,,,,0,globals,pgsql
,,,,,portal_production,pgsql
,,,,0,etc,,,/etc/
,,,,0,docker,,,/opt/docker/
,,,,0,localbin,,,/usr/local/bin/
0,0,,,0,root,,,/root/
0,0,,,0,home,,,/home/
```
---


```
misis.ru
  soa ns.misa.ac.ru
  ns ns.misa.ac.ru
misa.ac.ru mtcm.ru
  soa ns.misis.ru
  ns ns.misis.ru ns2.misis.ru

ns.misis.ru lather carbon 85.143.104.132(mail,st,lg,list,mylap), 135(stat), 142(api), 147(admin), 171(net)
ns2.misis.ru blazer chrome 85.143.106.3(st,proxy), 4(ssp), 5(glpi+ocs), 6(owncloud)
ns.misa.ac.ru sever copper 85.143.106.97 85.143.104.131
              saver tin 85.143.106.107(vlan211) 85.143.104.157(vlan205)

ssh tcp/22
httpd tcp/80 tcp/443
named udp/53 tcp/53
dhcpd udp/67
ntpd udp/123
rsyslog udp/514
iperf udp/5201
tftpd udp/69
flow-capture udp/10.20.0.2:9014
smtpd tcp/25 tcp/587
dovecot tcp/4190(sieve) tcp/143(imap) tcp/110(pop3) tcp/993(imaps) tcp/995(pop3s)
bgpd tcp/179
charon udp/4500 udp/68 udp/500
nprobe udp/55562
postgres tcp/5432
mysql tcp/3306
dhclient udp/68
```
