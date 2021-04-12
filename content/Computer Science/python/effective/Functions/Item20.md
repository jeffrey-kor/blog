---
title: "Effective Python: Return None"
date: 2021-04-12T17:16:48+09:00
draft: true
thumbnail: "images/effective.jpg"
categories:
  - "Python"
  - "Effective Python"
tags:
  - "Effective python"
  - "이펙티브 파이썬"
  - "아이템 19"
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

#### ITEM:20. Prefer Rasing Exceptions to Returning None

이번 아이템은 함수의 예외에 대한 내용인데 초보 몽키님과 타 블로거분들의 블로그를 참고하면서 천천히 고민해보았다.

##### What is the Exception and Why important?

예외란 무엇이고 왜 중요할까? 우리는 프로그램을 만들고 배포를 하게 되며, 사용자가 서비스를 받아줬으면 하는 생각으로 프로그램을 작성하게 된다. 하지만, 사용자가 꼭 제공하고자 하는 서비스의 룰을 지키는 것만은 아닐 것이다. 비밀번호를 입력하는 곳에 나의 시스템에서 허용하지 않는 포맷을 사용한다던지, 아니면 예기치 못한 연산을 실행하도록 한다던지, 연산이 되지 않는(항상 일정한) 값을 제공 한다던지 등등 지켜줘야 하는 포맷을 지키지 않고서도 필터 코드를 통과한다면 차후에 해당 데이터로 어떠한 기능을 하는 연산을 시행했을 때 시스템은 동작을 멈추게 될 것이다. 이러한 런타임 중에 발생할 수 있는 버그를 **예외**라고 하며 이를 조작하는 것을 일컬어 **예외처리** 또는 **Exception handling**이라고 한다.

> In computing and computer programming, **exception handling** is the process of responding to the occurrence of exceptions – anomalous or exceptional conditions requiring special processing - during the execution of a program. In general, an exception breaks the normal flow of execution and executes a pre-registered exception handler; the details of how this is done depend on whether it is a hardware or software exception and how the software exception is implemented. It is provided by specialized programming language constructs, hardware mechanisms like interrupts, or operating system (OS) inter-process communication (IPC) facilities like signals. Some exceptions, especially hardware ones, may be handled so gracefully that execution can resume where it was interrupted.

> **An alternative approach to exception handling in software** is error checking, which maintains normal program flow with later explicit checks for contingencies reported using special return values, an auxiliary global variable such as C's errno, or floating point status flags. Input validation, which preemptively filters exceptional cases, is also an approach.

##### 파이썬 함수의 예외처리 코드

예외처리를 위한 코드를 작성하기 위해서는 Try ~ catch문이 일반적이고, 유명한 언어에서는 모두 지원한다고 보면 된다. 파이썬에서는 **try ~ except** 코드로 지원하며 일반적인 사용방식은 아래와 같다:</br>

```python
try:
  # 예외를 유발시킬 수 있는 구문
except <# 예외의 종류>
  # 예외 처리를 수행하는 구문
finally
  # 예외의 발생 여부와는 상관없이 실행되는 구문
raise
  # 프로그래머가 직접 예외를 발생시키는 코드
```

**try code block**: 예외가 발생할 수도 있는 코드 <일반적인 코드> </br>
**except code block**: try 코드 블럭에서 발생한 예외를 캐칭해 예외를 처리하는 코드 블럭이다. 여기서 처리라는 것은 해당 예외를 정상적인 상태로 만들어 시스템을 재동작 시킨다는 개념이 아니라 해당 예외를 처리할 수 없음을 인지하고 예외가 발생한 코드를 출력한다던가하는 작업이 실행되는 것이다. </br>
**finally code block**: 예외의 발생 여부와는 상관없이 실행되는 코드 블럭이다.
**raise**: 프로그래머가 예외를 직접 발생시키는 코드 </br>

