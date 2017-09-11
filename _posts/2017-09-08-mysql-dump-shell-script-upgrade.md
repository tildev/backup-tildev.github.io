---
layout: post
title:  "MySQL dump - 2 - shell script upgrade"
date:   2017-09-08
desc: "MySQL backup 을 위한 쉘 스크립트"
keywords: "mysqldump,dump,mysqlbackup"
categories: [Mysql]
tags: [mysqldump,dump]
icon: icon-html
---

**MySQL dump (mysql multi) - shell script upgrade**
===============================================

1.백업 스크립트 편집

*# vi backup.sh*

```

TODAY=`/bin/date +%m-%d-%Y_%H:%M`
TODAY_Y=`/bin/date +%Y`
TODAY_M=`/bin/date +%m`
DIRECTORY=/경로/$TODAY_Y/$TODAY_M

# 경로가 되는 Directory 가 없을 경우 디렉토리 만들어 준다.
# mkdir 의 -p 옵션 => 상위 경로도 함께 생성.
if [ ! -d "$DIRECTORY" ]; then
    echo $DIRECTORY
    mkdir -p $DIRECTORY
fi

# 계정정보
DATABASE_A="DUMP하려는 데이터베이스 A"
DATABASE_B="DUMP하려는 데이터베이스 B"

mysqldump --login-path=명칭A -S /mysql_소켓_경로/mysqld1.sock  $DATABASE_A | gzip -c > $DIRECTORY/mysqldump-$DATABASE_A-$TODAY.gz
mysqldump --login-path=명칭B -S /mysql_소켓_경로/mysqld1.sock  $DATABASE_B | gzip -c > $DIRECTORY/mysqldump-$DATABASE_B-$TODAY.gz

# 권한 설정
if [ ! -w "$DIRECTORY" ]
then
    chown -R 유저계정:유저계정 $DIRECTORY
fi

```

이렇게 해서 년/월 별 디렉토리를 생성해서 관리하면 더 좋을 것 같다.
