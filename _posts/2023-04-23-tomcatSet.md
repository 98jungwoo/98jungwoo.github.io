---
layout: single
title:  "[html] Tomcat(톰켓)정의와 세팅방법"
categories: 프론트엔트
toc: true
---

<br/><br/>

# 웹 애플리케이션 서버 #

사진
![웹동작흐름](https:/images/2023-04-23-tomcatSet.md/웹동작흐름.jpg)

요청된 페이지의 데이터베이스 등의 연동을 위해 요청하는 작업을 수행한다.
웹서버가 직접 애플리테이션 프로그램을 처리하는 것이 아니라, 웹 애플리케이션 서버에 처리를 넘겨주고 처리한다. 웹 서버의 기능들을 구조적으로 분리하여 처리하고자 하는 목적이 있다.
<br/>

- 웹ct가 웹서버에 웹 페이지를 요청한다.

- 웹서버는 웹ct의 요청을 받아서 응답으로 요청 처리의 상태를 사용자에게 전달한다.

- 요청된 웹 페이지의 로직이나 데이터 베이스의 연동을 위해 웹 애플리케이션 서버에 처리를 요청한다.

- 웹 애플리케이션 서버는 데이터베이스와의 연동이 필요하면 데이터베이스 데이터의 처리를 수행한다.

- 웹 애플리케이션 서버는 데이터베이스 작업의 처리 겨로가를 웹 서버에 돌려보낸다.

- 웹 서버는 결과를 다시 웹 클라이언트로 사용자에게 전달하고 동시에 새로운 요청을 한다.
<br/>

웹 애플리케이션에는 종류가 다양하지만 그중에 나는 톰켓을 설치하였다. 
<br/><br/>

## 톰켓 ##
<br/>
톰켓(Tomcat)이란 아파치 재단에서 만든 오픈소스 was(web Application Server)이다. Tomcat은 Java Servlet 과 JSP가 실행할 수 있는 환경을 제공하여 동적인 페이지를 생성한다. 그리고 DB 연결 및 데이터 조작, 다른 응용프로그램과 상호작용이 가능하다. 라고 구글에서 이야기 하고 있으며 
<br/><br/>

## WAS ##
<br/>
WAS란 웹 서버와 웹 컨테이너의 결합으로 이루어진 소프트웨어이다. 웹서버를 포함하고 있기 때문에 웹서버처럼 사용할 수도 있습니다. DB와 연결되어 트랜잭션 처리를 하거나 다른 시스템과 연동 기능 또한 포함하고 있습니다. 그리고 웹서버와 달리 요청에 대해 동적인 페이지를 만들어 유연하게 응답할 수 있습니다.
<br/><br/>

## Tomcat 세팅방법 ##
<br/>

### 1. 설치 ###

https://tomcat.apache.org/download-80.cgi

사진톰켓9
![](https:/)

사진톰켓64
![](https:/)

tomcat 9 -> 64-bit Windows 다운

이건 사용하는 환경에 따라 다름. 자신이 사용하는 컴퓨터가 32비트인지 64 비트인지 확인하고 설치해야한다.

<br/>

▶ 압축해제해서 c드라이브에 넣어놓고,	

사진
![](https:/)
<br/><br/>

### 2. 환경변수 설정 ###

zip 파일압축 해제하면 환경변수를 설정해줘야한다. 압축을 풀면 무조건 빈을 등록해줘야한다.

패스(path)에서 bin을 등록해야하는데
패스(Path)는 ‘길’이라는 의미가 있는데 패스에 bin을 등록해주면 bin을 실행하는 위치를 등록해주는거다

즉,  패스(Path)는 실행하는 위치를 가르쳐주는 것을 말한다.
<br/>

▶ CMD창에서 톰켓 시작

사진
![cmd에서톰켓시작](https:/images/2023-04-23-tomcatSet.md/CMD에서톰켓시작.jpg)

