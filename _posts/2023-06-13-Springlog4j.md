---
layout: single
title:  "[Spring] Log4j(로그) 환경개발"
categories: Spring
toc: true
---
<br><br>

# 스프링 로그환경개발 #

aop는 비즈니스로직과 로그를 완전 분리한거다 (관점지향적인 관점)
<br>
 

![dependency_artifactId](https:/images/2023-06-13-Springlog4j.md/dependency_artifactId.png)

artifactId는 jar의 이름이다 라고 생각해라 
<br><br>


## 로그버전 변경 ##
<br>

![Log4j버전변경1](https:/images/2023-06-13-Springlog4j.md/Log4j버전변경1.png)

내가 버전을 바구려면 
<br>


메이븐레포지토리
[메이븐레포지토리](https://mvnrepository.com/) 여기 들어가서 log4j를 검색.
<br>


메이븐 홈페이지에 들어가서 Usages가 높은 1.2.17의 메이븐작성된거와 같게 바궈줘야함 
<br>

![Log4j버전변경2](https:/images/2023-06-13-Springlog4j.md/Log4j버전변경2.png)

원래는 1.2.15였는데 17로 바군거임.

xml에서는 가독성이 높게 내가 변경한 날짜와 무슨 버전에서 뭘로 바꿨는지 써주면 좋음
<br>


![Log4j버전변경3](https:/images/2023-06-13-Springlog4j.md/Log4j버전변경3.png)
확인해보면 log4j버전이 바뀌여져 있음.
<br><br>



## xml느낌표 제거 ##
<br>

![xml느낌표제거1](https:/images/2023-06-13-Springlog4j.md/xml느낌표제거1.png)

xml에는 이렇게 느김표가 뜨면 안되는데 이거를 지워주기 위해서는 
밑에 작업을 해줘야함
<br>


![xml느낌표제거2](https:/images/2023-06-13-Springlog4j.md/xml느낌표제거2.png)

위에 있는 log4j로 바꿔줘야하고 밑에 있는건 단위테스트 할 때 쓰는거라서 단위테스트 할 때 사용하면 되는거임 

or 변경해주면 되는거임 근데 지금은 안써서 신경 안써도 됨
<br>


![xml느낌표제거3](https:/images/2023-06-13-Springlog4j.md/xml느낌표제거3.png)

참고해서 변경해주기
<br>


![xml느낌표제거4](https:/images/2023-06-13-Springlog4j.md/xml느낌표제거4.png)
<br><br>



## logger 설정 ##
 <br>


![logger설정](https:/images/2023-06-13-Springlog4j.md/logger설정.png)

첫 번째 : min으로 시작하는 모든 패키지에 로그를 찍을 수 있다. 

두 번째 : min.spring.test로 되어있으면 이거로 된거 + 하이패키지도 다 인식해서 로그를 찍을 수 있게 한다.
<br><br>



## debug 설정 ##
<br>

★★★★★★★★★★
(https:/images/2023-06-13-Springlog4j/
![debug설정](https:/images/2023-06-13-Springlog4j.md/debug설정.png)

여기 있는 벨류를  warn을 debug로 바꿔줘야함
<br><br>



## 스프링 기억할 것 ##
<br>

1. 스프링은 라이브러리 확인한다. 버전이 적당하게 개선이 되었으면 개선된거로 내가 변경해준다. (jdk버전이 맞는지 스프링 버전이 ~~인지)

2. xml파일에 들어가서 느낌표를 발생시키지 않는다.(공백제거)

3. xml에서 내가 필요한것들만 파악한다. 로그를 찍을려면 패키지를 설정해줘야하는데 패키지가 설정이 되면 하이에 있는 모든 패키지를 포함시킨다. (min.spring.test이면 min.spring.test.go 도 로그 찍을 수 있음)

4. 맨밑에 있는 root에 있는 벨류를 warn을 debug로 바꾼다.


----------------- 여기까지가 세팅임 그러니까 이거 할줄 알아야함. -----------------

