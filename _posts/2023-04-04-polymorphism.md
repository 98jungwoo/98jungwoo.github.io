---
layout: single
title:  "[Java] Polymorphism(다형성)"
categories: Java-객체지향
toc: true
---
<br/><br/>

# 다형성 #

## 다형성의 특징 ##

- 다형성이란 모든 프로그램에서 동작하며 타입을 다양하게 사용하다.

- 다형성으로 구현하게 되면 구현되는 구현체에서는 어떤 것을 해도 관여하지 않으며, 탈것 이라고 선언하면, 이것과 관련된 것들을 다양하게 말해준다. 탈것이 아닌 내용은 다형성이 필요가 없습니다.

- 다형성의 특징으로는 얕은 복사를 통해서 구현체를 생성한다.
<br/><br/>

- 업케스팅은 타입을 참조변수로 자동 변환하는 것(뉴에다가 할당시켜주는거)
(부모클래스에 자식클래스를 넣으면 업케스팅)

- 다운케스팅 오버라이드가 일어나고 오버로드 되는 것 (강제형변환)
(자식클래스에 부모클래스를 넣으면 다운케스팅)
<br/><br/>

## 다형성 예시1 ##

프로그램을 개발할 때 인터페이스를 사용해서 메서드를 호출하도록 코딩을 했다면, 구현체를 교체하는 것은 매우 손쉽고 빠르게 할 수 있다. 프로그램 소스 코드는 변함이 없다, 구현체를 교체함으로써 프로그램의 실행 결과가 다양해진다. 이것이 인터페이스의 다형성이다.

예를 들어 인터페이스를 이용해서 프로그램을 개발했다. 인터페이스를 구현한 클래스로 A클래스를 작성하였다. 개발 후, A클래스에 문제가 생겨 다른 클래스를 사용해야 한다. 이런 경우 인터페이스를 구현한 B클래스를 만들고 단 한 줄만 수정해서 프로그램을 재실행 할 수 있다.
<br/>

```java
[프로그램]
I i = new A();  // 삭제
I i = new B();  // 생성

i . method1();
i . method2(); // 수정이 필요 없음
```

```java
interface I {
void method1();
void method2();
}
```
<br/>

즉, 자동차가 바뀌어도 운전자의 기본 운전 방법에는 영향을 주지 않는다는 의미입니다.
여기서 운전자는 인터페이스이며 자동차는 구현체입니다.
<br/><br/>

## 인터페이스의 다형성 기능 ##

구현 대상의 내부 구조를 몰라도 영향을 받지 않는다.

구현 대상의 내부 구조가 변경되어도 영향을 받지 않는다.

구현 대상의 자체를 변경해도 영향을 받지 않는다.
<br/><br/>

## 다형성 예시2 ##

```java
// 추상클래스 생성
abstract class Vehicle { 
	
	// 추상메서드 생성
	abstract void move();
}
```

```java
// 추상클래스에 의해서 car클래스를 선언한다.(상속받았다.)
public class Car extends Vehicle {

	@Override
	void move() {
		System.out.println("도로로 다닌다.");
	}
	
	// Car에서 만든 메서드
	void move2() {
		System.out.println("ehfhfh ekslsek.");
	}

}
```

```java
public class Plane extends Vehicle {

	@Override
	void move() {
		System.out.println("하늘로 다닌다.");

	}


}
```

```java
public class Ship extends Vehicle {

	@Override
	void move() {
		System.out.println("바다로 다닌다.");

	}

}
```

```java
public class VehicleCall {
	public static void main(String[] args) {

		// 인스턴스화 오브젝트로 다형성을 구현하여 인스턴스를 선언한다.
		Vehicle vehicle = new Car(); // Vehicle 클래스에 잇는 메서드만 사용할수 잇다.
		vehicle.move();
		
//		Vehicle vehicle = new Car();  // 그렇기 때문에 car에서 만든 메서드는 불가능해
//		vehicle.move2();
		
		vehicle = new Plane();
		vehicle.move();
		vehicle = new Ship();
		vehicle.move();
	}
}
```
<br/><br/>


## 다형성 예시3 ##

```java
public interface LocalInterface {

	public void call();

}
```

```java
public class LocalUsing implements LocalInterface{

	@Override
	public void call() {
		
	final int localVar = 40;
	System.out.println("로컬변수값 : " + localVar );
		
	}

}
```


```java
public class LocalUsingCall {

	// 앞에가 부모면  A a = new B 업캐스팅   ///  앞에가 자식이면 B b = new  A 다운캐스팅
	public static void main(String[] args) {
		
		// 이렇게 다형성으로 하면 구현체에 있는 상수와, 표준출력이 인터페이스로 저장된다.
		LocalInterface localInterface = new LocalUsing();

		// 인터페이스를 호출한다.
		localInterface.call();

	}
}
```