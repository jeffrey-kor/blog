---
title: "DDD01"
date: 2021-04-27T21:42:35+09:00
draft: true
categories:
  - "Category 1"
  - "Category 2"
tags:
  - "Test"
  - "Another test"
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
## Domain Driven Development
도메인 주도 개발이란, 사전적으로, 비지니스 도메인을 이해하고 도메인을 중심적으로 우선순위를 두어 개발하는 방법론을 의미한다고 한다.

> Domain-driven design (DDD) is the concept that the structure and language of software code
  class names, class methods, class variables) should match the business domain. 
  For example, if a software processes loan applications, it might have classes such as LoanApplication and Customer,
  and methods such as AcceptOffer and Withdraw.

도메인 주도 개발과 설계는 2003년 에릭 에반스가 창시한 개념으로 "유용한 소프트웨어를 개발하고 싶다면 도메인에 귀를 기울여라" 라는 슬로건으로부터 시작되었다고 한다.
다시 말하면 이는, 개발자와, 도메인 전문가, 설계자가 협업하여 고객에게 알맞은 형태의 비지니스를 제공하자는 취지를 가지고 있으며,
최근 협업과 페어 프로그래밍, 그리고 각 분야의 사람들이 합심하여 하나의 복잡하고 거대한 소프트웨어를 효율적으로 만드는데에 중점을 두고 있다.
</br>

#### Goals
도메인 주도 개발의 목표는 위에 언급했듯이 각 분야의 전문가들이 서로 협력하여 하나의 거대하고 복잡한 소프트웨어를 만들기 위해 고안된 소프트웨어
방법론 중 하나이다. 그렇다면 도메인 주도 개발의 지향점은 어떻게 될까? 그 동안 소프트웨어를 개발하면서 고객의 목소리를 듣고 아이디어를 창출해
개발로 이르기까지 다양한 방법론들이 적용되어 왔지만 공통적으로 느끼는 부분은 소프트웨어의 핵심 도메인을 이해하는데 의사소통의 어려움을 많이 겪었다고 한다.
도메인 주도 개발 방법론은 이 의사소통의 어려움을 유비쿼터스 언어(Ubiquitous Language)로 비지니스 규칙과 보편적으로 도메인을 이해하기 위한 언어를 선정함으로서
소프트웨어 개발에 참여하는 도메인 전문가와 설계자, 개발자들의 의사소통의 어려움을 해소하는 것이 첫번째 지향점이다. 
</br>

더 나아가 도메인 주도 개발은 Loose Coupling, High Cohesion으로 결합도는 낮추면서 높은 협력 관계를 통해 복잡한 소프트웨어를 구성해 나아가는 것이 핵심적인 목표다.

#### 도메인 전문가와 협업하는 방식, Event Storming
이벤트 스토밍은 포스트잇을 가지고 객체, 도메인을 표현하며 관계도를 벽에다 붙이면서 능동적으로 소통하는 것을 의미한다.
[그림](url)

