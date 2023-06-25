---
layout: single
title:  "[Spring] Annotation(어노테이션)"
categories: Spring
toc: true
---
<br><br>

# 어노테이션 #

- 어노테이션은 인터페이스의 하나다.

- 시그니처는 누구나 알수있도록 지정해주는걸 시그니처라고 한다.

- 인터페이스는 void인 것 만 조절한다.

- 저장하는 기능이 필요하다.
<br><br>


## 메타데이터 ##

메타데이터 형태로 던져준다.= (가능성이 있는 모든 것 = 클래스를 만들면 생성자, 필드생성자, 필드메서드, 스테틱 메서드, 추상메서드 등 클래스가 동반할 수 있는 내용을 전부다를 가능성 있는 것으로 보는 것을 메타데이터라고한다.)

![메타데이터](https:/images/2023-06-25-SpringAnnotation.md/메타데이터.png)

이때 클래스가 구현이냐, 상속이냐 까지 포함하는게 메타데이터이다. 
<br>

![어노테이션메서드](https:/images/2023-06-25-SpringAnnotation.md/어노테이션메서드.png)

xml기반 어노테이선은 : 설정 파일이 존재한다.

자바기반 어노테이션은 : 설정 파일이 필요하지 않다.
<br>

![어노테이션파라미터](https:/images/2023-06-25-SpringAnnotation.md/어노테이션파라미터.png)

프로토타입을 이용해서 내가 사용한 메서드가 - > 파라미터로 바뀐다.
<br>

![어노테이션순차방식](https:/images/2023-06-25-SpringAnnotation.md/어노테이션순차방식.png)

1. 타겟이 어디인지를 확인할 것

2. 어떨 때 동작할건데? 정책? 등등을 잘 알아야한다.

try...catch, 클로즈 다 해주지 않아도 된다 (@컨트롤)어노테이션이 알아서 해줘서 


컴파일은 내가 저장하는거고 컴파일러는 런타임과 인터프린터가 동시에 있는거
<br><br>

## 어노테이션 수행 ##

어노테이션은 컴파일 타임에 어노테이션 프로세서에 의해 처리된다.

어노테이션의 처리는 반복 처리될 수 있다.

컴파일 과정에서 어노테이션 정보로부터 원본코드에서 새로운 코드를 생성한다.

![어노테이션수행](https:/images/2023-06-25-SpringAnnotation.md/어노테이션수행.png)

스캔 작업 과정에서 보일러플레이트 코드가 생성된다.
<br><br>


### 보일로플레이트코드 ###

보일러플래이트코드: 일반적인 규약으로 생성된 애들은 생략이 가능

보일러 플레이트 코드는 최소한의 수정으로 여러곳에 재사용되고, 반복적으로 비슷한 코드를 의미

ex) 템플릿을 통한 getter 메서드와 setter 메서드의 자동 생성
<br><br>


## Reflection(리플랙션) ##

특정 어노테이션이 선언된 필드나 메서드를 읽어올때는 리플랙션API를 사용

리플랙션은 구체적인 클래스의 타입을 알지 못해도 내부에 있는 메서드, 타입, 변수 등에 접근할 수 있음

바이트 코드로 컴파일 되어 클래스 영역에 위치하는 클래스 정보를 읽어와서 정확한 타입을 알지 못해도 리플랙션을 통해 클래스의 요소를 사용할 수 있다.

![어노테이션리플랙션](https:/images/2023-06-25-SpringAnnotation.md/어노테이션리플랙션.png)

자바는 컴파일 시점에서 타입을 결정하는데, 리플랙션을 사용하여 런타임 시점에 타입을 결정할 수 있다. 
<br>

```java
public class ReflectionService{

	private int age;

	public RelflectionService(){
	}

	public RelflectionService(int age){
		this.age = age;
	}

	public int getAge(){
		return age;
	}

	public void setAge(int age){
		this.age = age;
	}
}

```

```java
import java.lang.reflect.*;
public class ReflectionCall {
	// 원시 유형 사용법과 관련된 경고를 무시한다.
	@SuppressWarnings("rawtypes")
	public static void main(String[ ]args) throws ClassNotFoundException {

		// 클래스에 직접 접근하여 할당한다.
		Class class1 =ReflectionService.class;

		// 클래스의 이름을 호출하여 출력한다.
		System.out.println(class1.getName( ));

		// 이미 로드된 클래스 내에서 다른 클래스에 접근하여 클래스의 요소를 사용한다.
		class1 =Class.forName("min.servlet.begin.ReflectionService");

		// 클래스에서 필드를 호출한다.
		Field[ ]field =class1.getDeclaredFields( );
		System.out.println(field[0]);

		// 클래스에서 생성자를 호출한다.
		Constructor[ ]constructors =class1.getDeclaredConstructors( );
		System.out.println(constructors[0]);
		System.out.println(constructors[1]);

		// 클래스에서 메서드를 랜덤으로 호출한다.
		Method[ ]methods =class1.getDeclaredMethods( );
		System.out.println(methods[0]);
		System.out.println(methods[1]);
		}
	}
```
