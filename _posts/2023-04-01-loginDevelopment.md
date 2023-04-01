---
layout: single
title:  "[Java] 로그인,회원가입,게시판 개발"
categories: Java-개발
toc: true
---


[[Java] 개발의 기본순서는 (분석 - 설계 - 코딩)이다.](https://98jungwoo.github.io/java/development/)

위에 포스팅에서 개발을 할때 순서를 지키면서 해야한다는 내용을 다룬적이 있다.

내용을 지키면서 또 알아야할 내용을 이야기하고 간단한 회원가입, 로그인, 게시판을 공유하도록 한다.(본 코드는 데이터베이스와 아직 연동하지 않았으며, 이클립스에서 실행 하여 확인할 수 있는 회원가입, 로그인, 게시판이다.)

# 다이어그램 #

![개발다이어그램](https:/images/2023-04-01-development/개발다이어그램.JPG)

위의 그림은 CRUD의 개발의 흐름을 보여주는 다이어그램이다.

입력view - Controller - Command - Service(CRUD) - Command - DAO - Oracle - DAO - command - Controller - 출력view

이런 형태의 흐름으로 진행이된다.