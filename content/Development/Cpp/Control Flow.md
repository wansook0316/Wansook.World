---
title: Control Flow
thumbnail: ''
draft: false
tags:
- cpp
- control-flow
- while
- break
- continue
- do-while
- for
- switch
created: 2023-10-03
---

기존에 작업한 글이 있어 링크로 대체한다.

* [Control Flow](Development/C/Control%20Flow.md)
* [Loop Part. 01](Loop%20Part.%2001.md)
* [Loop Part. 02](Loop%20Part.%2002.md)

## iomanip library

기본적으로 iostream 라이브러리로 출력을 하게되면, 왼쪽 정렬이다. 그리고 내가 원하는 칸에 정렬하기가 힘든데, 이 라이브러리를 불러오고,

````c++
sd::cout << std::setw(10) << endl;
````

이런식으로 쳐주면, 10개의 칸중 오른쪽에 정렬되어 출력된다.

````c++
//         1
//        10
//       100
````

## locale library

1000단위로 끊어준다!

````c++
std::cout.imbue(std::locale(""));
````

## while

* 보통 무한 루프 돌릴 때 많이 쓴다.
* 왠만한 건 다 for 루프

## break

* while 탈출
* 유효성 검사후 탈출

## Continue

* 이 이후를 수행하지말고 처음으로 돌아가라
* 보통 loop 랑 함께 사용함.

## do-while

* 먼저 실행하고 조건문 판단
* 보통 입력을 먼저 받아야 하는 무한루프에서 사용하는 경향이 있음

## for

* 너무 많이 사용해서 생략

## Switch

* 조작에 관련된 것
* 프로그램 종료할 때 사용
* if 문보다 뭔가 명확한 것일 때 사용하면 좋음