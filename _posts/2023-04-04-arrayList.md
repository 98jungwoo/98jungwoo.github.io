---
layout: single
title:  "[Java] ArrayList(어레이리스트)와 Vector(벡터)"
categories: Java
toc: true
---

<br/><br/>

![컬랙션](https:/images/2023-03-23-알고리즘/컬랙션.JPG)

<br/><br/>

![컬랙션의인터페이스의 분류](https:/images/2023-03-23-리스트/컬랙션의%20표(List,Set,Map).JPG)
<br/><br/>


# 리스트 #

![어레이리스트와백터비교](https:/images/2023-04-05-arrayList/어레이리스트와%20백터.JPG)
<br/>
순서대로 정리된 요소들을 담는 구조로 순서를 갖는 임의 객체의 집합을 말한다.

데이터의 추가, 데이터의 삭제, 데이터의 중복 허용 등의 기능은 벡터와 같다.

저장한 데이터의 접근은 비순차적 접근 이나 순차적 접근으로 접근한다.

- 인덱스에 요소를 삽입하면 해당 인덱스부터 마지막 인덱스 까지 모두 1씩 밀려난다.

- 인덱스의 요소를 제거하면 바로 뒤 인덱스부터 마지막 인덱스까지 모두 앞으로 1씩 당겨진다.
<br/>

![어레이리스트저장,삭제방법](https:/images/2023-04-05-arrayList/어레이리스트.png)
<br/>

데이터들을 하나의 순차적인 묶음으로 데이터를 검색한다.

각요소에 대한 인덱스를 가지고 있으믈 검색이 매우 빠르다.

단일 스레드에서는 안전하지만, 멀티 스레드에서는 안전하지 않다.

하지만 List 인터페이스로 다형성을 구현하게 되면 멀티 스레드에서도 안전하게 동작할수 있다.
<br/><br/>


# 백터 #

벡터는 크기와 방향을 가지는 양을 나타내는 수학적 개념으로 주로 화살표로 표현된다. 
자바에서 벡터는 동적 배열로 구현된다.(공백도 개수로 치는) 

- 설정된 임계영역은 하나의 스레드로 리소스를 사용할 수 있도록 자동으로 락을 걸어준다.

- 락을 하나씩 가지고 있고, 설정한 락을 가지고 있는 스레드만 임계 영역에 접근 할 수 있다.

- 인덱스에 요소를 삽입하면 해당 인덱스부터 마지막 인덱스 가지 모두 1씩 밀려난다.

- 인덱스의 요소를 제거하면 바로 뒤 인덱스부터 마지막 인덱스 까지 모두 앞으로 1씩 당겨진다.
<br/>

![벡터저장,삭제방법](https:/images/2023-04-05-arrayList/벡터.png)
<br/>

데이터들을 하나의 연속적인 묶음으로 데이터를 저장한다.
<br/><br/><br/>

인원이 많은 경우가 아니라면 어레이리스트를 사용하여 검색하는 것이 좋다. 하지만 인원이 많은 경우라면 벡터를 사용하는 것이 좋다. 그 이유는 어레이리스트는 속도가 빠르다는 특징을 가지고 있다. 인원이 많아서 멀티스레드 환경에서 사용하려면 벡터가 적합하기 때문이다.
