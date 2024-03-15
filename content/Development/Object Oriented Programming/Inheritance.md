---
title: Inheritance
thumbnail: ''
draft: false
tags: null
created: 2023-09-29
---

상속은 간단하게 보면 별 문제 없어보이나, 실무적으로 보았을 때 상당히 까다로운 개념이다.

# 상속

* 거의 모든 사람이 OOP의 핵심이라 여김
  * 초창기 OO
  * 재사용성이 궁극의 목적이라 신봉했었음
  * 현재에도 상속 지원하지 않으면 OO 언어라고 보지 않음
* **다형성의 기반**
* 한국 단어 "상속"보다 "계승", "진화", "유전"의 의미가 강하다.

# is-a, has-a

* is-a: 상속관계
  * 자식클래스 is (still) a 부모클래스
  * `Teacher` is (still) a `Person`
* has-a: 컴포지션
  * `WaterSpray` has a `SprayHead`

# 상속 vs. 컴포지션

* 둘 다 재사용을 위한 방법
* 상속으로 가능한 것 컴포지션으로도 가능
  * 기술적인 관점에서 채택
  * 반대도 가능
* 선호는 계속 왔다갔다했음
  * 초창기는 상속 선호
  * 현재는 컴포지션이 답이다라는 잘못된 조언을 따르는 중
* OO에서 큰 결정사항: 상속 vs 컴포지션 중 하나를 고르는 것.

## GuideLine

* 실생활에서 개채들끼리의 관계를 기준으로 선택할 것
  * is-a: 상속
  * has-a: 컴포지션
* 하지만 결국에는 필요에 따라 이 규칙을 어겨야 할 것임

# 사람에게 상속이 어려운 이유

* 컴포지션은 그나마 쉬웠다. 이미 있는 개체를 조립하는 것이니
* 상속은 실세계에서 찾기 어렵다.
* 인간은 실세계에서 직간접적으로 경험한 것을 쉽게 이해한다.
* 하지만 상속은 유전 + 진화다.
* 오랜시간 걸쳐서 진행되는 과정이다.
* 이런 변화를 일반화시키려면 매우 많은 사례가 필요한데, 이를 모두 인지하기엔 인간의 수명이 너무 짧다.
* 따라서 **경험에 기초해서 상속을 이해하기 어렵다.**

# 상속을 이해하는 방법

1. 일반화/특정화 관점
1. 기능의 관점

## 일반화/특정화

![](ObjectOrientedProgramming_10_Inheritance_0.png)

* 아래로 갈 수록 특정한 개체를 의미함
* 위로 갈수록 일반화된 집합을 말함

## 기능

* 공통 클래스를 만들고 그로부터 상속받은 상태와 기능을 재활용
* 즉 재활용하기 위해 사용하는 관점

# 시계 클래스

* 시, 분, 초를 생성자로 받자.
* 그런데 데이터 유효성 검사를 어떻게하지?
* Exception? 이건 당장 좋지 않다.
* **실세계의 시계에서 답을 찾을 수 있다.(아날로그)**
* 태엽을 돌린다는 것에서는 값이 커져도 문제가 생길 수 없다.
* 즉, circular의 구조를 가지기 때문에, 12를 넘는 순간 나머지에 해당하는 값으로 판단된다.
* 여기서 배울 수 있는 점은, **일상의 엔지니어링 방식을 모사하여 프로그램에 넣을 수 있다는 것**
* 구현 방법은 사람마다 다를 수 있으니 생략
  * `clamp(h:m:s:)`: 12를 넘으면 12, 0보다 작으면 0
  * `wrap(h:m:s)`: circular로 만들기

# 상속을 하는 프로그래머의 흔한 사고 방식

* 부모를 만들고 자식을 만든다: X
* 요소를 만들다가 부모로 일반화 한다: O
* **사람은 구체적인 사례들을 더 잘 이해하기 때문**
* 다만, 이미 누군가가 분류를 잘해놨을 때는 그대로 따르면 됨

# 다중 상속

* 디지털, 아날로그 시계를 만든 상태에서 생각해보자.
* 손목시계를 새롭게 만들어야 된다면 `wear()` method는 어디에 추가되어야 할까?
* 손목시계는 디지털도 있고 아날로그도 있다.
* 그렇다고 부모 클래스인 `Clock`에 넣자니 모든 시계가 `wear()` 동작을 하지는 않고..
* 아 벽시계하고 손목시계하고 분리를 해보자.
  * Clock \<- WallClock \<- AnalogClock, DigitalClock
  * Clock \<- WristWatch \<- AnalogWristWatch, DigitalWristWatch
* 손목 시계도 디지털, 아날로그가 있다보니 같은 코드가 중복되네..?
* 상속관계를 바꿔보자.
  * Clock \<- AnalogClock \<- AnalogWallClock, AnalogWristWatch
  * Clock \<- DigitalClock \<- DigitalWristWatch, DigitalWristWatch
* 어.. 그래도 중복이 생기네
* 최선이 뭐지..?

![](ObjectOrientedProgramming_10_Inheritance_1.png)

* source: pocu academy

## 문제점

* Clock을 결과적으로 두번 상속받고 있다.
* 잘못 사용하면 **매우 복잡해진다.**
* Java는 다중 상속 지원 X, C++ 지원
* 죽음의 다이아몬드(the Deadly Diamond of Death; DDD)의 문제가 발생할 수도 있다.
  * 같은 method를 가진 A, B 두개의 클래스를 다중상속받는 C 클래스가 어떤 method를 호출해야할지 애매함을 가진다는 문제

## 다중 상속이 생기는 이유

* **전혀 다른 양상(Aspect)의 특징을 상속받으려 하기 때문에 발생한다.**
* 최상위 부모(`Clock`): 시간을 기록하는 기능
* Analog vs Digital: 어떻게 표현하는가?
* Wall vs Wrist: 어디에 장착하는가?
* **"표현"과 "장착"은 완전히 다른 개념이다.**

## Java에서의 해결법

1. `wear()`와 `mount()`를 추상화하자.
   * 어디에 붙이는 거잖아?
   * `attach()`로 퉁치자.
   * 시계를 차다 -> 시계를 붙이다
   * 시계를 벽에 걸다 -> 시계를 벽에 붙이다.
   * 단, 너무 심한 추상화는 의미를 해칠 수 있음
1. `Interface`: 이게 보다 나은 방법

# 깊은 상속의 어려움과 생물 분류

* 여기서 갑자기 애플워치 같은 것이 들어간다면..?
* 토나온다.
* 이런 것을 "깊은 상속"이라 한다.
* 깊은 상속은 어렵기 때문에 1~2단계만 상속하는 것이 보통이다.
* 깊어질수록 추상화 능력이 더 필요하다. n단계 일반화가 필요.
* 하지만.. 추상화는 인간에게 어려운 방식. 실수할 가능성도 증가

# Reference

* [Pocu Academy](https://pocu.academy/ko)
* [Taxonomic rank](https://en.wikipedia.org/wiki/Taxonomic_rank)
* [다중 상속](https://ko.wikipedia.org/wiki/%EB%8B%A4%EC%A4%91_%EC%83%81%EC%86%8D)
* [Multiple inheritance](https://en.wikipedia.org/wiki/Multiple_inheritance)