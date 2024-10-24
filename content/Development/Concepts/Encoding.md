---
title: Encoding
thumbnail: ''
draft: false
tags:
- encoding
- ASCII
- ANSI
- EUC-KR
- CP949
- Unicode
- UTF
- UTF-8
- UTF-16
- UTF-32
- URL-encoding
- percent-encoding
- base64
created: 2023-10-01
---

네트워크 공부를 하다보니, 인코딩이라는 것에 대해 제대로 이해할 필요가 있다고 생각했다. 왜 필요한지, 어떻게 사용하는지에 대해서 이해해보는 포스팅이다.

# ASCII

* [ASCII](https://ko.wikipedia.org/wiki/ASCII)
* American Standard Code for Information Interchange)
* 7 Bit로 하나의 문자 표현
  * 128개의 문자 표현 가능
* 영어를 위한 인코딩 방식
  * 한국어, 중국어, 일본어, 아랍와와 같은 다른 나라 언어 표현 불가

# ANSI

* [ANSI](https://ko.wikipedia.org/wiki/미국_국가표준_협회)
* American National Standard Institute
* 7비트의 한계를 보완하기 위해 8비트 사용
  * 256개의 문자표현 가능
* 0x00부터 0x7F까지는 ASCII와 동일
* 나머지 128개에 대해 다른 문자 표현
  * 하지만 128개는 모든 문자를 표현하기에 택도 없기 때문에, **코드 페이지** 라는 것을 만들어서 각각 다른 코드표를 사용하도록 함
  * 호환성이 상당히 떨어짐

# EUC-KR

* 한글 지원을 위해 유닉스 계열에서 등장한 완성형 인코딩 방식
  * 완성형: 완성된 각 문자 (각, 완, 탁)에 코드를 부여하는 방식
  * 조합형: 문자를 이루는 요소(초성, 중성, 종성)에 코드를 부여하는 방식
* 2byte(16bit)로 하나의 문자를 표현
* 0x0000부터 0x007F까지는 KS X 1003 체계 (ASCII와 동일, 역슬래시만 ₩로 변경)와 동일, 나머지는 KS X 1001 체계와 동일
  * 하지만 KS X 1001 체계가 한글 단어를 2350자만 사전 순 배열했기 때문에 모든 한글 단어 표현하기 역부족
  * 초성 자음(19) * 중성 모음 (21) * 종성 받침 자음 (27) + 추가 친구들 = 약 11000개 이상

# CP949

* [코드 페이지 949](https://ko.wikipedia.org/wiki/코드_페이지_949)
* a.k.a MS949
* MS에서 한글 지원을 위해 확장한 완성형 인코딩 방식
* EUC-KR이 많은 한글 단어를 표현하지 못하는 문제를 보완하기 위해 등장
* 2byte(16bit) 사용, 하지만 EUC-KR이 사용하지 않는 나머지 바이트열을 활용하여 대부분의 한글 단어 표현 가능
* 하지만 EUC-KR에서 정렬했던 2350개의 문자를 제외한 나머지 문자열의 경우 사전순 정렬하지 않았다.
* 949은 한국에 대응하는 코드 페이지 번호를 의미

# Unicode

* [Unicode](https://ko.wikipedia.org/wiki/유니코드)
* 전세계에서 사용하는 수많은 문자들 각각에 부여한 코드 집합(표)
* 즉, 전세계에 있는 모든 문자를 특정 표에 매핑하여, 이를 참고하여 인코딩을 할 수 있도록 한 것을 의미
* utf-8, utf-16, utf-32 등은 그러한 유니코드 기반의 문자들을 바이트열에 인코딩하는 방식을 의미한다.

# UTF-N

* 유니코드 기반의 문자들을 바이트열에 표현하는 인코딩 방식
  * UTF-8, UTF-16, UTF-32
* 변환 방식
  * 유니코드 표에서 인코딩하고자 하는 문자의 코드를 찾는다.
  * 해당 코드를 인코딩 규칙에 따라 변형하여 바이트열에 표현한다.
  * 이 때, 인코딩 규칙에 따라 여러 방식이 존재한다.

## UTF-8

* [UTF_8](https://ko.wikipedia.org/wiki/UTF-8)
* 가변 길이 인코딩 방식
  * 인코딩 하려는 문자 코드가 속한 범위에 따라 1byte~4byte로 인코딩 함
  * 저장 공간을 효율적으로 사용할 수 있다.
    * 자주 사용되는 문자는 짧은 바이트로 표현
    * 그렇지 않은 경우 긴바이트로 표현
    * 128개 문자(0x0000~0x007F)는 인코딩 없이 1byte에 넣을 수 있다.
      * 즉, 영어만 사용할 경우 문자하나당 1byte만 사용
    * 중동, 유럽 지역 언어 사용시 문자하나 당 2byte 사용
    * 동아시아권 언어 3byte
* 방식의 경우, Wiki 참조

## UTF-16

* [UTF-16](https://ko.wikipedia.org/wiki/UTF-16)
* 16비트 기반의 가변거리 인코딩 방식
* 한글을 2byte로 인코딩할 수 있기 때문에 저장 공간 절약 가능
* 하지만 ANSI와 호환 불가, Byte Ordering 고려 문제 때문에 사용의 복잡성이 높음

## UTF-32

* [UTF-32](https://ko.wikipedia.org/wiki/UTF-32)
* 모든 문자를 4byte 고정 길이 인코딩
* 일관성있고 단순한 방식
* 하지만 하나의 문자를 저장하는데 있어 공간을 너무 많이 차지함

# Url Encoding(Percent Encoding)

* [Percent Encoding](https://ko.wikipedia.org/wiki/%ED%8D%BC%EC%84%BC%ED%8A%B8_%EC%9D%B8%EC%BD%94%EB%94%A9)
* URL에서 URL로 사용할 수 없는 문자, URL로 사용은 가능하나 의미가 왜곡될 수 있는 문자들을 `%XX`의 형태로 변환하는 것
  * `XX`는 16진수 값
* 비예약 문자
  * `alphanumeric` + `-_.?~`
* 예약 문자
  * `!*'();:@&=+$,/?#[]`
* 예시
  * Original : `https://velog.io/@wansook0316/?keyword=인코딩&디코딩`
  * Transformed : `https%3a%2f%2fvelog.io%2f%40wansook0316%2f%3fkeyword%3d%ec%9d%b8%ec%bd%94%eb%94%a9%26%eb%94%94%ec%bd%94%eb%94%a9`
* 사용 이유
  * 인터넷을 통해 전송할 수 있는 문자는 오로지 ASCII 문자이다.
    * 따라서 한글 같은 경우 변환이 필요하다.
    * 이 때, 문자열을 바이트열로 변환해준다. 이 때, UTF-8을 사용한다.
    * UTF-8에서 한 문자는 3바이트로 변환된다.
      * `인코딩 = %ec%9d%b8%ec%bd%94%eb%94%a9` 으로 총 9바이트로 인코딩되었다.
      * `ec9db8` 각각을 octet으로 표현 (4bit * 6 = 24bit)
  * 이스케이프 처리가 필요하기 때문
    * ASCII 문자라고 할지라도 URL에서 특정한 의미로 사용되는 단어들이 있을 수 있다.
    * 예를 들어 `/`, `&`, `"="` 등이 있다.
      * `/`
        * url의 레벨 분리
      * `&`
        * 쿼리 파라미터 구분
      * `"="`
        * 쿼리 파라미터 값 지정
    * 위의 예시에도 `%3d, %26`과 같이 변환되어 들어갔다.
    * 이러한 문자의 경우, 문자 그 자체의 의미로 사용하기 위해서는 변환과정을 통해 이를 구분할 수 있도록 해야 한다.
* 공백같은 경우 URL에서 허용되지 않는다. (`%20` 또는 `+`로 인코딩된다.)

# Base64

* [Base64](https://ko.wikipedia.org/wiki/베이스64)
* Byte열 (1010...)을 문자열로 바꾸는 방법
* 이 때, 바이트열을 6비트 단위로 쪼갠 후, 해당 6비트에 해당되는 ASCII 문자로 변환한다.
  * 그렇기 때문에 (6비트), 128개의 문자중 (아스키 코드는 7비트 내로 표현됨) 출력가능한 문자 95개 중에 (제어 문자) 64개만을 사용한다.
  * 6비트 사용 -> 표현 가능한 문자의 개수 64개 -> 숫자로 변환했을 때 64개의 수에 대응되는 코드들 -> 64진법 -> Base64 라는 이름이 붙게 되었다.
  * A-Z, a-z, 0-9로 처음의 62개가 보통 구성되며, 나머지 2개의 문자를 어떤 것을 사용하냐에 따라 종류가 구분된다.
    * 사실 64개의 문자를 어떤 것을 사용할 지는 임의로 정하면 되기 때문
* 길이 증가
  * 임의의 3개의 문자가 있다고 하자. (Man)
  * 각각의 문자는 1byte로 표현되기 때문에 총 24Bit를 차지한다.
  * Base64는 이 바이트 열을 6개씩 쪼개게 되고, 각각의 6비트에 해당하는 문자로 이를 치환한다.
  * 이 경우, 24/6 = 4로, 4개의 문자로 변환된다. (TWFu)
  * Man -> TWFu로 길이가 늘어났다.
  * 1바이트로 표현되는 문자를 6비트로 표현했기 때문에 길이 증가는 필연적이다. 
  * 그럼에도 불구하고 왜 사용할까?
* 사용 이유
  * System 독립적인 방법으로 데이터를 전달할 수 있다.
    * ASCII는 모든 시스템이 공통으로 알고 있는 방법이다.
    * 그렇기 때문에, 이러한 방식으로 문자열을 바꾼뒤 데이터를 전송할 경우 통신 과정에서 데이터가 잘못 해석되는 등의 문제가 발생하지 않는다.
    * 혹은, 이미지와 같은 바이너리 데이터를 포함해야 하는 경우, 시스템과 무관한 방식으로 동일하게 표현되도록 변환이 가능하다.
* 인코딩 과정
  * 8비트 단위로 되어 있는 바이트열을 6비트로 쪼갠 후, 24비트 버퍼에 차곡차곡 채워 넣는다.
    * 6비트인 이유는 위에도 말했듯, 64개의 문자만을 활용하기 때문이다.
    * 24비트인 이유는 8(변환 전 문자 크기)과 6(변환할 비트 크기) 의 최소 공배수이기 때문이다.
  * 만약 마지막 덩어리가 6비트보다 작다면, 나머지 부분은 0(Padding Bit)로 채워서 24비트 버퍼에 집어 넣는다.
  * 모두 넣었을 때, 24비트가 다 채워지지 않았다면 남은 6비트 공간의 개수만큼 `"="`을 추가한다.
