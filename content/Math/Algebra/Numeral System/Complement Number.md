---
title: Complement Number
thumbnail: ''
draft: false
tags: null
created: 2024-01-02
---


 > 
 > 보충을 해주는 수.

* 10진법의 경우 3의 보수는 7, 2의 보수는 8이다.
* 즉, 자리수를 높여주기 위한 수를 보수라 한다.

# 왜 사용하는가?

* 컴퓨터는 뺄셈을 처리할 수 없다.
* 또한 하나의 숫자를 표현하기 위한 용량이 제한되어 있다.
* 이러한 필요에서 보수를 사용한 뺄셈을 처리하는 방식을 주로 사용한다.

# 보수를 사용한 계산

* 8 - 3 = 5
* 8 + 7(3의 보수) = 15 -> 자리수 버림 5
* 이와 마찬가지로 이진수에서도 처리할 수 있다.

# 이진법의 경우

* 이진법의 경우 음수를 표현하는 방식에 두가지가 있다.
* 위의 8-3 예시처럼 생각해봤을 때, 00000110의 보수는 11111010이 되어야 할 것이다.
  * 더하면 1 00000000이 된다.
* 이와 같은 방식을 2의 보수라 한다.

## 1의 보수

* 옛날 시스템의 경우 1의 보수를 사용해서 표현하는 경우도 있었다.
* 11111111의 상태를 만드는 것을 목적으로 한다.
* 00000110의 1의 보수는 11111001이 된다.

## 정리

|방식|숫자|표현 결과||||||||
|------|------|-------------|--|--|--|--|--|--|--|
|-|6|0|0|0|0|0|1|1|0|
|1의 보수|-6 (=249)|1|1|1|1|1|0|0|1|
|2의 보수|-6 (=250)|1|1|1|1|1|0|1|0|

* 자리수가 $n$이라 할 때,
* 1의 보수: $-x = (2^n-1) - x$
* 2의 보수: $-x = 2^n - x$

# Reference

* [보수](https://ko.wikipedia.org/wiki/%EB%B3%B4%EC%88%98_(%EC%88%98%ED%95%99))
* 
