---
layout: single
title:  "[Java] log로 값을 확인했을때 null발생 오류"
categories: Java-1차ProjectError
projects: Java-1차ProjectError
toc: true
---


<br/><br/>

# log로 값을 확인했을때 null발생 오류 #

![error](https:/images/2023-04-23-1차프로젝트오류/inselet(사진)/인설트DTOnull값.PNG)


테이블에 값이 입력이 되었는데 log가 null 로 발생.

<br/><br/>


# 원인 # 

![원인](https:/images/2023-04-23-1차프로젝트오류/inselet(사진)/인설트DTOnull값원인.png)

DAO에서 리턴으로 null로 선언 했기 때문에  log로 확인하였을 때 null 발생.



<br/>

# 해결 #

![해결](https:/images/2023-04-23-1차프로젝트오류/inselet(사진)/인설트DTOnull값해결.png)

DAO에서 동작한 내용 log에서 확인하려면 DTO로  반환해줘야 함.

<br/><br/>