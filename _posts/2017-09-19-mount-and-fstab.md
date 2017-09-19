---
layout: post
title:  "Linux mount + fstab 설정"
date:   2017-09-19
desc: "Linux mount + fstab 설정"
keywords: "lunux,mount,fatab,centOS7"
categories: [Linux]
tags: [lunux,mount,fatab,centOS7]
icon: icon-html
---

**Mount 하기**
=============

---

**마운트 할 경로 생성**

*# mkdir /data*

**mount할 장치 확인**
*# fdisk -l*
*# df*

로 마운트 되어야 하는 것, 지금 마운트 되어있는것을 체크해 볼 수 있다.

다음, 마운트 할 장치를 생성한 경로에 마운트 해 주면 된다.

*# mount /dev/sdb2 /data*

 \* 참조 : USB 의 경우 대부분 sdb 이라한다.


---

**부팅시 자동 인식하도록 하기**
=======================

마운트를 하고, 컴퓨터를 부팅하면, 다시 마운트를 해야 한다.

계속적으로 마운트 하고 있어야 하는 장치의 경우

/etc/fstab 에 등록해주면, 부팅시에 자동으로 인식된다.

*# vi /etc/fstab*

```
/dev/sdb2               /data                  ext3    defaults,nofail 0 2
```

이런식으로 해주면 되는데,

각각 필드에 대한 설명을 하자면

1 \- 장치명

2 \- 마운트 할 포인트

3 \- 파일시스템 종류

- \* 참조 \- 리눅스 파일 시스템 확인
- 마운트 후에 확인 한다면
-    # df -Th
- 마운트 전에 확인 한다면
-    # blkid

4 \- 마운트 옵션 (자주 사용하는 몇 가지만)

```
    default : rw, nouser, auto, exec, suid
    rw : 읽기, 쓰기 전용으로 설정
    nouser : root만 마운트 가능
    auto : 부팅시 자동 마운트
    exec : 실행가능
    suid : SetUID, SetGID 허용 
```

5 \- dump 여부
```
 0 : dump 불가능
 1 : dump 가능
```

6 \- 파일시스템 검사 여부 (fsck 무결성 검사 여부)
```
 0 : 검사하지 않음.
 1 : 루트 파일시스템
 2 : 루트 파일시스템을 제외한 나머지 파일시스템
```
