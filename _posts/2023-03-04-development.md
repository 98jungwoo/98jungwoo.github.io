---
layout: single
title:  "[Java] MVC모델"
categories: Java-개발
toc: true
---

## 개발의 순서는 [분석 - 설계 - 코딩]이다. ##
<br/>
java를 배운지 14일되었습니다. 근데 개발을 하는 과정에대해서 배워서 기록 해놓을까 합니다.
<br/><br/>

1. 분석<br/>
    > 벤치마킹(구글링) - 단어선정 - 표준화<br/>
2. 설계<br/><br/>
    
3. 코딩<br/>
    > 패키지 생성 - 클래스 생성 - 모델클래스 - 뷰 - 메서드 생성<br/>


이런 순서로 개발을 해야합니다. 그래야 개발의 속도가 빨라지며, 큰 흐름을 파악하는 능력이 발전될 수 있습니다.
<br/><br/><br/>

## 분석 ## 
<br/>
1) 벤치마킹(구글링)
    먼저 내가 만들 프로젝트 관련한 내용을 찾아봐야합니다. 예를 들어 회원정보 검색에 관련된 코딩을 하려고 한다면 구글에 검색해서 찾아보는 과정을 거쳐야 합니다. 
<br/>

 2) 단어선정 
    내가 개발을 할때 필요한 정보를 생각하여 추상화시킨다.

        - 프로젝트 명 : 회원정보 검색

        - 필요정보 : 이름, 나이

        - 필요패키지: service, model, contorl(DB와 연동할때 사용), view 
            > 패키지 명은 어느 회사를 가든 변경하지 않는다고 해서 바로 영어로 적었습니다.

        필요클래스: 검색, 저장, 동작?, 출력

<br/>
 3) 표준화작업 
    정보들의 추상화가 끝났다면 표준화 작업이 필요합니다. 영어단어로 변경해주세요.

        - 프로젝트 명: Member

        - 필요정보 : name, age

        - 필요패키지: service, model, contorl(DB와 연동할때 사용), view .

        필요클래스(메서드) 
            > MemberSearch(membersearch)
            > MemberCommand(MemberCommand, getName, getAge, toString)
            > MembersearchResult(membersearchresult)
            > MemberCall(main)

## 설계 ##
 흐름 <br/>
    콘솔창에서 입력을 받으면 MemberCommand에 저장
    MemberSearch에서 회원정보를 검색
    MembersearchResult에서 회원정보의 유무를 확인한다. -> 없으면 입력으로 반복
    있다면 MemberCall에서 정보를 출력한다.



설계
<br/>
검색할 이름: 임꺽정
해당 회원이 없습니다.

검색할 이름: 홍길동
홍길동 회원의 정보입니다.
이름: 홍길동
나이: 33
<br/> <br/>


## 코딩 ##
1) 패키지 생성
            개발의 시작은 패키지부터 생성해야한다.(단어선정과 표준화를 통해서)
<br/> 

 ![패키지 생성](https:/images/%ED%8C%A8%ED%82%A4%EC%A7%80%EC%83%9D%EC%84%B1.png)  
<br/>
2) 클래스 생성
    필요한 클래스를 생성해놓고 코딩을 시작해야하며, 코딩작성 중 필요한 클래스를 중간 추가하는 방식으로 진행해야한다.
<br/> 

![클래스 생성](https:/images/%ED%81%B4%EB%9E%98%EC%8A%A4%EC%83%9D%EC%84%B1.png)  
<br/>
    저장 클래스 코딩후 호출 클래스 작성하는 순서로 진행한다.
<br/>
3) 모델 세팅
    <br/> 

![모델세팅1](https:/images/%EB%AA%A8%EB%8D%B8%EC%84%B8%ED%8C%85.png)  
<br/>
이런식으로 작성하게 되면 컬럼의 모양으로 저장된다.
<br/><br/>

  ![모델세팅2](https:/images/%EB%AA%A8%EB%8D%B8%EC%84%B8%ED%8C%85%EB%B0%A9%EB%B2%95.png) 
<br/>

- MemberCommand메서드
<br/><br/>

  ![모델세팅2](https:/images/%EB%AA%A8%EB%8D%B8%ED%95%84%EB%93%9C.png) 

<br/>

    이클립스 메뉴 Source-Generate~~fields
<br/>

 - getld, getName, getAge메서드 
<br/><br/>

 ![모델세팅2](https:/images/%EB%AA%A8%EB%8D%B8get.png) 

<br/>
    이클립스 메뉴 Source-Generate getters and setter
<br/><br/>
4) 뷰 메인메서드 작성
    <br/><br/>

5) 매서드 생성
<br/>
코딩 시작전에 설계를 하고, 단어선정, 표준화 작업을 통해서 생각한 메서드를 작성해야 한다.

코딩 전 메서드 작성은 뼈대를 만들어 놓아 전체적인 흐름을 잘 이해하고 파악하기 위함이다.
<br/>



개발의 필요한 순서를 정리해 보았습니다. 


제가 정리하면서 공부하려고 만든 블로그이기 때문에 혹시 읽어보시다가 수정해야할 부분이 있다면 댓글을 달아주면 감사할거같은데 댓글을 쓸곳이 안보이네요.... 공부가 더 필요하겠어요.

감사합니다.
