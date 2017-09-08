---
layout: post
title:  "crontab 으로 자동백업 하기"
date:   2017-09-08
desc: "Crontab 으로 자동백업 하기"
keywords: "centOS7,backup,crontab"
categories: [LINUX]
tags: [centOS7,crontab]
icon: icon-html
---

**crontab 으로 cron job 추가하여 자동으로 백업 스크립트 수행하기**
=========================================================================================

crontab 사용
============

\-e 옵션으로 cron job을 편집할 수 있다.

*# crontab -e*

```
0,20,40 * * * * sh backup.sh
```

이렇게 하면 20분마다 백업 스크립트를 실행한다.

crontab?
========

-	cron ?
	-	프로세스 예약 데몬.
-	crontab ?

	-	스케줄링을 관리하는 프로그램.
	-	cron job을 등록하여 사용.

-	crontab 문법

```
  * * * * * [수행할 명령어]

  각각의 * 을 앞에서 부터 Ⓐ Ⓑ Ⓒ Ⓓ Ⓔ 라 할 때

  Ⓐ = 분 (0-59)
  Ⓑ = 시 (0-23)
  Ⓒ = 일 (1-31)
  Ⓓ = 월 (1-12)
  Ⓔ = 요일 (0-6) (0:일요일, 1:월요일, …, 6:토요일)
```

\* crontab 명령어 옵션
----------------------

```
-e : cron job 수정
-u : root권한자가 user의 crontab 접근 할 때 사용
-l : cron job 리스트 보기
-r : cron job 삭제
```

사용예 )

-	crontab -e -u user
	-	root 권한자가 유저계정이 user인 사용자의 crontab 을 편집
-	crontab -l
	-	crontab 리스트 확인
-	crontab - r
	-	crontab 내용 삭제
-	crontab cron-text.txt
	-	cron-text.txt 파일의 내용을 크론탭에 등록
		-	단, 크론탭 형태로 작성되어 있어야 함

\* crontab 예제
---------------

-	\* \* \* \* \* sh backup.sh
	-	1분마다 backup.sh 수행
-	0,20,40 \* \* \* \* sh backup.sh
	-	0분, 20분, 40분에 backup.sh 를 수행 (20분 마다)
-	\*/20 \* \* \* \* sh backup.sh
	-	0분, 20분, 40분에 backup.sh 를 수행 (20분 마다)
-	0 0,12 * * * sh backup.sh
	-	매일 0시, 12시에 backup.sh 를 수행 (12시간 마다)
-	0 \*/12 \* \* \* sh backup.sh
	-	매일 0시, 12시에 backup.sh 를 수행 (12시간 마다)
-	0 1-23/6 * * * sh backup.sh
	-	1시부터 6시간마다 수행(1시, 7시, 13시, 19시)
-	0 12 * * 1-3 sh backup.sh
	-	월-수요일 12시 backup.sh 수행
-	30 * * * 0,1 sh backup.sh
	-	토요일, 월요일 30분 마다 backup.sh 수행
