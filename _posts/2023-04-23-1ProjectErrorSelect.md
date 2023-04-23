---
layout: single
title:  "[Java] select에서 조회안되는 오류"
categories: Java-1차ProjectError
toc: true
---

<br/><br/>

# ORA-00904 #

![error](https:/images/2023-04-23-1차프로젝트오류/select(사진)/샐랙트회원번호0번만뜬다.PNG)

테이블에는 회원번호가 입력한대로 저장이 되는데 조회할때는 0번으로 조회됨.

<br/><br/>


# 원인 # 

![원인](https:/images/2023-04-23-1차프로젝트오류/select(사진)/샐랙트회원번호0번만뜬다원인.PNG)

DAO에서 MemberNum을 호출해야하는데 memberEmail을 호출하여 생긴 오류
<br/>

# 해결 #

![해결](https:/images/2023-04-23-1차프로젝트오류/select(사진)/샐랙트회원번호0번만뜬다해결.PNG)
<br/><br/>