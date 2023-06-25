---
layout: single
title:  "[Spring] no qualifying bean of type 오류 "
categories: Spring
toc: true
---
<br><br>



# 업캐스팅 빈 한정 #

<h3>no qualifying bean of type 오류</h3>
<br>

스프링 컨테이너에서 주입할 빈을 찾을 수 없을 때 발생하며 발생 원인은 다음과 같다.

- 빈을 등록하지 않았거나 빈을 잘못 등록했을 때 발생한다.

- 같은 타입의 빈이 2개 이상 등록되어 있을 때 선택할 수 없는 상황에서 발생한다.

- 주입하려는 빈의 타입이 잘못되었을 때 발생한다.

- 타입의 빈이 있지만, 필요한 의존성을 주입받지 못했을 때 발생한다.


이거 오류 나오면 (지금 예제에서는 빈을 두가지를 사용하기 때문에 오류가 나온거라)
<br>


다형성과 업캐스팅을 잘못 다룰 때오류가 발생할 수 있다.

인터페이스 타입으로 빈을 주입하려고 할 때 스프링 컨테이너는 해당 타입의 빈을 찾는데 실패할 수 있다.

인터페이스 타입의 빈을 찾으려면 인터페이스를 구현한 구현 클래스의 인스턴스가 필요하기 때문이다.

업캐스팅은 구현체가 인터페이스 타입의 참조 변수로 자동 변환하는 것을 의미한다.


![업캐스팅빈오류발생원인2](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/업캐스팅빈오류발생원인2.png)

업캐스팅으로 인해 인터페이스 타입의 빈을 찾는데 필요한 구체적인 구현체를 찾을 수 없게 되는 것이다.

구체적인 구현체를 명시하지 않거나 적절하게 주입하지 않았다면 오류가 발생하게 된다.
<br>


![Qualifier어노테이션값지정](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/Qualifier어노테이션값지정.png)

qualifier 써주기 (내가 설정되는 이름(messageKr)으로 검색하도록 지정해줘라) 따로 지정해주지 않으면 No qualifying bean of type 오류가 발생
<br><br>

## [1오류] ##


![업캐스팅빈오류1](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/업캐스팅빈오류1.png)

![업캐스팅빈오류2](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/업캐스팅빈오류2.png)
or

![업캐스팅빈component](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/업캐스팅빈component.png)


![업캐스팅빈scan](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/업캐스팅빈scan.png)
이렇게 적어주면 지정한 패키지의 하의 패키지는 다 스캔을 사용할 수 있따  라는 의미 (근데 스캔이 무슨 의미야?- 밑에서 다룰거임)
xml에 저렇게 써주고 무작정 각각 클래스에 컴포넌트 어노테이선 써주면  No qualifying bean of type 오류가 발생 (타입을 못찾는다.) 근데 내가 @qualifier (messageKr)를 적어웠는데 왜 못타입을 못찾아가는지 그거를 알필요가 있음
<br>

[2오류]

![업캐스팅빈오류1](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/업캐스팅빈오류1.png)

![업캐스팅빈오류2](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/업캐스팅빈오류2.png)

1. 스캔 쓰면 오류 못찾는다 

2. 내가 사용하는것들에서 대소문자 잘 구별하거나 아니면 소문자로만 쓰기 

3. 그리고 무작정 컴포넌트를 쓰면 안된다.
<br>

## [실습] ##

```java

public interface Message {
	public String call();
}
```

```java

public class MessageKr implements Message {

	@Override
	public String call() {
		
		return "안녕하세요 :D";
	}

}
```

```java
public class MessageEn implements Message {

	@Override
	public String call() {
		
		return "HELLO :D";
	}

}
```

```xml
Bean.xml
	<!-- Message -->
	<context:annotation-config />
	<bean class="min.spring.qualifier.MessageKr" id="messageKr" />
	<bean class="min.spring.qualifier.MessageEn" id="messageEn" />
	<bean class="min.spring.qualifier.MessageService" id="messageService" />

	<!-- <context:component-scan base-package="min.spring.qualifier"></context:component-scan> -->
```

```java

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

//@Component  // 스캔을 빈에 패키지 잡아주고 여기에 @Component 사용하면 No qualifying bean of type 오류가 발생한다.
			  // 그래서 무작정 @Component를 사용하면 안되는거임
public class MessageService {
	private Message message;

	@Autowired // 의존관계를 자동으로 설정한다.
	@Qualifier("messageKr") // 빈을 한정시켜 예외를 방지하며 생략을 하면 No qualifying bean of type 오류가 발생한다.
	public void setMessage(Message message) {
		this.message = message;
	}

	@Override
	public String toString() {
		return message.call();
	}

}
```


![업캐스팅빈실습결과](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/업캐스팅빈실습결과.png)

