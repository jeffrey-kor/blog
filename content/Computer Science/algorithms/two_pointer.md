---
title: "Two_pointer"
date: 2021-04-20T11:31:46+09:00
draft: true
categories:
  - "Algorithms"
tags:
  - "Two Pointer"
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
#### Two Pointer
투 포인터 알고리즘은 1차원 배열에서 두 개의 포인터를 조작해서 원하는 결과를 얻는 알고리즘이다. </br>
나는 투포인터 알고리즘을 이해하기 위해 리트코드를 풀고 있는데, 처음으로 나온 문제는 링크드리스트의 순환 고리가 있는지 여부를 판단하는 알고리즘이었다.

[Two-Pointer](https://leetcode.com/explore/learn/card/linked-list/214/two-pointer-technique/1211/)

{{< rowhtml >}}
    <img src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png" alt="img" />
{{< rowhtml >}}

```
Given head, the head of a linked list, determine if the linked list has a cycle in it.
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.
Return true if there is a cycle in the linked list. Otherwise, return false.
```
이 문제는 그냥 반복해서 풀면 정답은 나오는데 알고리즘의 성능은 향상 시킬 수는 없다. 두 개의 변수를 선언해 공간복잡도를 조금 늘리는 대신
검색 속도의 향상을 올리는 기법이다. <br>
`slow`는 한 칸이동, `fast`는 두 칸이동하여 모든 노드의 head를 검색할 수 있고, 빠르게 다음 노드를 검색할 수 있다.

{{< gist jeffrey-kor 9c1eedbc0a6d3cb1a44d7ee2d02db2d1 >}}

[Two pointer2](https://leetcode.com/explore/learn/card/linked-list/214/two-pointer-technique/1214/)
{{< rowhtml >}}
<img src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png" alt="img" />
{{< rowhtml >}}
```
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.
Notice that you should not modify the linked list.
```
이 문제도 간단하게 풀어볼 수 있을 것 같은데, 반복문을 돌려서 `tail`로 이동하여 해당 노드의 사이클이 있는지, 있다면 사이클의 노드를 반환하고 아니면 `null`을 반환하면 된다.
이 문제 역시 사이클이 있는지를 검사해야하므로 하나의 포인터를 이용해 순회를 하게 되면 무한루프로 돌 가능성이 있다 - 만약 사이클이 있다면.
따라서 두 개의 포인터로 만나는 지점이 있는지 없는지를 판단해서 만약 만나는 지점이 있다면, 사이클이 존재한다고 판단하면 되는 것이다.
{{< gist jeffrey-kor 7d4960690d8820151a2149f8940f8b01 >}}
[문제 풀이](https://leetcode.com/explore/learn/card/linked-list/214/two-pointer-technique/1214/discuss/295776/Share-my-Python3-solution-with-explanation-easy-to-understand)

[Intersection of Two Linked Lists](https://leetcode.com/explore/learn/card/linked-list/214/two-pointer-technique/1215/)
```
Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect.
If the two linked lists have no intersection at all, return null.
```
{{< rowhtml >}}
    <img src="https://assets.leetcode.com/uploads/2021/03/05/160_statement.png" alt="img" />
{{< rowhtml >}}
