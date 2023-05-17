---
layout: single
title:  "[Java] Interface(인터페이스)의 개념정리"
categories: Java-객체지향
toc: true
---


<br/><br/><br/>

# Interface(인터페이스)의 개념 #

<br/><br/>

저는 인터페이스를 배울 때가 가장 어려웠습니다. 그렇기 때문에 더욱 공부를 해서 정리를 해놔야겠다는 생각이 들어서 정리해보게 되었습니다. 

<br/>

 - 인터페이스 : 데이터베이스와 연동할 때 사용한다.

 - 추상 : 다른 어플리케이션과 연동한다.(기계적인 내용과 연동할 때 사용한다.)

 - 어노테이션 : XML과 연동할 때 사용한다.(다른 언어하고 연결)

 <br/>

이렇게 3가지를 배울때는 목적을 잊지 말아야합니다. 
<br/>

```java
public class G extends F {

	@Override
	public void go() {
	}

	@Override
	public age() {
		return 0;
	}
}
```
<br/>


```java
public class C implements B{

	@Override
	public void go() {
	}

	@Override
	public age() {
		return 0;
	}
}
```
<br/>

그래야지 비슷한 코드를 봣을 때 헷갈리지 않을 수 있습니다.
<br/><br/>


## 인터페이스 ##

데이터베이스와 연동할 때 사용한다. 
<br/>
- 추상메서드만 가지고 동작한다.(추상 메서드와 동일)

- 데이터베이스와 연동할 때 사용자가 연동한다고 선언하면 데이터베이스 라이브러리에서 연동이 가능한지 확인해준다. 그렇기 때문에 사용자는 어떤 동작으로 작동하는지, 원리가 어떤지 아는건 나중의 일이며, 이미 만들어져있기 때문에 참고 하면 된다. 
ex) 모니터와 컴퓨터가 있을 때 모니터와 본체를 연결해주는 케이블이 인터페이스다. 

- 인터페이스에서는 생성자가 나타자지 않는다. 대신 구현체(~Imp)에서 생성자가 확인된다.

- 변수로 상수만을 가질 수 있음(public, static, final)

- Interface(인터페이스)에서 implements(임프리먼트)한 클래스를 구현 클래스라고 말한다.(= 인터페이스를 구현한다는 말은 인터페이스의 추상 메서드를 완성한다는 의미이다.)
<br/><br/>


## implements(임프리먼트) ##

그리고 정확하게 잡고 가야할 개념은 

- implements(임프리먼트) = 호출하고 실행 (상속X)
- extends(익스텐즈) = 호출 (상속)


- mark(마크): 인터페이스에서 객체가 할수있는 행위에 대해 무엇을 나타내 보이는 일정한 방식, 
              ex) 도로의 표지판처럼 알려주는 기능이다.(표지판처럼 그냥 알려만 주고 그곳에 갈지 말지는 사용자가 정하는 것)

- super(슈퍼): 상속에서 부모클래스를 말한다. 서브 클래스에서 슈퍼 클래스의 구성 요소를 명시적으로 호출할 때사용한다.

<br/><br/>


 ![인터페이스 결과값](https:/images/2023-03-13-interface/예제%20결과값.JPG) 

<br/>




```java

interface InterfaceCreate {
	
public int NUMBER = 10;  // 상수 선언

public void call(); // 추상메서드 선언

}

```

<br/>


```java
public class InterfaceImp implements InterfaceCreate { // InterfaceCreate에 정의된 추상 메서드를 InterfaceImp에서 구현한다.

	@Override

	public void call() {

	System.out.println("인테페이스의 메서드를 상속받아 구현한다.");
		
	}
    
}
```

<br/>


```java
public class InterfaceCall {

  public static void main(String[] args) {
	

	InterfaceImp interfaceImp = new InterfaceImp();
	
	System.out.println("객체 상수는" + InterfaceImp.NUMBER+"이다.");
	
	System.out.println("객체 주소값은 "+ interfaceImp + "이다.");
	
	interfaceImp.call();

	
	
	InterfaceCreate interfaceCreate = new InterfaceImp(); // InterfaceCreate타입이며, InterfaceCreate클래스에 있는 NUMBER과 call메서드만 사용할 수 있다.
	
	System.out.println("인터페이스 상수는 "+ InterfaceCreate.NUMBER + "이다." );
	
	System.out.println("객체 주소값은 " + interfaceCreate + "이다. ");
	
	interfaceCreate.call();
	
  }

}
```

<br/><br/>


## 요약 ##
오늘 인터페이스의 개념에서 이렇게 두가지만 기억해도 성공이다. 
<br/>

★ 
<br/>
 - 인터페이스 : 데이터베이스와 연동할 때 사용한다. 
 - 추상 : 다른 어플리케이션과 연동한다.(기계적인 내용과 연동할 때 사용한다.) 
 - 어노테이션 : XML과 연동할 때 사용한다.(다른 언어하고 연결) 
<br/><br/>

★
<br/>
- implements(임프리먼츠) = 호출하고 실행 (상속X)
- extends(익스텐즈) = 호출 (상속)
<br/><br/>

어려운 만큼 더 열심히 공부하자.