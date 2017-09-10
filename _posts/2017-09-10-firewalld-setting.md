---
layout: post
title:  "firewalld setting"
date:   2017-09-10
desc: "방화벽 설정하기"
keywords: "centOS7,centOS6,firewalld,iptables"
categories: [LINUX]
tags: [firewalld,centOS7,iptables,centOS6]
icon: icon-html
---

**firewalld setting**
===============================================
---

**CENTOS 7 설정**
-----------------

허용할 포트나 ip 를 입력해주자.

*# vi /etc/firewalld/zones/allowlist.xml*
```
<?xml version="1.0" encoding="utf-8"?>
<zone>
  <source address="xxx.xxx.xxx.xxx/32"/>
  <source address="xxx.xxx.xxx.xxx/32"/>
  <source address="xxx.xxx.xxx.xxx/32"/>
  <port protocol="tcp" port="3306"/>
  <port protocol="tcp" port="22"/>
</zone>
```

*# firewall-cmd --reload*


---
**CENTOS 6 설정**
-----------------

*# vi /etc/sysconfig/iptables#

```
# Firewall configuration written by system-config-firewall
# Manual customization of this file is not recommended.
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -m state -s xxx.xxx.xxx.xxx/32 --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A INPUT -m state -s xxx.xxx.xxx.xxx/32 --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT

```

*# service iptables restart*



