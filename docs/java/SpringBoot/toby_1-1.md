---
layout: default
title: 토비의 스프링 1권 1장 - 오브젝트와 의존관계
parent: SpringBoot
grand_parent: ★ Java
data: 2024-09-24 20:41:36
---

# 토비의 스프링 1권 1장 - 오브젝트와 의존관계
{: .no_toc }

## 2024.09.24 (TUE)
{: .no_toc .text-delta }

---

## 스프링의 핵심 철학
> 객체지향 프로그래밍이 제공하는 오브젝트에 집중한다.

스프링은 객체지향 설계와 구현에 관해 특정한 모델과 기법을 억지로 강요하지는 않는다.
-> 하지만 오브젝트를 어떻게 효과적으로 설계, 구현, 사용, 개선할지에 대한 기준을 알려준다.

## 오브젝트의 동일성과 동등성
- **직접 생성한 팩토리 오브젝트**는 오브젝트를 만들 때, 매번 다른 오브젝트가 생성된다.

```java
DaoFactory factory = new DaoFactory();
UserDao dao1 = factory.userDao();
UserDao dao2 = factroy.userDao();

System.out.println(dao1);
System.out.println(dao2);
```
> 출력: 
> example.dao.UserDao@118f375
> example.dao.UserDao@117a8bd

- 하지만, **스프링 컨텍스트로부터 가져온 오브젝트**는 동일하다.

```java
ApplicationContext context = new
	AnnotationConfigApplicationContext(DaoFactory.class);

UserDao dao3 = context.getBean("userDao", UserDao.class);
UserDao dao4 = context.getBean("userDao", UserDao.class);

System.out.println(dao3);
System.out.println(dao4);
```
> 출력:
> example.dao.UserDao@ee22f7
> example.dao.UserDao@ee22f7

오브젝트 팩토리와 스프링의 애플리케이션 컨텍스트의 동작방식에 차이가 있기 때문이다.
- **스프링**은 여러 번에 걸쳐 빈을 요청하더라도 매번 동일한 오브젝트를 돌려준다.
- **애플리케이션 컨텍스트**는 오브젝트 팩토리와 비슷한 방식으로 동작하는 IoC 컨테이너이다.
	- 그러면서 싱글톤을 저장하고 관리하는 **싱글톤 레지스트리**이다.
	# 싱글톤 레지스트리란?
	- 왜 싱글톤으로 빈을 만들까?
		- 스프링은 주로 "자바 엔터프라이즈 기술"을 사용하는 서버환경이기 때문이다.
		- 서버 하나당 최대로 초당 수십에서 수백 번씩 브라우저나 시스템으로부터의 요청을 받아 처리할 수 있는 **높은 성능**이 요구된다.
		- 아무리 자바의 성능이 좋아도 요청 한 번에 여러 오브젝트를 만들면,,, 서버 XoX,,,
	- 싱글톤 레지스트리는 private와 스태틱 메소드 만을 사용해야하는 비정상적인 클래스가 아닌 평범한 클래스도 싱글톤으로 사용이 가능하다.