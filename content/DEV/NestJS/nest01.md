---
title: "Nest Overview"
date: 2021-04-29T22:39:00+09:00
categories:
  - "Nest.js"
tags:
  - "Nest.js"
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

{{< figure src="/img/posting/nestjs.png" width="100%" >}}

Nest.js는 타입스크립트를 이용해 웹 서버를 구축하는 웹 프레임워크 중 하나이다. 기존에 node.js 기반으로 express 웹 프레임워크를 사용했으나
아키텍처 또는 node.js 기반의 규모가 큰 프로젝트에서 개발자들에게 안정적이며, 확장 가능한 웹 서버를 구축하기 위해 탄생했다.

> Nest is a framework for building efficient, scalable Node.js server-side applications.
  It uses progressive JavaScript, is built with and fully supports TypeScript and combines elements of OOP, FP, and FRP.

Nest가 재미있는 점은 서버를 구성하는 아키텍쳐 요소가 `모듈` 이라는 점인데, 각각의 모듈이 하나의 모듈로 구성되면서 서버를 구축해 나아가는 방식이다.
모듈 단위의 캡슐화가 가능하고 `AOP` 기법도 사용할 수 있다고 한다. 스프링과 상당히 유사한 점도 많다고 느끼지만, 무엇보다 다루기 쉽고, **공식 문서의 설명이
친절한 편**이다.

#### Advantages
- 유지보수가 편하고 확장성 있는 개발이 가능
- 작은단위의 개발부터 큰 규모 있는 개발이 가능
- 수많은 서드파티와의 결합을 손쉽게 제공
- Swagger를 통한 문서화의 편의성 제공

Nest.js는 swagger와 쉽게 연동이 가능해 API 문서화를 손쉽게 할 수 있도록 지원해주고, Dependency Injection 기법을 이용해 객체지향 설계 기법을 지원한다.
Nest Application의 기본 단위는 Module로 지원하고 있는데 서브 모듈을 각각의 컴포넌트라고 생각하고, 그것들을 합치고 덜어내 서버를 구성하는 것이 가능하다.
구조는 Tree 구조 형태를 띄고 있으며 Root module이 존재하며 각각 하위 모듈로 구성이 된다.

{{< figure src="/img/posting/nestjsModule.png" width="100%" >}}

### Overview
`main.ts`

{{<gist jeffrey-kor 16392176510901e88aee0110689f6afc >}}

`Main.ts` 의 전체 코드인데, `bootstrap()` Root module을 `AppModule` 로 잡고 시작하는 모습이다.

##### Controller
Application의 컨트롤러 부분이며 `@Controller()` 데코레이터와 함께 사용하며, 들어오는 URL에 대한 경로를 지정해주는 역할을 한다.
다양한 내장 데코레이터들이 있으며 Restful Api를 설계하기 위한 기본 데코레이터들을 제공한다.

- `@Get()`
- `@Post()`
- `@Put()`
- `@Delete()`
- `@Patch()`

{{<gist jeffrey-kor aa4992156e897f75a31d6200be0224c8 >}}

Http 상태코드를 담은 Request Body 같은 JSON 형식의 데이터도 `@Request()` 데코레이터로 받을 수 있고 Request Payload인 DTO 객체에 대해서도 다루어야 하지만,
이는 공식문서의 Controller 편을 더 참고해보고, 클린 아키텍처를 공부하면서 더 작성해 볼 생각이다. 컨트롤러 작성이 끝나면 컨트롤러 자체가 하나의 모듈이므로 `app.module.ts` 에 등록 해주어야 한다.

##### Module

Application Server 구성 요소의 단위이며,  `@Module()` 데코레이터로 모듈을 표현하는 Single Object를 정의할 수 있다. 보통 모듈은
기본 값으로 캡슐화가 되어 있다. 따라서 Provider로 의존성 주입을 할 수는 없다고 한다. 하나의 모듈은 하나 이상의 도메인과 컨트롤러 서비스 등을 포함하고 있으며
각각 작성된 파일들을 모듈에 등록해주어야 Application이 의존성을 찾아갈 수 있다.

{{<gist jeffrey-kor 11a460f2779dbedade8f378cbf3c1e85 >}}

