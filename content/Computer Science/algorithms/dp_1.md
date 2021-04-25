---
title: "Dp_1"
date: 2021-04-23T18:19:10+09:00
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
## Dynamic Programming
동적 프로그래밍이란 문제의 크기가 작은 소문제에 대한 해를 저장해 놓고, 이를 이용하여 크기가 보다 큰 문제의 해를 점진적으로 만들어가는 상향식 접근 방법이다.
- 각각의 소문제는 원래의 문제와 동일하지만 입력의 크기에 줄어듦
- 입력 크기가 아주 작은 단순한 문제가 되면 쉽게 해를 구할 수 있고, 이런 소문제의 해는 다시 사용될 수 있으므로 테이블에 저장
- 해당 소문제의 해가 필요할 때마다 테이블에서 결과를 바로 이용한다.
- 유형:
    - 최적화 문제: 최솟값, 최댓값 구하는 문제
    
- 원리
분할 정복 방법
  - 하향식 접근 방법
  - 상우 레벨의 큰 문제를 순환적으로 부분 배열로 분할하고 이들의 해를 결합해서 원래 문제를 해결하는 방법
  - 알고리즘: 이진 탐색, 합병 정렬, 퀵 정렬, 선택 문제
동적 프로그래밍 방법
    - 상향식 접근 방법
    - 입력 크기가 작은 소문제들을 모두 해결하여 구한 해를 테이블에 저장 후 이 해들을 이용해서 보다 큰 크기의 문제를 해결하는 방법
    - 소 문제들은 독립적이지 않고, 중복되는 부분이 존재
    - 피보나치 수열, 연쇄 행렬 곱셈, 스트링 편집거리, 모든 정점 간의 최단 경로(플로이드 알고리즘), 저울 문제
    
    
동적 프로그래밍 방법의 원리
최적성의 원리(principle of optimality)를 반드시 만족해야 한다
    - 주어진 문제에 대한 최적해는 주어진 문제의 소문제에 대한 최적해로 구성된다. << 이게 만족해야만 DP 를 쓸수있음
동적 프로그래밍 방법의 적용 과정
    - 문제의 특성을 분석해서 최적성으 원리가 성립되는지 확인
    - 주어진 문제에 대해서 최적해를 제공하는 점화식을 도출
    - 가장 작은 소문제부터 점화식의 해를 구해서 테이블에 저장
    - 테이블에 저장된 소문제의 해를 이용하여 점차적으로 큰 상위 문제의 해를 구한다.
    
#### 피보나치 수열 문제
f(n)  = f(n-1) + f(n-2) n>=2 f(0) = 0, f(1) = 1
```java
public (n) {
    f[0] = 0; f[1] = 1;
    for (i=2; i <= n; i++)
        f[i] = f[i-1] + f[i-2]
    return f[n]
}

```
분할정복 방법을 적용한다면?
```java
int f(n) {
  if (n<=0) return 0;
  if (n==1) return 1;
  else { return f(n-1) + f(n-2)
}
```
분할정복 방법으로 풀게되면 소문제가 독립이 아니므로 중복된 계산이 필요 > 매우 비효율적

#### 연쇄 행렬 곱셈 문제
n개의 행렬(M1, M2 ... Mn)을 연쇄적으로 곱하는 경우
- 결합 법칙 성립 -> 여러가지 다른 곱셈 순서가 존재하게 됌 -> 연산에 필요한 곱셈의 횟수가 달라짐(문제) -> 연쇄 행렬 곱셈문제
n개의 행렬을 연쇄적으로 곱할 때 **최적의 곱셈 순서**를 구하는 문제
- 최적의 곱셈 순서 -> 최소의 기본 곱셈 횟수를 갖는 행렬의 곱셈 순서
- 행렬이란? 공부하자 이거

동적 프로그래밍 적용
1. 최적성의 원리가 만족되는지 봐야한다 -> 주어진 문제의 최적해가 주어진 문제의 소 문제에 대한 최적해로서 구성이된다.
2. n개의 행렬을 곱하는 최적의 순서는 n개의 행렬의 어떤 부분집합을 곱하는 최적의 순서를 포함
3. 7개의 행렬을 곱하는 최적의 순서 (M1, M2)((((M3, M4)M5)M6)M7)
-> M3, M4, M5를 곱하는 최적의 순서는 ((M3,M4)M5)
-> 모든 부분 문제들의 최적해로 n개 행렬을 곱하는 최적의 순서를 구할 수 있다.
-> 최적성의 원리를 만족
-> 동적 프로그래밍 방법으로 해결이 가능

4. 점화식 만들어내기 -> 소문제에 대한 해를 구하기 위해
Q) n개의 행렬 Mi(di-1 * di 차원) (1<=i<=n)
도대체 무슨개소린지 모르겠다
j=i=0, 1, (n-1)까지 C(i,j)를 차례대로 계산
   벋붜두버줃ㅂㅈ두버두ㅏㅂㅈ


C(i, i+2) = min(M(Mi+1 + M))

막대기 자르기
53. Maximum Subarray