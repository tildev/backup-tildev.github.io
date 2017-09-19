---
layout: post
title:  "server Name 가져오기"
date:   2017-09-18
desc: "server Name 가져오기"
keywords: "Java"
categories: [Java]
tags: [java]
icon: icon-html
---

아래와 같은 주소가 있을 경우
http://localhost:8080/test/index.jsp

```
request.getServerName();  
	-> localhost
request.getRequestURI(); 
	-> /test/index.jsp
request.getContextPath(); 
	-> /test
request.getRequestURL();  
	-> http://localhost:8080/test/index.jsp
request.getServletPath(); 
	-> /index.jsp
```