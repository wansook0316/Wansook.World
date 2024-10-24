---
title: Transport Layer
thumbnail: ''
draft: false
tags:
- network
- transport-layer
- TCP
- UDP
created: 2023-10-04
---

# 전송 계층

* [Physical Layer](Physical%20Layer.md), [Data Link Layer](Data%20Link%20Layer.md), [Network Layer](Network%20Layer.md) 이 세개의 계층만 있으면 목적지에 데이터를 보낼 수 있다.
* 하지만 데이터 유실, 손상되는 경우 알수도 없고 해줄게 없다.
* 이를 방지하기 위한 계층이 전송계층이다.
* <mark style='background-color: #fff5b1'> 신뢰성 있는 데이터 전달 </mark>을 위해 필요하다.
* 오류 점검 기능
  * 오류 발생시 데이터 재전송하도록 요청
* 식별 기능
  * 전송된 데이터의 목적지가 어떤 애플리케이션인지 식별 가능
  * 예를 들어, 웹에서 사용된다고 명시되어 있는 패킷을 메일 프로그램에 전달하는 것을 방지한다.

# 연결형 통신 / 비연결형 통신

* 전송 계층의 특징
  * 신뢰성, 정확성
    * 데이터를 목적지에 문제 없이 전달하는 것 -> 연결성 통신(TCP)
  * 효율성
    * 빠르고 효율적으로 전달 -> 비 연결형 통신(UDP)
    * 스트리밍

![](Pasted%20image%2020231004134109.png)