확인을 하는데 CATALINA_HOME이 없다고 확인됨 : 등록해줘야함
<br/>

▶ 내컴퓨터 – 속성 – 고급설정 – 고급 – 환경변수 – 시스템변수 – 새로만들기 

![환경변수1](https:/images/2023-04-23-tomcatSet.md/환경변수1.jpg)


![환경변수2](https:/images/2023-04-23-tomcatSet.md/환경변수2.jpg)
C드라이브에 설치한걸로(톰켓9. ~~~) 폴더를 등록하기
<br/>

▶ 시스템변수 – Path- 편집 – 찾아보기- c드라이브의 설치파일에 bin- %CATALINA_HOME%\bin 으로 이름변경하기

사진
![환경변수2](https:/images/2023-04-23-tomcatSet.md/환경변수3.jpg)
<br/>

▶ cmd에서 실행하면 자바 뭐가 없다고 뜸 (자바 홈도 등록해야함)

사진
![환경변수4](https:/images/2023-04-23-tomcatSet.md/환경변수4.jpg)
<br/>

▶ 내컴퓨터 – 속성 – 고급설정 – 고급 – 환경변수 – 시스템변수 – 새로만들기 

사진
![환경변수5](https:/images/2023-04-23-tomcatSet.md/환경변수5.jpg)
C드라이브 - 프로그램 파일 – java – jdk폴더 등록하기
<br/>

▶ 시스템변수 – Path- 편집 – 찾아보기- c드라이브의 설치파일- %JAVA_HOME%\bin 으로 이름변경하기

사진
![환경변수6](https:/images/2023-04-23-tomcatSet.md/환경변수6.jpg)
설치하고 cmd창 열어서 startup치면 이상한 언어나오면서 촤라락 되면 설치 된거임

<br/><br/>

### cmd에서 명령어 안치고 실행 or 종료하는 방법 ###

 C:\apache-tomcat-9.0.74\bin

 ![cmd명령어안치고실행](https:/images/2023-04-23-tomcatSet.md/cmd명령어안치고실행.jpg)

 사진(관리자모드실행)
 ![cmd명령어안치고실행2](https:/images/2023-04-23-tomcatSet.md/cmd명령어안치고실행2.jpg)
 관리자 권한으로 실행하면 (startup)실행  or  (shutdown)종료 할수 있다.

 가끔 명령어해서 인식이 안될때가 있어서 이렇게 하는 방법도 있다고 알려주셨다. 
<br/><br/>

 ### 이클립스에서 html 사용하기 ###

이건 내가 이클립스를 사용하기 때문에 설정하는 방법을 적었다.

![이클립스에서html사용하기](https:/images/2023-04-23-tomcatSet.md/이클립스에서html사용하기.jpg)
<br/>

▶ 이클립스에서 파일 – 스위치 ~ - other   

![이클립스에서html사용하기2](https:/images/2023-04-23-tomcatSet.md/이클립스에서html사용하기2.jpg)
 <br/>

▶ html_workspace 로 런치하기

 사진
 ![이클립스에서html사용하기3](https:/images/2023-04-23-tomcatSet.md/이클립스에서html사용하기3.jpg)
 <br/>

 ▶ file – Dynamic WebProject생성하기

  ![프로잭트생성](https:/images/2023-04-23-tomcatSet.md/프로잭트생성.jpg)
 <br/>

 ▶ 윈도우 – web ~~- 크롬 (이건 내가 편하거로 설정) 
 
 ![클립스에서html사용하기4](https:/images/2023-04-23-tomcatSet.md/이클립스에서html사용하기4.jpg)
 <br/>

▶ 윈도우 – preferences – web – HTML Files – Editor – Syntax coloring

 ![글씨체변경](https:/images/2023-04-23-tomcatSet.md/글씨체변경.jpg)
 왜냐면 나중에 경로볼때 공백을 알아보기가 어려워서 해제 해야함