---
title: "Effective Python: Python Unpacking "
date: 2021-04-12T15:51:12+09:00
# thumbnail: "images/effective.jpg"
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

### Effective Python

이펙티브 파이썬이라는 책은 구글 검색 결과 파이썬 중급자들이 읽는 책이라고 설명되어 있는 부분들이 많다. 나는 굳이 파이썬에 대해 초급, 중급, 고급으로 분류를 해 미리 입문의 허들을 높이는 것은 좋지 않다고 생각한다. 하기사 그럴만큼 파이썬의 기본 동작 원리나 내부를 잘 알지 못한 채 다양한 기법을 배우는 것 또한 좋지는 않지만, 도저히 호기심을 이길 수 가 없어 중급이 아님에도 읽어보려한다. 이 책을 보기 앞서 잠깐 INDEX를 살펴본 결과 파이썬 기본 책이나 Docs를 보면 나와있는 목차들의 심화적인 내용을 다루고 있다고 생각하면 편할 듯 하다. </br>

#### ITEM:: FUNCtiONS

ITEM: </br>

- Never Unpack More Than Three Variables When Functions Return Multiple Values
- Prefer Rasing Exceptions to Returning None
- Know How Closures Interact with Variable Scope
- Reduce Visual Noise with Variable Positional Arguments
- Provide Optional Behavior with Keyword Arguments
- Use None and Docstrings to Specify Dynamic Default Arguments
- Enforce Clarity with Keyword-Only and Positional-Only Arguments
- Define Function Decorators with functools.wraps </br>

#### ITEM:19. Never Unpack More Than Three Variables When Functions Return Multiple Values

이 아이템은 함수가 한 개 이상의 값들을 리턴할 때 절대 풀어져 있는 상태, 즉 언패킹이 되어있는 상태로 값들을 리턴하지 말라고 이야기하고 있다.

```python
def get_stats(numbers):
  maximum = max(numbers)
  minimum = min(numbers)
  return minimum, maximum

lengths = [30, 40, 50, 60, 70]
minimum, maximum = get_stats(lengths)
print('Min: {minimum} Max: {maximum}') # >>> Min: 60, Max: 73
```

이 경우는 일반적인 언패킹 방식인데, 기능을 하는 함수의 인스턴스를 만들고 인스턴 스가 반환하는 값들을 각각의 변수로 담아 출력하는 예제를 보이고 있다.

```python
def get_avg_ratio(numbers):
  average = sum(numbers) / len(numbers)
  scaled = [x / average for x in numbers]
  scaled.sort(reverse=True)
  return scaled

lengths = [30, 40, 50, 60, 70]
longest, *middle, shortest = get_avg_ratio(lengths)
print('Longest: {longest:>4.0%}')
print('Shortest: {shortest:>4.0%}')
```

```python
def get_stats(numbers):
  maximum = max(numbers)
  minimum = min(numbers)
  count = len(numbers)
  average = sum(numbers) / count
  sorted_numbers = sorted(numbers)
  middle = count // 2
  if count % 2 == 0:
    lower = sorted_numbers[middle - 1]
    upper = sorted_numbers[middle]
    median = (lower + upper) / 2
  else:
    median = sorted_numbers[middle]

  return minimum, maximum, average, median, count

  minimum, maximum, average, median, count = get_stats(lengths)
  print('Min: {minimum}, Max: {maximum}')
  print('Average: {average}, Median: {median}, Count {count}')
```

이 경우의 문제점은 두 가지라고 소개하고 있는데, 첫째는 많은 언패킹 변수로 인해 에러가 생길 소지가 많다는 것이다. 만약 값을 변수에 담으려고 할 때 사용자가 원했던 변수와 값이 다르게 들어갈 수 있기 때문에(swapped) 에러의 소지가 발생할 수 있고, 둘째는 가독성을 심하게 훼손시킬 가능성이 있다는 것이다. 간단한 예제이지만 만약 변수명이 길 경우 가독성은 상당히 떨어질 수 있음을 직감할 수 있다.

</br>
따라서 3개 이상의 값들을 언패킹 시 가볍게 클래스로 만들어 리턴하거나 튜플 네임스페이스를 이용하는 방식이 더 낫다고 한다.

#### ITEM:21. Know How Closures Interact with Variable Scope

#### ITEM:22. Reduce Visual Noise with Variable Positional Arguments

#### ITEM:23. Provide Optional Behavior with Keyword Arguments

#### ITEM:24. Use None and Docstrings to Specify Dynamic Default Arguments

#### ITEM:25. Enforce Clarity with Keyword-Only and Positional-Only Arguments

#### ITEM:26. Define Function Decorators with functools.wraps </br>
