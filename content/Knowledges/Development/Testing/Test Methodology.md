---
title: Test Methodology
thumbnail: ''
draft: false
tags:
- test
- testing
- FIRST
- Right-BICEP
- unit-test
- alpha-test
- beta-test
- QA
created: 2023-10-01
---

# 왜 필요할까?

![](151102538-edaf10ef-4c78-4bdb-b414-0331109b349d.png)

* V-Diagram
* 왜 단계적인 테스트가 필요할까?
* 문제가 발생했을 때, 시간, 의사소통 등의 비용을 줄이기 위함
* 요구사항 만족함을 증명하는 것

# 어떤 종류가 있을까?

## 단위 테스트

* 테스트가 가능한 최소 단위로 나누어진 모듈, 프로그램, 객체, 클래스 내에서 결함을 찾고 기능을 검증
* 독립적으로 수행됨
* 프로그래머가 주도함
* 코드를 중심으로 수행
* 이러한 구분은, 어떤 Task냐에 따라 구분이 달라진다.
* 가장 집중해야 하는 테스트

## 통합 테스트

* 모듈간 인터페이스 테스트
* 다른 모듈과 상호작용 테스트
* 기능적 특성: 제대로 된 기능을 수행하는가
* 비기능적 특성: 성능, 부하, 스트레스 등의 테스트

## 시스템 테스트

* 전체 시스템, 제품의 동작 테스트
* 실게 최종 사용 환경 또는 유사한 환경에서 수행
  * 환경 특정 장애 리스크를 최소화 하기 위해
* 기능, 비기능 요수 사항을 모두 검증
* 독립적인 테스트 팀이 주도 (QA팀)

## 인수 테스트

* 실제 사용할만한 준비가 되어 있는지 평가
  * 결함을 찾는 것이 주된 관심사가 아님
* 사용자가 전담하여 수행함
* 결함은 발견하는 것이 아니고 발견되는 것
* 알파/베타 테스트가 이에 속함
* 알파 테스트
  * 사내 이해 당사자에게
* 베타 테스트
  * 사외 사용자에게

# FIRST: 좋은 단위 테스트는 무엇인가?

## Fast

* 실행이 느린 단위 테스트
  * 외부 자원 접근 코드를 실행함
    * 외부 자원: 데이터베이스, 파일, 네트워크
  * 수십~수천 ms
* 실행이 빠른 단위 테스트
  * 프로덕션 코드만 실행
  * 수 ms
* 테스트 코드 개수에 따라 위 차이는 기하급수적으로 늘어남
* 실제 외부 자원 IO를 하는 코드와, 평가 코드를 분리해둔다면 mock 객체를 사용하여 테스트가 가능
* 만약 프로덕션 코드에 이러한 분리 작업이 이루어지지 않을 경우 분리하는 것이 좋은 습관임
* 외부자원 의존성을 줄이는 방법
  * Stub: 하드 코딩한 값을 반환하는 구현체
  * Mock: 가상 데이터 구조를 만듦

## Isolated/Independent

* 접근성, 가용성 이슈
  * 특정 테스트 코드가 Database에 접근
  * 그런데 데이터 베이스에 문제 발생
  * 테스트 케이스 실패
  * 이런 경우를 접근성(accessibility), 가용성(availibility) 이슈라 함
  * 이렇게 되면, 보통은 데이터 베이스 문제가 발생하지 않으므로 코드 문제라 판단하기 쉽고, 결국 문제 탐색에 시간이 소요되게 된다.
* 데이터 의존적인 경우
  * DB에 있는 값을 기반으로 테스트 코드를 짰기 때문에, 접근하는 실행 주체가 많을 경우 원하는 테스트를 수행할 수 없게 된다.
  * 고립되어 있지 않고, 값에 의존적인 상황이다.
* 순서 의존성 존재
  * TC C를 수행하기 위해서는 TC A, B가 선행되어야 한다.
  * 이럴 경우 실패시 단위 테스트 체인을 분석해야 함
  * 또, 앞선 TC가 통과하지 못하여 원하는 TC C를 수행하지 못한다.

## Repeatable

* 실행할 때마다 동일한 결과를 보장함
  * 통제할 수 없는 외부 요소는 동일한 결과를 보장하지 못할 수 있다.
  * 산발적으로 실패하는 테스트는 불필요한 비용을 발생시킴

## Self-Validating

* 스스로 검증 가능해야 한다.
  * 콘솔에 찍는 행위 X: 판단하러 로그를 보아야 함
  * Assert: 스스로 검증 가능
  * 효과
    * 실행 자동화
    * 지속적 통합
      * Jenkins, TeamCity

## Thorough/Timely

* 적절한?
  * 요구사항이 변경이 빈번한 개발 초기 단계
  * 오래 방치된 하지만 문제 없는 레거시 코드
  * 프로덕션 코드 구현 전후
  * develop 브랜치에 통합하기 전
  * 배포하기 전
* 이러한 상황에서 도입은 사실 고민이 필요하다.

# Right-BICEP

## Right

* 기대한 결과를 검증한다.
* 해피 시나리오 테스트
  * 코드가 정상적으로 동작한다면, 그것을 알 수 있을까?
  * 이를 작성할 수 있다는 것은 곧 요구사항, 시나리오, 프로덕션 코드를 충분히 이해한 상태라는 것을 말함

## Boundary condition

* 경계 조건을 테스트 한다.

* 경계조건의 예시

* 모호하고 일관성 없는 입력값

* 잘못된 양식의 데이터

* 수치적 오버플로우를 일으키는 연산

* 비거나 빠진 값

* 이성적인 기대 값을 훨씬 벗어나는 값
  
  * 나이 (150살?)
* 중복 허용이 안되는 목록에 중복 값이 존재

* 정렬이 안된 정렬 리스트, 혹은 정렬된 리스트

* 시간 순이 맞지 않는 경우
  
  ## CORRECT (경계조건)

* Conformance (양식 준수)

* Ordering (정렬 순서)

* Range (범위)

* Reference (참조)

* Existence (존재)

* Cardinality (기수)

* Time (순서)

## Inverse relationship

* 논리적인 역관계를 활용하여 테스트 한다.
* 수학적인 계산 로직 테스트에 종종 사용됨
  * 제곱근: 결과를 두번 곱해서 해당 값이 나오는지 테스트 한다.

## Cross-check result

* 다른 수단을 활용하여 교차 테스트 한다.
* 제곱근 함수가 있다면, 다른 제곱근 함수와 비교를 해서 결과를 확인한다.
* 재구성한 라이브러리
* 리팩토링 이전 vs 이후
* 총합 확인

## Error condition

* 오류 조건하에 오류가 발생하는지 테스트 한다.
* 언해피 시나리오
  * 환경적인 제약
    * 메모리가 가득 찰 때
    * 디스크 공간이 가득 찰 때
    * 벽시계 시간에 관한 문제들
    * 네트워크 가용성 및 오류들
    * 시스템 로드
    * 제한된 색상 팔레트
    * 매우 높거나 낮은 비디오 해상도

## Performance

* 성능 조건을 테스트 한다.
* 단위 테스트로 구간별 경과시간을 측정하여 진단
  * 병목 지점 추측이 어렵기 때문
* 성능 최적화 이전 코드 vs 최적화 이후 코드
  * old vs new
  * 각각의 함수 리턴 사이 호출 시간 비교

# Reference

* [guru99](https://www.guru99.com/sdlc-vs-stlc.html)