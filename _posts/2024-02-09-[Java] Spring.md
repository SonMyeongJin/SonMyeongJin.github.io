---
title:  "[Java] Spring / Spring Boot"
ccategories: [Backend,Java]
tags:
  [
    spring,
    java
  ] 
image: "/assets/img/title/java.png" 
---

## 스프링

자바에서 사용되는 프레임워크

의존성주입,제어역전, 관점 지향 프로그래밍 을 중심으로 개발된 프레임 워크

### 의존성 주입

```java
@Controller
public class Contorller{
private MySservice service = new MyServiceImpl();
}
```

위 코드는 DI 를 지키지 않은 경우임

컨트롤러가 서비스 객체에 의존을 함 -> 컨트롤러를 수정시 서비스도 수정해야 하는 경우가 생김 / 이러면 테스트도 불편해짐

컨트롤러는 컨트롤러만 , 서비스는 서비스만 구현하도록 설계해야 유지보수 쉬워짐

```java
@Controller
public class Controller{
MyService myService;

@Autowired
public controller(MyService myService){
this.myService=myService;
}
}
```

이건 DI를 지킨 경우임

컨트롤러가 서비스 객체를 의존하지 않음.

그럼 객체를 어떻게 사용하냐? -> 스프링 컨테이너를 통해 주입받음

이떄 생성자를 통한 @Autowired를 사용하거나 config에서 직접 @Bean으로 설정해 줄 수 있음.

이렇게 하면 다른 Service를 사용하고 싶으면 다른 객체를 스프링 빈으로 등록해주면 끝남. ( 다른 소스 수정할 필요 X )

### 관점지향 프로그래밍 ( AOP )

여러곳에서 쓰이는 공통 기능을 모듈화하여 필요한 곳에 연결하여 사용

쉽게말해 각 로직마다 시간을 측정하는 코드를 추가하고싶으면 원하는 곳에 같은 내용을 다 추가해야함. 반복코드를 함수로 묶는것과 비슷

AOP의 장점

공통관심사항과 핵심관심사항으로 분리 할 수 있다.

핵심로직이 별로 중요하지도 않는 공통 기능때문에 코드가 더러워지는 걸 막을 수 있다.

AOP도 구현하고 스프링빈에 등록해서 사용하면 됨

스프링 프레임워크의 대표적인 모듈

- Spring JDBC
- Spring MVC
- Spring AOP
- Spring ORM
- Spring Test
- Spring Expression Language

## 스프링부트

 스프링은 편리하지만 초기설정 너무 복잡. -> 스프링을 좀더 쉽게 사용하기위해 발전

스프링부트가 제공하는 기능

AutoConfig : 자동설정 -> 어플리케이션 개발에 필요한 모든 Dependency를 프레임워크에서 관리

미리 설정되어있는 Starter 프로젝트를 제공

xml 설정 없이 자바코드를 통해 설정가능

스프링은 개발시 사용되는 디펜던시들의 호환되는 버전관리를 해야함 -> 스프링부트가 Starter를 통해 자동으로 호환되는 버전을 관리 ( 이게 리얼 편함 굿 )

실무에서는 스프링부트를 위주로 개발하겠지만 공부할땐 쌩Java -> Spring -> Spring Boot 순서로 개발해봐야지
