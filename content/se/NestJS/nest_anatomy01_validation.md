---
title: "Nest Anatomy: Validation"
date: 2021-05-02T19:55:15+09:00
draft: true
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

{{< figure src="/img/posting/nestjs.png" width="100%" >}}

## Validation
클라이언트로부터 데이터를 받을 때 유효한 데이터인지 확인할 필요가 있다. Nest에서는 그런 데이터의 유효성을 위해서 제공하는 몇가지 파이프들이 있는데
한번 알아보자.

##### Several Decorators
`ValidationPipe` `ParseIntPipe` `ParseBoolPipe` `ParseArrayPipe` `ParseUUIDPipe`

### ValidationPipe
[class-validator](https://github.com/typestack/class-validator)를 이용하는 파이프인데, 선언형 데코레이터로 이를 주입할 수 있다.
`ValidationPipe` 는 유효성 규칙을 편리하게 이용할 수 있도록 도와주고, 모든 클라이언트에서 접근하는 페이로드에 대해 규칙을 적용할 수 있다고 한다.
다른 포스팅에서 언급하지만 파이프가 존재하는 목적은 일반적으로 두가지로 말할 수 있다.
- Transformation: 들어오는 데이터를 내가 원하는 폼으로 바꿔줄 수 있다. --- JSON -> DTO ---
- validation: 들어오는 데이터가 유효한지 검사하는 역할로 수행된다.


### Schema based validation

### Class Validation
