---
title: "Data structure and Python: STACK"
date: 2021-04-08T18:48:24+09:00
categories:
  - "Data structure"
tags:
  - "Stack"
  - "data structure"
# menu: main # Optional, add page to a menu. Options: main, side, footer
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
#### STACK
> Stack is a linear data structure which follows a particular order in which the operations are performed.
  The order may be LIFO(Last In First Out) or FILO(First In Last Out).

Stack 자료구조는 선형 자료구조이며, LIFO, 즉 후입선출의 데이터 플로우를 가진 자료구조이다. </br>
구현에 따라서 다양하게 디자인을 할 수 있지만 기본적인 동작 방식은 후입선출의 자료구조이다.
함수의 콜스택, 재귀 프로그램의 순서 제어 및 후위 표기법으로 표현된 산술식 연산 등에서도 사용된다고 한다. 
후에 공부할 DFS(Depth first search)에서도 사용한다고 하니 충분히 공부해두어야 겠다.</br>

![StackOnGeeksforGeeks](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/stack.png)

##### Stack Implementation and design
아래 코드는 간단하게 스택 자료구조를 구현한 것이다. 이미 파이썬에서의 배열 관련 함수로 append()와 pop()를 제공하기 때문에 따로 스택 자료구조를
구현할 필요는 없다. 다만 기본 자료구조가 제공하는 오퍼레이션 등은 기억해두고 다른 언어로 구현하는 연습도 해보자.
##### Implementation using built-in Function
{{< gist ef6cd08ef666b81817065e998c012c0c >}}
##### Implementation using singly linked list

##### Time Complexity
작성 예정
##### Space Complexity
작성 예정





















