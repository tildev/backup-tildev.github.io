---
layout: post
title:  "rsync 사용해서 원격서버에 백업하기"
date:   2017-09-08
desc: "rsync (remote sync)를 사용해서 원격서버에 백업하기"
keywords: "centOS7,rsync,remote sync"
categories: [LINUX]
tags: [centOS7,rsync]
icon: icon-html
---

**rsync (remote sync)를 사용해서 원격서버에 백업하기**
=============================================================================

---

rsync를 사용해서 원격 서버에 백업
=================================

\#rsync -avzu /백업할 파일 경로/ -e "ssh -p포트번호" 접속계정@원격지IP:/백업파일이 들어갈 원격지 파일경로/

---

많이 사용하는 rsync 옵션
========================

-	-v : 상세정보 표시
-	-r : 재귀적으로 디렉토리 복사.(이 옵션이 있어야 디렉토리 동기화 가능)
-	-a : archive mode. 심볼릭 링크, 파일 유저/그룹 권한, timestamp 복사.
-	-z : 파일 데이터 압축.
-	-e : rsync 커맨드로 사용할 리모트 쉘 프로그램(ssh, rsh) 지정.
-	-u : 동기화할 디렉토리에 원본보다 최신인 파일이 있을 경우, 해당 파일은 동기화 하지 않음.
