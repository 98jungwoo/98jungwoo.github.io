---
layout: single
title:  "[Spring] 의존관계 자동 설정 @Autowired 어노테이션"
categories: Spring
toc: true
---
<br><br>

# 의존관계 자동 설정 #

@Autowired- Bytype 방식으로 연결.

@Qualifier-ByName 방식으로 연결할수도 있다.

스프링에서 의존성 주입을 자동화하며 의존성 주입을 처리하는데 사용된다.


![의존관계자동다이어그램](https:/images/2023-06-27-@Autowired.md/의존관계자동다이어그램.png)

스프링 컨테이너에 존재하는 빈 중에서 타입이 일치하는 빈을 자동으로 주입한다.
생성자, setter 메서드, 필드에서 주로사용된다.
<br>

![DI프레임워크표1](https:/images/2023-06-27-@Autowired.md/DI프레임워크표1.png)


![DI프레임워크표2](https:/images/2023-06-27-@Autowired.md/DI프레임워크표2.png)
<br><br>


# @Autowired 어노테이션 #

빈이 존재하지 않거나 빈이 두개이상 존재할 때 @Autowired 어노테이션으로 빈을 설정하게 되면 NoUniqueBeanDefinitionException 예외가 발생할 수 있으므로 required 엘리먼트로 조정해야 한다.
<br><br>


## required 엘리먼트 ##

의존성이 필수인지 아닌지를 지정할 수 있다.

기본값은 true이고 생략할 수 있으며 타입의 빈을 찾지 못하면 애플리케이션은 시작되지 않는다.

false로 값을 설정하면 설정 파일과 관련 있는 빈이 없어도 예외가 발생하지 않고 null을 출력한다.

@Required 어노테이션을 대체하므로 required 엘리먼트를 설정하면 @Required 어노테이션을 선언하지 않아도 된다.
<br>

```java


public class AutowiredDTO {
	private String name;
	private int age;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	@Override
	public String toString() {
		return "AutowiredDTO [이름=" + name + ", 나이=" + age + "]";
	}

}
```

```java


import org.springframework.beans.factory.annotation.Autowired;

public class AutowiredMethodService {
	
	private AutowiredDTO autowiredDTO;


	// 의존관계를 자동으로 설정한다.
	@Autowired
	// 프로퍼티를 주입하고 set을 제외한 첫 글자가 소문자인 autowiredDTO가 빈이 된다.
	public void setAutowiredDTO(AutowiredDTO autowiredDTO) {
		this.autowiredDTO = autowiredDTO;
	}

}
```

```xml
Bean.xml

<!-- AutowiredDTO @Autowired어노테이션으로 xml에서 autowire가 사라짐 -->
	<context:annotation-config />

	<bean class="min.spring.autowired.AutowiredDTO" id="autowiredDTO">
		<property name="name" value="홍길동" />
		<property name="age" value="22" />
	</bean>
	<bean class="min.spring.autowired.AutowiredMethodService" id="autowiredMethodService" />
```

```java

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class AutowiredMethodCall {

	private static final Logger logger = LoggerFactory.getLogger(AutowiredMethodCall.class);

	public static void main(String[] args) {
		ApplicationContext applicationContext = new GenericXmlApplicationContext("bean/Bean.xml");
		logger.info("정보", applicationContext);
		AutowiredMethodService autowiredMethodService = (AutowiredMethodService) applicationContext
				.getBean("autowiredMethodService");
		logger.info("" + autowiredMethodService);
		System.out.println(autowiredMethodService.getAutowiredDTO());
	}
}
```



![의존관계자동실습결과](https:/images/2023-06-27-@Autowired.md/의존관계자동실습결과.png)
