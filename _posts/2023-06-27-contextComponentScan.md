---
layout: single
title:  "[Spring] <context:component-scan>태그 "
categories: Spring
toc: true
---
<br><br>

# xml 어노테이션(스캔) #


![스캔다이어그램](https:/images/2023-06-27-NoUniqueBeanDefinitionException.md/스캔다이어그램.png)

스캔(scan)은 원하는 파일이나 프로그램을 검색하고 찾아내는 과정을 의미.

<context:component-scan>태그를 사용하면 지정된 패키지 내의 모든 클래스에서 어노테이션을 스캔.

스캔한 어노테이션이 붙은 클래스를 자동으로 스프링 컨테이너에 빈으로 등록.
<br>

<context:component-scan> 태그를 선언하면 <context:annotation-config> 태그는 선언할 필요가 없다.

<context:component-scan> 태그는 <context:annotation-config> 태그의 기능을 포함하고 있어 어노테이션을 해석하고 처리하는 역할을 수행을 함.