이렇듯 다양하게 언어적 차원에서 에러에 대한 대응을 하는 모습을 보여주고 있다. 다양한 예외 처리는 [이 블로그](https://gomguard.tistory.com/122)에서 참고해보면 좋을 듯 싶다. 에러가 발생하는 코드는 정말 다양하며, 어떤 입력값을 주었을 때 에러가 발생하는지에 대한 상황 또한 많을 것이다. 적절하게 예외에 대해 대응하며 코드를 작성하는 것만이 에러를 적절하게 마주하는 방법일 것이다. <br>
이번 아이템에서는 함수가 None을 리턴하는 경우에 대해 **raise** 코드 블럭을 이용해보자! 하는 것이다. </br>

```python
def careful_divided(a, b):
  try:
    return a / b
  except ZeroDivisionError:
    return None
```

이 함수는 다음 실행 영역 코드에서의 예외처리를 담당할 수 있다. </br>

```python
x, y = 1, 0
result = careful_divide(x, y)
if result is None:
  print("Invalid inputs")
```

하지만:</br>

```python
x, y = 0, 5
result = careful_divide(x, y)
if not result:
  print("Invalid inputs")
```

이 상황에서는 예외가 발생하지 않고 코드가 실행 된다. 이게 파이썬 코드에서의 False와 같은 의미로 파악하는 일반적인 실수라고 하는데 일반적으로 None은 특별한 의미를 가지고 있다고 한다. **None은 아무것도 없다라는 의미로 쓰이는 자료형인데 타 언어에서는 null로 표현한다고 한다. **값의 부재를 나타낼 때 사용하고, None에 값을 대입할 수 없고 SyntaxError를 발생시킨다고 한다\*\*. </br>
어찌됐건, None을 리턴하게 되면 에러의 상태나 상황을 직관적으로 알수가 없기 때문에 큰 코드 베이스에서의 None 리턴은 상당히 치명적인 코드가 될 가능성이 크다. 이를 피하기 위해서는 튜플 형태로 반환해 언패킹을 해서 변수를 출력해보는 방법이 첫번째 핸들링 방법이라고 한다.

```python
def careful_divide(a, b):
  try:
    return True, a / b
  except ZeroDivisionError:
    return False, None

# example 1
success, result = careful_divide(x, y)
if not success:
  print("invalid inputs")

# example 2
_, result = careful_divide(x, y)
if not result:
  print("Invalid inputs")
```

첫번째 예시에서는 함수의 호출 지점에서 튜플을 언패킹을 해야만 하기 때문에 이는 튜플의 상태를 강제할 뿐만 아니라 아이템 19에서도 보았듯이 Swapping의 위험이 있다. 따라서 이는 잠재적 버그를 만들 수 있으므로 다른 방법을 강구해야 한다.</br>

두번째 예시는 언더스코어 변수라는 것인데, 튜플의 첫번째 요소를 쉽게 무시할 수 있는 기능 중 하나라고 한다. 이 또한 잠재적 버그의 위험한 요소라고 한다. 이쯤 되니 자바가 매우 안정적으로 보이기 시작했다. </br>

```python
def careful_divide(a, b):
  try:
    return a / b
  except ZeroDivisionError as e:
    raise ValueError("Invalid Inputs")
```

이 경우는 특별한 상황에 대해 None을 **절대 리턴하지 않는 방법**이다. 이 예외를 발생시킨 호출 지점에 예외를 직접 발생시키고 호출 지점에서 이 예외를 핸들링 하는것이다. 이는 자바의 throws로 예외를 던지는 기법이랑 비슷하게 보인다. (똑같은가?) 이 코드에서는 `ZerodivisionError`{:.python}에서 `ValueError`{:.python}으로 코드를 바꾸었는데 호출 지점의 입력값이 Bad Input이라는 것을 알려주기 위함이라고 한다. `raise`{:.python}구문을 사용하지 않고 except ~ else 구문을 사용해 핸들링을 하는 방식도 있는데 ITEM을 천천히 익혀 나가다보면 만난다고 하니까 여기서 다루진 않을 생각이다. </br>

```Python
def careful_divide(a: float, b: float) -> float:
  try:
    return a / b
  except ZeroDivisionError as e:
    raise ValueError("Invalid input")
```

이 방식은 **타입 힌팅(Type hinting)** 방식으로 함수 자체를 작성하는 방식인데, 최근 들어 **Typescript** 라던지 동적인 언어에 정적인 요소가 반드시 필요하다는 개념으로 등장한 것 같다. 이런 예외 처리를 어떻게 핸들링 할까를 고민하기보단 애초에 안정성 있는 함수를 작성하는 것이 다양한 예외를 발생시킬 수 있는 코드보다는 낫다고 생각한다.

참고:

- [Exception handling](https://en.wikipedia.org/wiki/Exception_handling)
- [예외처리 Try Catch 남용 시 문제점](https://okky.kr/article/426594)
