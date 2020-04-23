---
title: "파이썬 GIL이란"
date: 2020-04-23 16:44:30 +0900
categories:
  - python
tags:
  - python
  - gil
classes: wide
---

## 1. GIL이란

- Global Interpreter Lock의 약자로 CPython에서 파이썬 코드를 여러 쓰레드에서 실행할때 인터프리터가 하나의 쓰레드만 파이썬 객체에 접근할 수 있게 제한하는 것이다.

## 2. GIL을 사용하는 이유

- lock을 사용하는 이유는 CPython이 메모리를 관리하는 방법이 thread-safe하지 않기 때문이다.
- 파이썬은 객체의 생성과 소멸을 reference count로 관리한다.
- 만약 두 개의 쓰레드가 하나의 객체를 동시에 참조해 동작을 할 경우 경쟁 상태(race condition)가 되고 reference count의 잘못된 증감으로 메모리 누수가 생기거나 객체가 메모리에서 제거될 수 있다.
- 그래서 파이썬은 해결책으로 객체마다 lock을 거는 것이 아닌 인터프리터에 lock을 걸어 객체에 동시에 접근한는 것을 막았다.

## 3. GIL로 인한 성능 문제

![](/assets/images/python/01-1.png)

- CPU Bound Task일 경우
  - 한 쓰레드에서 점유를 마칠때까지 기다렸다가 다음 쓰레드가 동작함으로 한개의 쓰레드로 실행하는 것보다 context switching 오버헤드 발생으로 더 오래걸릴 수 있다.
- I/O Bound Task일 경우
  - I/O가 많으면 CPU Idle 상태일때가 많아지기 때문에 좋은 성능을 발휘한다.
- 어떤 쓰레드로 넘어가는지 알 수 없다.

## 4. 파이썬 쓰레드 대안

- 계산량이 많은 즉 CPU 사용량이 많은 작업은 쓰레드를 만드는 것이 아니라 프로세스를 만들어 실행한다.
- multiprocessing 모듈을 사용해 프로세스를 만들어 CPU Bound Task를 실행하면 쓰레드를 사용하는 것보다 빠르다.

<br/>
<br/>
<br/>
<br/>

**참고:**

1. https://dgkim5360.tistory.com/entry/understanding-the-global-interpreter-lock-of-cpython
2. https://medium.com/@mjhans83/python-gil-f940eac0bef9
