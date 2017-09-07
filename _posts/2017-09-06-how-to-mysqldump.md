---
layout: post
title:  "MySQL dump"
date:   2017-09-06
desc: "MySQL backup 을 위한 쉘 스크립트 작성 ( * dump 시의 -S 옵션은 mysql-multi 환경이기 때문에 사용함)"
keywords: "mysqldump,dump,mysqlbackup"
categories: [database]
tags: [mysqldump,dump]
icon: icon-html
---

**MySQL dump (mysql multi)**
============================

**1. 백업 스크립트를 만들자**\*

*# vi backup.sh*

```
TODAY=`/bin/date +%m-%d-%y_%H:%M`

# 계정정보
USERNAME="MySQL 접속 계정"
PASSWORD="MYSQL 접속 비밀번호"
DATABASE="DUMP하려는 데이터베이스 이름"

mysqldump -u$USERNAME -S /경로/mysqld1.sock -p$PASSWORD $DATABASE | gzip -c > /저장경로/mysql_backup/mysqldump-$TODAY.gz
```

*# sh backup.sh*

쉘 스크립트를 실행하면,

*mysqldump: [Warning] Using a password on the command line interface can be insecure.*

warning 메세지가 떨어진다. mysql 5.6 버전 이상부터 password 를 노출하면 이런식으로 경고를 한다.

**2. password 노출 방지를 위해서 mysql_config_editor 를 사용하여 암호화된 파일을 만들어 사용하자**\*

*# mysql_config_editor set \-\-login-path=[명칭] \-\-host=[localhost] \-\-user=[root] \-\-password*

*Enter password:*

요청에 따라 password 입력하고 나면 \-\-login-path 명칭을 이용한 암호화된 로그인 파일을 사용할 준비가 되었다. (계정의 홈 디렉토리에 .mylogin.cnf 파일 생성된다.)

**3. 백업 스크립트를 생성한 암호화된 로그인 방법으로 수정해주자**\*

*# vi backup.sh*

```
TODAY=`/bin/date +%m-%d-%y_%H:%M`

# 계정정보
DATABASE="DUMP하려는 데이터베이스 이름"

mysqldump --login-path=[명칭] -S /경로/mysqld1.sock  $DATABASE | gzip -c > /저장경로/mysql_backup/mysqldump-$TODAY.gz
```

**4. 백업 스크립트 실행**\*

*# sh backup.sh*

\*\* **mysql_config_editor 정리**

-	**등록 내역 list 확인**
	-	#mysql_config_editor print --all
-	**mysql 접속**
	-	#mysql --login-path=dump_usr
-	**특정 접속 정보 삭제**\*
	-	#mysql_config_editor remove --login-path=dump_usr\*
-	**전체 정보 삭제**\*
	-	#mysql_config_editor remove\*
