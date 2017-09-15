---
layout: post
title:  "비밀번호 없이 ssh 접속 하기 + sudoers 설정"
date:   2017-09-15
desc: "비밀번호 없이 ssh 접속 하기 + sudoers 설정"
keywords: "ssh,linux,sudoers"
categories: [Linux]
tags: [Linux,ssh,sudoers]
icon: icon-html
---

**비밀번호 없이 ssh 접속 하기 + sudoers 설정**
===============================================

---

**ssh 접속시 비밀번호 없이 로그인 할 유저를 만든다.**

[root@localhost ~]# useradd user

---

**sudoers 설정을 해준다.**

sudo visudo 로 /etc/sudoers 파일을 열어서 설정할 것 

[root@localhost ~]# sudo visudo


```
root	ALL=(ALL) 	ALL
```

아래에
```
user	ALL=(ALL)	NOPASSWD:ALL
```
를 추가해줘서 user 계정에게 password 없이 sudo 접근을 하도록 허용해 준다.

---

**user 로 로그인 해서 public key 등록하기**

[root@localhost ~]# sudo su - user

[user@localhost ~]$ pwd

/home/user

[user@localhost ~]$ mkdir .ssh

[user@localhost ~]$ cd .ssh

[user@localhost .ssh]$ vi authorized_keys

이 authorized_keys 안에 접속할 pc의 public key 를 등록해 주면 되는데, 
키가 없을 경우

[user@localhost .ssh]$ ssh-keygen -t rsa

로 키를 생성해주면,
 개인키는 ~/.ssh/id_rsa로 공개키는 ~/.ssh/id_rsa.pub로 생성된다.

id_rsa.pub 의 내용을 저 authorized_keys 안에 복사해서 붙여넣기 해 주면 된다.

그렇게 되면

해당 public key 의 pc에서 원격지의 user 계정으로 ssh 접속을 했을 때 비밀번호 없이 접근 가능하게 된다.

단, 권한 설정이

[user@localhost ~]$ chmod 700 ~/.ssh/

[user@localhost ~]$ chmod 600 ~/.ssh/authorized_keys

이렇게 되어있어야 한다.