모듈은 `SingleThon` 디자인 패턴으로 구성되어 있으며, 여기서 말하는 소프트웨어 디자인패턴에서의 싱글턴 패턴을 따르는 클래스는 **생성자가 여러번 호출되더라도 실제로 생성되는
객체는 하나이고 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴하는 패턴**을 말한다. 주로 사용처는 Database Connection pool과 같은 곳에서 유용하게 사용한다고 한다.
예제는 DEV 파트에서 디자인 패턴 파트를 따로 생성해서 공부하자!

`$ nest g module 도메인명` Command 명령어로 모듈을 선언할 수도 있고,
`Module` 은 싱글턴 패턴을 따르는 객체로 분류가 되기 때문에 한번 모듈을 선언해놓으면 모듈의 인스턴스를 다른 모듈들이 쉽게 참조할 수 있다.
`Module` 은 `Dynamic Module` 과 `Global Module` 선언 방식도 있다고 하니 추후에 공부하도록 하자.

##### Provider

Nest에서 `Provider`의 역할은 상당히 중요한데, Nest에서의 기본적으로 클래스로 작성되는 것들은 보통 Provider로 존재한다고 한다.
--- 예를 들어 `Service` 와 `Respoitory` `Factory` `Helper` ---. Provider의 의미는 의존성을 주입할 수 있는 클래스를 말하는데
스프링 프레임워크에서 `@Bean` 으로 등록하는 객체로 봐도 무방하다. 클래스 하나를 정의하고 `Provider` 객체로 Depedency Injection을 하기 위해서는
객체 위에 `@Injectable()` 이라는 데코레이터를 사용해 IOC 컨테이너에 등록할 수 있다. 이 등록한 Provider를 원하는 객체에서 주입받기 위해서 여러
주입받는 기법 중 하나인 `생성자 주입` 을 이용하는 것 같다. 스프링 진영에서도 필드 인젝션보다는 생성자 인젝션을 권장하는 추세인 것 같다.

`constructor(private catsService: CatsService) {}` 으로 원하는 객체에 의존성을 주입시켜 주면 된다.

##### Service
Application의 서비스 부분을 담당하고 있다. 서비스 레이어는 컨트롤러가 받은 데이터를 위임받아 실제 비지니스 로직을 처리하는 레이어다.

{{< gist jeffrey-kor 14d60ed0de75d3a4412afa19fa0ab83f >}}

컨트롤러에서 서비스 레이어의 `CatsService`를 주입 받아, 들어온 데이터의 처리를 catsService의 `create()` 를 호출해 이를 위임하는 모습을 보여준다.
이 부분은 참고사항인데 async 키워드는 항상 Promise 객체를 반환한다는 사실도 명심해두자.

{{<gist jeffrey-kor ad6365a35384fa85c2d9e7f9ff343565 >}}

서비스 레이어의 CatsService 객체는 `@Injectable()` 을 사용해 객체를 IOC 컨테이너에 등록하는 코드를 보여준다.

