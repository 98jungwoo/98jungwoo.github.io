---
layout: single
title:  "[Java] ORA-01861 오류"
categories: Java-1차ProjectError
toc: true
---

<br/><br/>

# ORA-01861 #

![error](https:/images/2023-04-23-1차프로젝트오류/inselet(사진)/ORA-01861.png)

ORA-01861: literal does not match 
format string
(포맷 형식과 입력 값 형식이 다름)

<br/><br/>


# 원인 # 

값을 입력할때 199990101 로 입력하였음. 날짜 형식에 맞지 않은 값을 입력하여 오류발생.


<br/>

# 해결 #

19990101 or 990101 로 입력.

<br/><br/>

