---
layout: single
title:  "[java] 어노테이션의 개념(XML, 리플랙션)"
categories: Java-interface
toc: true
---

<br/><br/>

## annotation(어노테이션) ##

어노테이션 앞에 @기호를 선언한다. @ 기호는 at전치사의 의미로 공간(XML)에서 무슨일이 생기는.... 에 라는 의미다.

- 어노테이션: XML연동
- 각주(목차)처럼 프로그램밍 언어에 영향을 미치지 않으며, 유용한 정보를 제공
- 인터페이스에서는 데이터베이스와 연동할 때 메서드를 연결하면 되지만 XML과 연동할때는 자바에서 멤버변수 메서드, 클래스 등등을 인식할수 있게 설정해 줘야한다. 그렇게 설정해주는 것을 어노테이션이라고 하며, 어노테이션은 타켓을 가지고 잇다. XML에게 내가 메서드야, 클래스야 라고 알려주는 것을 타켓이라고 한다.

```ruby
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

// 어노테이션을 클래스에 적용한다.
// 타겟 어노테이션으로 타입 요소 (타입 열거 상수)를 설정했다. 그래서 적용 대상은 클래스가 되며 클래스 위에 어노테이션을 적용하고 오노테이션으 ㅣ정보를 가져온다.
@Target(ElementType.TYPE)

// 어노테이션을 리플랙션으로 어노테이션의 정보를 얻는다.
// 런타임 보존정택 열거 상수를 설정하였으므로 어노테이션 적용이 유지되는 시점은 바디트 코드 파일까지 어노테이션 정보를 유지하면서 리플랙션을 이용해서 런타임에 어노테이션 정보를 얻는다.
@Retention(RetentionPolicy.RUNTIME)

public @interface MarkerAnno {

	//엘리먼트를 설정하고 다폴드 값을 설정하며 엘리먼트에게 값을 설정하지 않으면 디폴드값으로 호출하낟.
	// 어노테이션에서 내가 콜이라고 선언하고, 여기에 홍길동의 값을 집어 넣으면 홍길동으로 리프랙션이 가능하다.
	public String call() default " 디폴트 값인 홍길동이 출력된다.";

}
```

```ruby
package min.java.annotation;

// 어노테이션 단독으로 설정한다.
@MarkerAnno
public class MarkerAnnoCall {

	public static void main(String[] args) {
		MarkerAnnoCall markerAnnoCall = new MarkerAnnoCall();
		
		// 어노테이션에 설언한 디폴트값을 호출한다..
		// getClass : 현재참조하고 있는 클래스를 확인 할 수 있는 메서드
		//getAnnotation(MarkerAnno.class).call()); = 지정된 유형에 대한 이 요소를 반환하고, 없으면 null을 반환한다.
		// (MarkerAnno.class) 마커어노가 있는 어노테이션을 참조하여 call 엘리먼트를 호출한다.
		// 근데 요소가 없기 때문에 call의 엘리먼트의 디폴트값인 (홍길동)이 호출된다.
		System.out.println(markerAnnoCall.getClass().getAnnotation(MarkerAnno.class).call());
															
//		System.out.println(markerAnnoCall.getClass()); // getClass : 현재 참조하고 있는 클래스를 확인 할 수 있는 메서드
		// 결과 값 : class min.java.annotation.MarkerAnnoCall 
		

	}
}
```

## XML ##
구글에서는 “Extensible Markup Language(XML)를 사용하면 공유 가능한 방식으로 데이터를 정의하고 저장할 수 있습니다. XML은 웹 사이트, 데이터베이스 및 타사 애플리케이션과 같은 컴퓨터 시스템 간의 정보 교환을 지원합니다.” 이라고 정의 되어있습니다.

쉽게 설명하면 개발을 할 때 각 사람들이 사용하는 언어가 다 다르게 되는데 그때 하나의 언어로 통일 하는 것은 어렵습니다. 그럴 때 XML을 이용해서 다른 언어를 사용해도 공유할수 있게 됩니다. 그때 어노테이션을 이용해서 연동할수 있게 되는 것입니다.

또한, 다른 언어에서는 사용할 때 규칙이 있기 마련입니다. 예를들어 HTML에서는 시작할 때 <head/></head> 이런식으로 정해진 규칙이 있지만 XML은 없습니다.(더 자세한 XML의 설명은 다시한번 다루도록 하겠습니다.) 쉽게생각해서 여러가지 언어를 공유해야하는데 규칙이 있게 되면 공유하기가 어렵기 때문이라고 생각하시면 됩니다.

