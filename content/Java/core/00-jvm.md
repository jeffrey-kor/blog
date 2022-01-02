---
title: "#00: JVM"
date: 2021-12-23T21:06:33+09:00
draft: true
categories:
  - "CORE JAVA VOLUME I"
tags:
  - "JVM"
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
  
## JVM
> A Java virtual machine (JVM) is a virtual machine that enables a computer to run Java programs as well as programs written in other languages
  that are also compiled to Java bytecode. The JVM is detailed by a specification that formally describes what is required in a JVM implementation.
  Having a specification ensures interoperability of Java programs across different implementations
  so that program authors using the Java Development Kit (JDK) need not worry about idiosyncrasies of the underlying hardware platform.

Java Virtual machine(JVM)이란, 컴퓨터가 자바로 된 프로그램, 그리고 자바 바이트코드로 작성된 다른 프로그램을 실행시키도록 하는 프로그램이다. JVM은 JVM 구현부에서 필요한 것을 공식적으로 서술한
명세서에 의해 구체화되어 있다. 명세서로 구현된 JVM을 가진 자바 프로그램은 특정 하드웨어 플랫폼에 종속적이지 않은 프로그램이며, 이는 모든 곳에 "Write once, run anywhere" 이라는 자바의 철학을 반영하는 가장 중요한 요소이다.
JVM 레퍼런스 구현은 `Hotspot` 으로 불리우는 JIT 컴파일러 포함하는 `OpenJDK` 오픈소스 프로젝트에 의해서 개발되었다. 

## JVM SPECIFICATION

### CLASS LOADER

1.0 클래스 로더란?
1.1 클래스 로더가 수행하는 일:

### VIRTUAL MACHINE ARCHITECTURE
JVM의 아키텍처는 클래스 로더, JVM 메모리, 

{{< figure src="/img/posting/JVM.png" width="100%" >}}

### BYTECODE INSTRUCTIONS
1.0 JVM 아래와 같은 작업을 수행하기 위한 인스트럭션이 존재한다:
  - Load and store
  - arithmetic
  - Type Convention
  - Object creation and manipulation
  - Operand stack management(push / pop)
  - Control transfer(branching)
  - Method Invocation and return
  - Throwing exception
  - Monitor-based concurrency

### JVM LANGUAGE

### BYTECODE VERIFIER
### BYTECODE INTERPRETER AND JUST-IN-TIME COMPILER
### GARBAGE COLLECTION

## JVM IN THE WEB BROWSER
### JAVASCRIPT JVMs AND INTERPRETER
### COMPILATION TO JAVASCRIPT

## JAVA RUNTIME ENVIRONMENT
### PERFORMANCE
  [JAVA RUNTIME PERFORMANCE](https://sungjk.github.io/2019/04/16/java-performance-tuning-4.html)
  [JVM PERFORMANCE TUNING](https://sungjk.github.io/2019/04/16/java-performance-tuning-4.html)
### GENERATION HEAP
  [GENERATION HEAP](https://performeister.tistory.com/60)
### SECURITY


### REFERENCES
[JAVA VIRTUAL MACHINE](https://en.wikipedia.org/wiki/Java_virtual_machine)
[JVM SPECIFICATION]()