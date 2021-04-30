---
title: "Nest Overview"
date: 2021-04-29T22:39:00+09:00
draft: true
categories:
  - "Nest.js"
tags:
  - "Nest.js"
thumbnail: "img/placeholder.jpg"
comments: true
authorbox: true
pager: true
toc: true
sidebar: "right"
widgets:
  - "search"
  - "recent"
  - "taglist"
---
## Nest.js
Nest.js는 타입스크립트를 이용해 웹 서버를 구축하는 웹 프레임워크 중 하나이다. 기존에 node.js 기반으로 express 웹 프레임워크를 사용했으나
아키텍처 또는 node.js 기반의 규모가 큰 프로젝트에서 개발자들에게 안정적이며, 확장 가능한 웹 서버를 구축하기 위해 탄생했다. 
Java 기반의 Spring 프레임워크와 유사한 부분이 많고 철학도 비슷한 부분이 있어서 열심히 공부해보려고 한다.  

> Nest is a framework for building efficient, scalable Node.js server-side applications.
  It uses progressive JavaScript, is built with and fully supports TypeScript and combines elements of OOP, FP, and FRP.

#### Advantages
- Modularization
- Dependency Injection
- Swagger API Document
- 

Nest.js는 swagger와 쉽게 연동이 가능해 API 문서화를 손쉽게 할 수 있도록 지원해주고, Dependency Injection 기법을 이용해 객체 지향 설계 기법을 지원한다.
Nest Application의 기본 단위는 Module로 지원하고 있는데 서브 모듈을 각각의 컴포넌트라고 생각하고, 그것들을 합치고 덜어내 서버를 구성하는 것이 가능하다.
구조는 Tree 자료구조 형태를 띄고 있으며 Root module이 존재하며 각각 하위 모듈로 구성이 된다.

#### Structure and Features
main.ts
Application의 `Entry Point` 이다.

{{<gist jeffrey-kor 16392176510901e88aee0110689f6afc >}}

