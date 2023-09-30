---
title: Estimating in ideal days
thumbnail: ''
draft: false
tags: null
created: 2023-09-17
---

# 이상적 시간과 실제 경과 시간

축구 한게임하는데 시간이 얼마나 걸릴까? 누구는 90분, 누구는 3시간이라 말할 것이다. 90분은 이상적 시간에 대응되고, 3시간은 실제 경과 시간에 대응된다고 볼 수 있다. 실질적으로 게임을 하는 시간은 90분이지만, 선수 입장, 휴게 시간 등을 포함하면 3시간 정도라 볼 수도 있다.

실제 경과 시간을 말하는 것보다 이상적 시간쪽으로 추정하는 것이 더 정확하기도 하고 간편하기도 하다. 실제 경과 시간을 여러 불확실성을 고려하여 추정해야 하기 때문에 모든 요소를 고려한 뒤에 대답할 수 있다. 반대로 이상적 시간으로 대답한다면, "축구 경기는 90분 진행돼!" 라고 간단하게 말할 수 있다.

# 이상적 시간과 소프트웨어 개발

* 소프트웨어 개발 프로젝트에서 이상적 시간과 실제 경과 시간 간에 차이가 생기는 이유는 **매일매일 겪게 되는 일상적인 오버헤드 때문이다.**
* 릴리스 버전 기술 지원, 병가, 회의, 시연, 개인 문제, 교육, 이메일, 코드 리뷰, 면접, Task Switching, 버그 수정
* 관리자들의 경우 방해 받지 않고 일할 수 있는 시간이 5분 정도에 불과하다는 연구도 있다. (Hobbs, 1987)

진짜 문제는 이런 상황에서 발생한다.

1. 관리자: "얼마나 걸릴까요?"
1. 개발자: "5일이요"
1. 관리자: 달력에 5일을 체크한다.
1. 개발자(진의도): "개발만 하면 5일만이면 하겠죠.. 근데 다른 일도 많아서 2주는 걸릴 것 같아요"

소프트웨어 개발 프로젝트에서는 여러 가지 일을 동시에 할수록 이상적 시간과 실제 경과 시간 사이의 차이는 더 커진다. 이런 점에서 이상적 작업일을 사용하려면 다음과 같은 가정을 전제해야 한다.

* 개발자는 추정 대상 스토리 이외의 다른 작업에는 관여하지 않는다.
* 개발자가 원하는 모든 것은 필요로 하는 그 즉시 구할 수 있다.
* **아무도 개발자를 방해하지 않는다.**

# 이상적 작업일을 이용한 규모 추정

* 이전에 규모 추정을 하는 방법으로 스토리 포인트를 소개했었다.
* 이상적 작업일을 기반으로 규모를 추정할 수도 있다.
* 이상적 작업일이 이 전 절에서 말한 가정들이 적용된 상태에서 만들어졌다면 규모 추정의 용도로 사용할 수 있다.
* 마찬가지로 하나의 기본 단위가 이상적 작업일이 되고, 팀의 속도가 도출되며, 결과적으로 기간 추정치를 얻을 수 있다.

# 추정치는 하나만

* 이상적 작업일을 기반으로 추정하기로 했다고 해보자.
* 그렇다면, 사용자 스토리 하나 당 하나의 추정치를 만들어라.
  * A 스토리: 9일
* 즉, 업무 구분에 따라 세부적으로 추정치를 만들어서 관리하지 말라는 뜻이다.
  * 프로그래머는 4일, 테스터는 2일, 관리자는 3일
* 이렇게 개인별 추정치를 만들게 되면 **애자일 팀에 요구되는 "하나의 팀" 정신이 손상된다.**
* 그리고 릴리즈 계획을 세우기도 어려워진다. 각각에 맞는 추정치를 만들어야 되기 때문에 복잡성이 증대된다. 
* 이를 기반으로 만들어지는 기간 계획도 추정이 어려워진다.

# 요약

* 이상적 시간과 실제 경과 기간은 다르다.
* 실제 경과 기간을 추정하기 위해서는 많은 불확실성들을 고려해야 한다. 그렇기 때문에 추정이 어렵다.
* 이런 경우, 이상적 시간을 통해 추정하는 것이 보다 간편하다.
* 이상적 작업일을 기반으로 규모 추정도 할 수 있다.
* 다만, 이 경우에는 각각의 스토리에 대해 개인별 추정치를 사용하는 것보다 하나의 추정치를 사용하는 것이 바람직하다.

# 토론 거리

* 이상적 작업일 "하루"를 "아무런 방해도 받지 않고 집중한 상태에서 작업에 몰두하는 8시간"이라 정의한다면, 실제 작업 환경에서 이 "하루"는 실제 경과 시간으로 환산했을 때 몇시간 정도가 되리라 보는가?
* Task Switching이 빈번하게 발생하는 상황을 개선하기 위해 어떤 조치를 할 수 있을까?

# Reference

* [불확실성과 화해하는 프로젝트 추정과 계획](http://www.yes24.com/Product/Goods/3067853)
* [Agile Estimating and Planning](https://www.amazon.com/Agile-Estimating-Planning-Mike-Cohn/dp/0131479415)