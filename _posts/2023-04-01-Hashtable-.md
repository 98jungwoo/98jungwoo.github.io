---
layout: single
title:  "[Java] Map(HashTable)"
categories: Java
toc: true
---

![멥](https:/images/2023-04-01-map/멥의%20내용%20정리.JPG)

비교를 위해 Map포스팅에서 첨부하였던 표를 가져왔다.

<br/><br/>

# Map - HashTable #

- 내부적으로 사용하는 배열을 해시테이블이라고 한다.

- 해시 테이블을 사용하여 데이터를 저장하며, key-value 쌍의 순서가 유지되지 않는다. 

- 중복된 key를 허용하지 않으며, key나 value에 null을 허용하지 않는다. 

- 멀티스레드 환경에서 안전하게 사용할 수 있다.
<br/><br/>


```java
public class SpecificKeyValue {
public static void main(String[] args) {
	
	// 비어있는 새 해시테이블의 인스턴스를 선언한다.
	Hashtable<String, String> hashtable= new Hashtable<String, String>();
	
	// Name = 변수명(키)
	// "홍길동" = 값
	// 설정된 키를 해시테이블의 설정된 값에 매핑하여 넣는다.
	hashtable.put("name", "홍길동");
	hashtable.put("age", "20");
//	hashtable.put("age", "40"); // 이러면 값 충돌이라 age가 40으로 변경되는 일이 발생 한다.
//	hashtable.put("ag2", "20"); // 이러면 키값이 다르기 때문에 값이 같은것은 상관없다. // 키값만 다르면 된다.
	hashtable.put("address", "서울");
	
	System.out.println("전체 : " + hashtable); // 이러면 {} 형태로 출력된다.
	
	// 설정된 키가 매핑되는 값을 반환하여 출력한다.
	System.out.println("이름 : " + hashtable.get("name"));
	System.out.println("나이 : " + hashtable.get("age"));
	System.out.println("이름 : " + hashtable.get("address"));
}
}
```