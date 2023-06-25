---
layout: single
title:  "[Spring] @MarkerAnno와 @SingleOption"
categories: Spring
toc: true
---
<br><br>

# ★마커어노테이션 #

![마커어노테이션](https:/images/2023-06-25-@MarkerAnno&@SingleOption.md/마커어노테이션.png)



```java

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface MarkerAnno {
	public String call() default "홍길동";
}
```


```xml
Bean.xml

	<!-- MarkerAnno -->
	<bean class="min.spring.custom.MarkerAnnoCall" id="markerAnnoCall"></bean>
```

```java

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

@MarkerAnno
public class MarkerAnnoCall {

	private static final Logger logger = LoggerFactory.getLogger(MarkerAnnoCall.class);

	public static void main(String[] args) {
		ApplicationContext applicationContext = new GenericXmlApplicationContext("bean/Bean.xml");
		logger.info("정보", applicationContext);
		MarkerAnnoCall markerAnnoCall = (MarkerAnnoCall) applicationContext.getBean("markerAnnoCall");
		logger.info("" + markerAnnoCall);
		System.out.println(markerAnnoCall.getClass().getAnnotation(MarkerAnno.class).call());
	}
}
```


# 싱글값 어노테이션 #

Single-value 어노테이션


![싱글값어노테이션](https:/images/2023-06-25-@MarkerAnno&@SingleOption.md/싱글값어노테이션.png)

하나의 요소만 갖는 어노테이션으로 프로토타입 패턴으로 파라미터처럼 사용할 수 있다.

요소값을 설정할 수 있는 요소를 가질 수 있다.

value 엘리먼트로 선언하면 value 요소를 생략할 수 있다.

```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface SingleOption {

	public String call();
}
```
-------------------------------------
```xml
Bean.xml	

	<!-- SingleOption -->
	<bean class="min.spring.custom.SingleOptionCall" id="singleOptionCall"></bean>	
```
-------------------------------------
```java

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

//SingleOption에서 지정한 메서드명이 파라미터가 되었다.
@SingleOption(call = "전우치")
//or
@SingleOptionValue(“전우치”)

public class SingleOptionCall {

	private static final Logger logger = LoggerFactory.getLogger(SingleOptionCall.class);

	public static void main(String[] args) {
		ApplicationContext applicationContext = new GenericXmlApplicationContext("bean/Bean.xml");
		logger.info("정보", applicationContext);
		SingleOptionCall singleOptionCall = (SingleOptionCall) applicationContext.getBean("singleOptionCall");
		logger.info("" + singleOptionCall);
		System.out.println(singleOptionCall.getClass().getAnnotation(SingleOption.class).call());
	}
}
```


