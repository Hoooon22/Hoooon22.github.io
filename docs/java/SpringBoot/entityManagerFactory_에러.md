---
layout: default
title: entityManagerFactory 에러
parent: SpringBoot
grand_parent: Java
date: 2024-07-22 21:12:11
category: Java
tags: [Springboot, Java, Error]
---

> [!question]
> 스프링부트 프로젝트에서 게시판을 만들고 있던 중, 게시판 작성 내용을 DB에 저장하는 컨트롤러를 만들던 중 오류가 발생하였다.
### 오류
```bash
***************************
APPLICATION FAILED TO START
***************************

Description:

Parameter 0 of constructor in Service required a bean named 'entityManagerFactory' that could not be found.


Action:

Consider defining a bean named 'entityManagerFactory' in your configuration.>)
```
### 초기 해결 방법
`EntityManagerFactory`를 수동으로 설정하는 방법을 채택

```java
@Configuration

@EnableTransactionManagement

public class JpaConfig {

  

@Autowired

private DataSource dataSource;

  

@Bean

public LocalContainerEntityManagerFactoryBean entityManagerFactory() {

LocalContainerEntityManagerFactoryBean factory = new LocalContainerEntityManagerFactoryBean();

factory.setDataSource(dataSource);

factory.setPackagesToScan("entity");

factory.setJpaVendorAdapter(new HibernateJpaVendorAdapter());

return factory;

}

  

@Bean

public PlatformTransactionManager transactionManager(EntityManagerFactory entityManagerFactory) {

JpaTransactionManager transactionManager = new JpaTransactionManager();

transactionManager.setEntityManagerFactory(entityManagerFactory);

return transactionManager;

}

}
```

- 는 다른 곳이였다... (아래는 해결)

```bash
# JPA 비활성화를 주석처리 ...

# spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```