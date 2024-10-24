---
title: Packet
thumbnail: ''
draft: false
tags:
- packet
- network
- data
- bandwidth
created: 2023-10-04
---


 > 
 > 한번에 전송할 데이터의 크기

편지를 내가 썼다. 그 편지를 누군가한테 보내는데, 글자하나하나를 보내지 않는다. 이 때 편지는 우체부 아저씨가 누군가한테 배달하는 단위가 된다. 이와 같은 개념이 패킷이다. 패킷은 데이터를 보내는 데 있어 발생하는 단위이다. 이 패킷의 구조에 대해서는 나중에 알아보자.

# 설명

* 네트워크에서 정보를 주고 받는 단위
  * Package, bucket의 합성어
  * 쉬운 전송을 위해 데이터를 쪼갠 조각
  * 왜 쪼개는가?
    * [Bandwidth](Bandwidth.md) 때문
    * 특정 데이터가 네트워크의 대역폭을 많이 점유하는 경우, 다른 패킷의 전송 흐름을 막을 수 있음
  * 그러면, 너트워크로 정보를 보낼 때, 패킷이라는 단위를 써서 쪼개서 전달하는 경우, 패킷이 섞여서 들어옴
  * 이 순서를 어떻게 맞출까?
    * 패킷의 구조
      * 헤더
        * 목적지
        * 주소
        * 순서
      * 데이터
      * 테일
        * 에러
    * 이렇게 패킷을 순서대로 받아서 목적지에서 재조립하여 데이터를 만든다.
