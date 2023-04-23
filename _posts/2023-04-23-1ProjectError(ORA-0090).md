---
layout: single
title:  "[Java] ORA-0090 오류"
categories: Java-1차ProjectError
toc: true
---

<br/><br/>

# ORA-00904 #

![error](https:/images/2023-04-23-1차프로젝트오류/select(사진)/ORA-00904.png)

ORA-00904: “MEMBEREMAIL “: invalid identifier
(유효하지 않은 식별자-컬럼명이 없음)

<br/><br/>


# 원인1 # 

![원인1](https:/images/2023-04-23-1차프로젝트오류/select(사진)/ORA-00904원인.png)

memberEmail을 호출해야 하는데 마케팅이메일이라는 변수로 호출해서 연동이 안됨
<br/>

# 해결1 #

![해결1](https:/images/2023-04-23-1차프로젝트오류/select(사진)/ORA-00904해결.png)
<br/><br/>


# 원인2 # 

![원인2-2](https:/images/2023-04-23-1차프로젝트오류/select(사진)/ORA-00904원인2.png)

![원인2-1](https:/images/2023-04-23-1차프로젝트오류/select(사진)/ORA-00904원인2-1.png)

memeberEmail 로 잘못 작성하여 없는 컬럼명을 사용하게 되었기 때문에 오류가 발생

<br/>

# 해결2 #

![해결](https:/images/2023-04-23-1차프로젝트오류/select(사진)/ORA-00904해결2.png)

테이블을 다시 작성하여 수정하였음