##### Middleware
[공식문서](https://docs.nestjs.com/middleware)
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

Nest core에서 `NestMiddleware` 인터페이스를 구현하고 로직을 작성한 후 `next()` 함수를 호출해 다음 루틴을 실행하도록 할 수 있다. 이를 잘 활용하게 되면
어떤 허가나 인증 또는 필터 등 다양하게 활용해 볼 수 있을 것 같다. 미들 웨어를 작성한 다음은 `app.module.ts` 에 작성한 미들웨어를 등록해주어야 하는데 module 부분에는
등록 할 수 있는 공간이 없다고 한다. 따라서 모듈을 내보내는 부분에 직접 `NestModule` 인터페이스를 구현하고 등록을 해주어야 한다.

##### Exception Filter

{{< figure src="/img/posting/nestjsException.png" width="100%" >}}

Nest는 별도의 예외처리 레이어를 가지고 있다. 만약 서버에서 예외가 발생한다면 이 예외처리 레이어에서 예외를 담당하게 된다.
이 예외처리 레이어는 전역 예외처리로 간주되고 수행되는데 만약 인식이 되지 않는 예외가 발생하면 JSON 객체로 500 상태코드를 응답하게 된다.
직접 예외를 던지는 방법도 있는데 이는 통상적인 방법을 이용한다.  Nest 의 경우 HttpException 을 base로 상속하여 기본적으로 제공하는 Exception 종류들이 많다.

{{< gist jeffrey-kor aea3a3f71e6a6c2559038478e1da528f >}}

이 외에도 직접 핸들러를 작성해 예외처리를 해줄 수 있다. 더 자세한 사항은 개발하면서 Overview 이외의 포스트에서 상세히 다뤄보자.

##### Pipe

Nest에서 파이프라는 개념은 `PipeTransform` 인터페이스를 구현한 `Injectable()` 데코레이터로 등록된 클래스를 말한다.
Overview 하는 기사이므로 자세한 설명은 생략하지만, 간단하게 이야기를 해보자면 파이프는 HttpRequest 로 넘어온 파라미터나 쿼리 또는 Body 를 Validation 해주거나
원시타입을 조작하거나 원하는 타입이 넘어오지 못했을 때 에러를 발생시킬 수 있는 기능을 담당한다. 자세한 것은 직접 코드를 작성하면서 포스팅 할 예정이다.

##### Guard

Nest에서 가드라는 개념은 `CanActivate` 인터페이스를 구현한 `Injectable()` 데코레이터로 등록된 클래스를 말한다.
Gurads 는 Role에 따라 Route의 수행 여부를 권한 별로 설정할 수 있는 기능이다. 가령 `Admin` 이나 `User` 등을 설정할 수 있다. 자세한 것은 이후 포스팅에서 다룰 예정이다.

##### Interceptor

Nest에서 `Interceptor` 라는 개념은 `NestInterface` 인터페이스를 구현한 `@Injectable()` 데코레이터로 등록된 클래스를 말한다.
Interceptor 는 Request 에서 Response 라이프 사이클에서 특정 함수가 개입하여 처리 및 데이터 조작 또는 로깅 등 다양한 기능을 이룰 수 있는 기능이다.
동작 원리는 다르지만 적용의 이유는 비슷하다고 할 수 있다. 자세한 것은 이후 포스팅에서 다룰 예정이다.

##### Custom Decorators 
Nest가 제공하는 기본 데코레이터 외 추가로 생성해서 주입할 수 있다.
자세한 것은 이후 포스팅에서 다룰 예정이다.

### Summary
Nest를 사용하면서 가장 기뻤던 것은 `공식 문서의 친절함` 이었다. 기능을 만들어놓고 뒤로 숨지 않고 어떻게 하면 프로그래머들이 기능에 대해 조금 더 이해를 도와줄 수 있을까가 보였다.
나같은 초보 개발자가 Spring 부터 시작하려하면 가장 크게 느껴지는 것이 의존성 관련 부분인데 쉽고 빠르게 확장 가능한 아키텍처를 고려한게 Nest 였다. 
앞으로 웹 서버를 고려한다면 Spring 또는 Nest로 정할 것 같다. <br>

부트캠프에서 JavaScript 위주의 개발을 다뤄왔지만 항상 아쉬운 점이 있었다. 주로 함수형 프로그래밍으로 코드를 작성해왔고, 자세한 설계는 뒷전이었다.
물론 역량이 부족한 나이기에 아쉬움이 남는 공부였지만, `Why` 가 없는 공부는 나에게 별다른 도움이 되지 않는다는 것이다. <br>

나는 객체 지향이 구 시대적 소프트웨어 설계 기법이라고 생각하지 않는다.
`Reddit` 이나 간혹 `Youtube` 에서도 추세가 함수형이라서 함수형 프로그래밍을 공부한다 라는 이야기들을 자주 보곤하는데 OOP의 철학은 실 세계의 복잡한 문제를 정적인 코드로 구현할 때 어떻게 소프트웨어를 잘 설계할 수 있을까라는
고민에서 출발했다고 생각한다. --- 물론 생산성 측면에서는 불리한 점이 있을 수 있음 --- 
`Nest.js`는 그런 Node.js의 아쉬움을 덜어내고자 만든게 아닐까하는 생각이 든다. Nest를 아주 잠깐 사용한 것이지만 Spring이 얼마나 많은 고민과 노력 끝에 탄생되었는지 조금이나마 공감할 수 있었고,
앞으로 Nest가 Spring을 뛰어넘는 웹 서버 프레임워크로 발전할 수 있을지 기대하며 Overview를 마친다.