---
layout: post
title:  "linux root login"
date:   2017-09-13
desc: "linux 보안 mini tip"
keywords: "linux,root,login"
categories: [Linux]
tags: [Linux,login]
icon: icon-html
---

**linux root login 접속 차단**
===============================================

ssh root 접속을 차단하는 것이 좋다.

/etc/ssh/sshd_config 에서

permitrootlogin yse를 permitrootlogin no로 변경.

*# vi /etc/ssh/sshd_config*

```
 # permitrootlogin yes 
 permitrootlogin no

```