XML의 내용을 자바로 가져올때는 파일 자체를 가져와야 하는데 자바는 JVM에서 작동하기 때문에 파일자체를 JVM으로 가져와야 합니다. 

XML에 대한 내용은 코드를 통해서 설명을 드리고 싶지만 이후 더 배우게 되면 한번 더 이야기해보면 좋을 것 같습니다.

자바와 XML은 서로 다르기 때문에 리프랙션이라는 기법으로 서로를 연결해야합니다.



## Reflection(리플랙션) ##
리플랙션은 구체적인 클래스의 타입을 알지못해도 내부에 잇는 메서드 타입 변수 등이 접근할 수 잇는 자바의 API이다. 바이트 코드로 컴파일 되어 클래스 영역에 위치하는 클래스 정보를 읽어와서 정확한 타입을 알지 못해도 리플랙션을 통해 클래스의 요소를 사용할수 있는 것이다.

쉽게 설명을 해보면 XML에 잇는 내용을 자바로 가지고 와서 수정을 하려면 어렵습니다. 그렇기 때문에 리플랙션을 이용해서 자바의 언어로 (또는 자신이 쓰는 언어로) 수정하기 위해 사용한다고 생각하시면 좋을 것 같습니다.

 즉, 직접 메서드에 들어가서 수정하겠다 라는 의미입니다.

그럼 임포트와 리플랙션의 차이는 
임포트는 다른 패키지 또는 클래스에 잇는 것을 사용하려고 임포트 한다면, 리플랙션은 만들어져있는 것을 재조립한다, 또는 기존에 만들어져 잇는 것을 수정하기 위해서 사용하는 것입니다.

앞 전에는 수정을 할때는 new연산자를 통해서 인스턴스로 선언해주고 수정을 햇습니다. 하지만 리플랙션은 인스턴스로 만드는 것이 아니라 수정하고 싶은 클래스 명을 지정해서 직접 수정하는 것입니다.

<리플랙션>
```ruby
public class ReflectionService {
	private int age;

	public ReflectionService() {

	}
	
	public ReflectionService(int age) {
		this.age= age;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

}
```


```ruby
import java.lang.reflect.*;

public class ReflectionCall {

	// 원시유형 사용법과 관련된 경고를 무시한다.
    // 어노테이션 사용하지 않는 코드 관련 경고를 억제한다.
	@SuppressWarnings("rawtypes")
	public static void main(String[] args) throws ClassNotFoundException {

		// 클래스에 직접 접근하여 할당한다.
		// 리프랙션서비스의 클래스이름을 확인한다.
		Class class1 = ReflectionService.class;

		// 클래스에서 나타내는 내용들의 이름을 문자열로 반환합니다.
		// 배열 유형이아닌 참조유형을 나타내는 경우 이진 이름이 반환된다.
		// 리프랙션서비스의 주소를 출력해볼게
		System.out.println(class1.getName());

		// 이미 로드된 클래스 내에서 다른 클래스에 접근하여 클래스의 요소를 사용한다.
		// 보통은 힙으로 나의 영역으로 가지고 와서 수정했지만 이렇게 사용하면 이건 스택영역 즉 오브젝트영역에석 바로 수정하겠다는 의미야
		// "~~"에 잇는건 내가 직접수정을 하려는 클래스의 주소야 여기잇는 주소의 클래스를 내가 직접 수정할게
		class1 = Class.forName("min.java.annotation.ReflectionService");

		// getDeclaredFields 내가 직접수정하겠다는 클래스의 필드배열을 호출하겠따.
		Field[] field = class1.getDeclaredFields();
		System.out.println(field[0]); // 필드영역 [0]자리에 있는 주소를 출력하겠다.

		// getDeclaredConstructors 내가 직접수정할 클래스(리프랙션한)의 생성자를 호출하겠다.
		Constructor[] constructors = class1.getDeclaredConstructors();
		System.out.println(constructors[0]); // 생성자 [0]자리에 잇는 주소를 출력하겟다.
		System.out.println(constructors[1]); // 생성자 [1]자리에 잇는 주소를 출력하겟다.

		// getDeclaredMethods 리프랙션한 메서드를 호출하겠다.(랜덤으로 접근한다.,,,)
		Method[] methods = class1.getDeclaredMethods();
		System.out.println(methods[0]); // 메서드 [0]자리에 잇는 주소를 출력
		System.out.println(methods[1]); // 메서드 [1]자리에 잇는 주소를 출력
	}
}
```