Controller [공식문서](https://docs.nestjs.com/controllers)
Application의 컨트롤러 부분을 담당하고 있다. `@Controller()` 데코레이터와 함께 사용하며, 들어오는 URL에 대한 경로를 지정해주는 역할을 한다.
도메인 단위의 마이크로 서비스에서는 하나의 경량 서버 자체가 하나의 컨트롤러로 처리되어 대규모 서비스에서는 부하 분산을 하도록 권장되고 있지만, MVC 하나의 모놀로틱 서비스에서는
`Controller`가 URL에 대한 분산 라우팅의 역할을 한다. 컨트롤러로 인식되는 클래스 내부에서 라우팅을 처리하기 위한 Rest API를 설계할 수 있는데 이는 다음 데코레이터로 처리할 수 있다.

- `@Get()`
- `@Post()`
- `@Put()`
- `@Delete()`
- `Patch()`

Http 상태코드를 담은 Request Body 같은 JSON 형식의 데이터도 `@Request()` 데코레이터로 받을 수 있고 Request Payload인 DTO 객체에 대해서도 다루어야 하지만,
이는 공식문서의 Controller 편을 더 참고해보고, 클린 아키텍처를 공부하면서 더 작성해 볼 생각이다. 컨트롤러 작성이 끝나면 컨트롤러 자체가 하나의 모듈이므로 `app.module.ts` 에 등록 해주어야 한다.

{{<gist jeffrey-kor aa4992156e897f75a31d6200be0224c8 >}}

Modules [공식문서](https://docs.nestjs.com/modules)
Application의 모듈 부분을 담당하고 있다. `@Module()` 데코레이터로 모듈을 표현하는 Single Object를 정의할 수 있으며 보통 모듈은
기본 값으로 캡슐화가 되어 있다. 따라서 Provider로 의존성 주입을 할 수는 없다고 한다. 모듈 내부는 같은 도메인의 Controller와 Service를 묶고 있으며
도메인을 하나의 모듈로 묶음으로서, Bounded Context와 구성을 깔끔하게 유지할 수 있다는 점에서 Solid 원칙에 위배하지 않으면서 도메인의 룰을 확장시킬 수 있다.

{{<gist jeffrey-kor 11a460f2779dbedade8f378cbf3c1e85 >}}

모듈은 싱글톤 디자인 패턴으로 구성되어 있으며, 여기서 말하는 소프트웨어 디자인패턴에서의 싱글턴 패턴을 따르는 클래스는 **생성자가 여러번 호출되더라도 실제로 생성되는
객체는 하나이고 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴한다는 패턴**이다. 주로 사용처는 Database Connection pool과 같은 곳에서 유용하게 사용한다고 한다.
예제는 DEV 파트에서 디자인 패턴 파트를 따로 생성해서 공부하자!

`$ nest g module 도메인명` Command 명령어로 모듈을 선언할 수도 있고,
`Module` 은 싱글턴 패턴을 따르는 객체로 분류가 되기 때문에 한번 모듈을 선언해놓으면 모듈의 인스턴스를 다른 모듈들이 쉽게 참조할 수 있다.
`Module` 은 `Dynamic Module` 과 `Global Module` 선언 방식도 있다고 하니 추후에 공부하도록 하자.

Provider [공식문서](https://docs.nestjs.com/providers)
Nest에서 `Provider`의 역할은 상당히 중요한데, Nest에서의 기본적으로 클래스로 작성되는 것들은 보통 Provider로 존재한다고 한다.
예를 들어 `Service` 와 `Respoitory` `Factory` `Helper` 등등을 말한다. Provider의 의미는 의존성을 주입할 수 있는 클래스를 말하는데
스프링 프레임워크에서 `@Bean` 으로 등록하는 객체를 의미하는 것 같다. 즉 클래스 하나를 정의하고 `Provider` 객체로 DI를 하기 위해서는
객체 위에 `@Injectable` 이라는 데코레이터를 사용해 IOC 컨테이너에 등록할 수 있다. 이 등록한 Provider를 원하는 객체에서 주입받기 위해서 여러
주입받는 기법 중 하나인 `생성자 주입` 을 이용하는 것 같다. 스프링 진영에서도 필드 인젝션보다는 생성자 인젝션을 권장하는 추세인 것 같다.

`constructor(private catsService: CatsService) {}` 으로 원하는 객체에 의존성을 주입시켜 주면 된다.

app.service.ts
Application의 서비스 부분을 담당하고 있다. 클린 아키텍처에서의 서비스 레이어는 컨트롤러가 받은 데이터를 위임받아 실제 비지니스 로직을 처리하는 레이어다.

{{< gist jeffrey-kor 14d60ed0de75d3a4412afa19fa0ab83f >}}

컨트롤러에서 서비스 레이어의 CatsService를 주입 받아, 들어온 데이터의 처리를 catsService의 `create()` 를 호출해 이를 위임하는 모습을 보여준다.
이 부분은 참고사항인데 async 키워드는 항상 Promise 객체를 반환한다는 사실도 명심해두자.

{{<gist jeffrey-kor ad6365a35384fa85c2d9e7f9ff343565 >}}

서비스 레이어의 CatsService 객체는 `@Injectable()` 을 사용해 객체를 IOC 컨테이너에 등록하는 코드를 보여준다.

Middleware [공식문서](https://docs.nestjs.com/middleware)
미들 웨어의 개념을 알기 위해서 이전에 `express` 프레임워크를 사용해봤다면 쉽게 이해할 수 있을 것 같다. 프로그램의 메인 루틴에 따라 어떤 함수를 호출하기 전,
중간에 한 개 이상의 미들웨어를 끼워 넣어 실행 시키는 중간 단계의 함수나 객체를 말한다.
아래는 `Express` 프레임워크의 미들웨어의 개념이다.

- execute any code.
- make changes to the request and the response objects.
- end the request-response cycle.
- call the next middleware function in the stack.
- if the current middleware function does not end the request-response cycle, it must call next() to pass control to the next middleware function.
  Otherwise, the request will be left hanging.

{{<gist jeffrey-kor 9e5719fa7b46d6dc26ffeca4e8f8ec5d >}}

Nest core에서 `NestMiddleware` 인터페이스를 구현하고 로직을 작성한 후 next() 함수를 호출해 다음 루틴을 실행하도록 할 수 있다. 이를 잘 활용하게 되면
어떤 허가나 인증 또는 필터 등 다양하게 활용해 볼 수 있을 것 같다. 미들 웨어를 작성한 다음은 `app.module.ts` 에 작성한 미들웨어를 등록해주어야 하는데 module 부분에는
등록 할 수 있는 공간이 없다고 한다. 따라서 아래와 같이 모듈 부분에 직접 `NestModule` 인터페이스를 구현하고 등록을 해주어야 한다.

{{gist jeffrey-kor 64bf1bc2c15db61024f4f1b3d72fc4ad >}}

Exception Filter [공식문서](https://docs.nestjs.com/exception-filters)
Nest는 별도의 예외처리 레이어를 가지고 있다. 만약 서버에서 예외가 발생한다면 이 예외처리 레이어에서 예외를 담당하게 된다.
이 예외처리 레이어는 전역 예외처리로 간주되고 수행되는데 만약 인식이 되지 않는 예외가 발생하면 JSON 객체로 500 상태코드를 응답하게 된다.
직접 예외를 던지는 방법도 있는데 이는 통상적인 방법을 이용한다.

{{< gist jeffrey-kor aea3a3f71e6a6c2559038478e1da528f >}}

이 외에도 직접 핸들러를 작성해 예외처리를 해줄 수 있다. 더 자세한 사항은 개발하면서 Overview 이외의 포스트에서 상세히 다뤄보자.

Pipes [공식문서](https://docs.nestjs.com/pipes)
Nest에서 파이프라는 개념은 `PipeTransform` 인터페이스를 구현한 `Injectable()` 데코레이터로 등록된 클래스를 말한다.

**Nest에서 말하는 두 가지의 전형적인 실사용 예:**

- Transformation
- Validation


Guard [공식문서](https://docs.nestjs.com/guards)
Nest에서 가드라는 개념은 `CanActivate` 인터페이스를 구현한 `Injectable()` 데코레이터로 등록된 클래스를 말한다.




Interceptor [공식문서](https://docs.nestjs.com/interceptors)
Nest에서 인터셉터라는 개념은 `NestInterface` 인터페이스를 구현한 `@Injectable()` 데코레이터로 등록된 클래스를 말한다.



Custom Decorators [공식문서](https://docs.nestjs.com/custom-decorators)
Nest is built around a language feature called decorators. 
Decorators are a well-known concept in a lot of commonly used programming languages, but in the JavaScript world, they're still relatively new.
In order to better understand how decorators work, we recommend reading [this article](https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841). Here's a simple definition:

> An ES2016 decorator is an expression which returns a function and can take a target, name and property descriptor as arguments.
  You apply it by prefixing the decorator with an @ character and placing this at the very top of what you are trying to decorate.
  Decorators can be defined for either a class, a method or a property.