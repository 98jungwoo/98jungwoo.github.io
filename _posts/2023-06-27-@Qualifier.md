---
layout: single
title:  "[Spring] 특정 빈 선택 @Qualifier"
categories: Spring
toc: true
---
<br><br>


# 특정 빈 선택 # 

같은 타입의 빈이 2개 이상일 때 스프링 컨테이너는 @Autowired 어노테이션을 통해 어떤 빈에 의존관계를 자동 설정해야 하는지 판단하기 어렵다. 

스프링의 초기화 과정에서 다수의 같은 빈이 존재하면 NoUniqueBeanDefinitionException 예외가 발생할 수 있다.


![특정빈예외발생](https:/images/2023-06-27-@Qualifier.md/특정빈예외발생.png)
<br>

예외 발생을 방지하기 위해 @Qualifier 어노테이션을 사용 할 수 있다.

@Qualifier 어노테이션은 다수의 같은 빈이 있을 때 특정 빈을 선택적으로 주입하는데 사용된다.

@Autowired 어노테이션과 함께 사용되어 스프링 컨테이너에 의존관계 자동 설정을 수행할 특벙 빈을 지정할 수 있게 해준다.

@Qualifier 어토테이션은 빈의 이름을 명시하여 예외 발생을 방지하고, 의존관계 설정에서 빈을 한정시킬 수 있다.

같은 타입의 다수 빈이 존재하더라고 @Qualifier 어노테이션으로 특정한 빈만을 사용하도록 한정할 수 있다.

![Qualifier어노테이션](https:/images/2023-06-27-@Qualifier.md/Qualifier어노테이션.png)
<br>


![Qualifier어노테이션사용법](https:/images/2023-06-27-@Qualifier.md/Qualifier어노테이션사용법.png)
<br>

[오류]
오류에서 알게된 내용 : bean.xml에는 <context:annotation-config/>는 한번만 선언하면 됨 빈 설정할때마다 안해줘도 됨

![특정빈실습오류](https:/images/2023-06-27-@Qualifier.md/특정빈실습오류.png)
<br>

[원인]

![특정빈실습원인](https:/images/2023-06-27-@Qualifier.md/특정빈실습원인.png)

어노테이션으로 만드는 테그 안에 내가 빈을 넣어줘서 오류가 난거임
<br>

[해결]

![특정빈실습해결](https:/images/2023-06-27-@Qualifier.md/특정빈실습해결.png)

그래서 어노테이션을 단일 테그로 닫아줘서 이제 qualifierService 빈이 생성되었음
<br>

[결과]

![특정빈실습결과](https:/images/2023-06-27-@Qualifier.md/특정빈실습결과.png)
<br>

```java

public class QualifierDTO {
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
		return "데이터 정보 [이름=" + name + ", 나이=" + age + "]";
	}
}

```

```java


import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;

public class QualifierService {
	
	private QualifierDTO qualifierDTO;

//	의존관계를 자동으로 설정한다.
	@Autowired

//	빈을 한정시켜 예외를 방지하며 생략을 하면 먼저 선언된 빈만 호출되는 논리적 오류가 발생한다.(어노테이션 사용하지 않으면 홍길동, 전우치가 선언되었지만 나중에 선언된 전우치는 안나옴)
	@Qualifier("qualifierDTO2")
	public void setQualifierDTO(QualifierDTO qualifierDTO) {
		this.qualifierDTO = qualifierDTO;
	}
	
	public QualifierDTO getQualifierDTO() {
		return qualifierDTO;
	}

}
```

```xml
Bean.xml
	<!-- QualifierDTO -->
	<context:annotation-config/>
		<bean class="min.spring.qualifier.QualifierDTO" id="qualifierDTO">
			<property name="name" value="홍길동" />
			<property name="age" value="33" />
		</bean>
		<bean class="min.spring.qualifier.QualifierDTO" id="qualifierDTO2">
			<property name="name" value="전우치" />
			<property name="age" value="22" />
		</bean>
		<bean class="min.spring.qualifier.QualifierService" id="qualifierService"/>
```

```java

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class QualifierCall {

	private static final Logger logger = LoggerFactory.getLogger(QualifierCall.class);

	public static void main(String[] args) {
		ApplicationContext applicationContext = new GenericXmlApplicationContext("bean/Bean.xml");
		logger.info("정보", applicationContext);
		QualifierService qualifierService = (QualifierService) applicationContext.getBean("qualifierService");
		logger.info("" + qualifierService.toString());
		System.out.println(qualifierService.getQualifierDTO());
	}
}
```