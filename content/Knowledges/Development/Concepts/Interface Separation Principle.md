---
title: Interface Separation Principle
thumbnail: ''
draft: false
tags:
- oop
- SOLID
- interface-separation-principle
created: 2023-10-01
---

리팩토링 작업중, 고민했던 것들을 정리해본다. 누군가에게는 도움이 되겠지.

# 문제 상황

![](Thinking_01_InterfaceSeparationPrinciple_0.png)
일단 문제상황은 위와 같다. 같은 VC로 작성되어있음에도 불구하고, 실제 유저가 진입했을 때 보는 화면은 두가지이다. 하나는 없는 상품이기 때문에 "등록"이 필요하고, 하나는 이미 등록된 상품을 "수정"하는 화면이다.

두 화면은 상당히 유사하며, 약간의 로직 차이가 있다. 가장 대표적으로 이해하기 쉬운 것이 등록의 경우 추가만 가능하고, 수정의 경우 삭제, 수정이 가능하다. 이 버튼들은 단순히 hidden 처리와 같은 방식으로만 되어 있는 상태이다.

`상품 선택`의 경우 "수정", "등록" 화면 모두에서 사용하는 method이지만, 실제로 동작하는 로직은 다르다. `추가 하기`, `수정 하기`, `삭제 하기`의 경우 보여지는 mode(수정, 등록)에 따라 달리 사용되고 있다.

# 상황 판단

가장 이상적으로는, 두 화면이 비슷하지만 다른 동작을 하고 있기 때문에 두 개의 VC를 만들고 두 개의 ViewModel을 가지는 것이 보기 좋을 것이다. 이 때, View code를 component화 하여 재활용을 통해 생산성을 높히는 방향이 가장 깔끔할 것이다.

하지만, 이러한 점을 앎에도 불구하고 지금 상황에서는 VC 코드를 만지지 않을 생각이다. 일단 Component화 되지도 않았고, Storyboard로 짜져있기 때문에, 당장 이 부분을 건들이는 건 리팩토링 시 큰일이라 생각했기 때문이다.

그보다는 일단 business logic 부터 분리를 하고, 추후에 View는 바뀔 가능성이 높으니, 그 때 변경하는 것이 보다 효율적이라 판단했다. 이러한 가정에서 출발한 해당 작업의 제약 사항은 다음과 같다.

## 제약 조건

**"등록"과 "수정"에 있어 ViewModel을 분리한다.** "등록"과 "수정"은 명백히 다른 동작을 하고 있다. 분리하는 것이 추후 개발자가 해당 화면을 진입할 때 편하게 할 수 있을 것이다. 실제로 두 로직이 혼재되어 있어 해당 화면의 코드를 읽는 것이 상당히 어려웠다. 근본적으로 두 화면의 진입 시점에서 분기가 되어야 함을 명시적으로 작성한다면, 이해가 쉬울 것이다. 따라서 해당 화면의 business logic을 분리한 ViewModel을 가지는 것이 맞다고 판단했다.

**두번째로, 당장 View를 건들이지 않는다.** View는 상대적으로 많이 변경되는 부분이다. 실제로 추후 스펙에서 변경됨이 확인되었다. Cost 측면에서 보다 우선이 아니라고 생각한다.

## 목표

이러한 제약 조건에서 달성하고 싶은 목표는 다음과 같다.

 > 
 > 최대한 재사용성, 코드의 가독성, 직관성을 유지하면서 중복을 최소화한 분리를 성공시킨다.

해당 화면에 대해 이제야 조금 이해가 되었지만 초반에는 어떤 전략을 해야할 지 몰라 배운다고 생각하고 내가 생각하는 모든 옵션을 적용해보았다. 다음은 그 과정이다.

# Naive한 Protocol 사용

![](Thinking_01_InterfaceSeparationPrinciple_1.png)

일단 가장 먼저 생각한 옵션은 Protocol이다. 이전에 OOP에 대한 강의를 들으면서, 상속은 최후의 수단이라고 정리한 적이 있다. [Object Oriented Programming](https://velog.io/@wansook0316/%EC%8A%A4%ED%8C%8C%EA%B2%8C%ED%8B%B0-%EC%BD%94%EB%93%9C%EC%9D%98-%EB%AC%B8%EC%A0%9C%EC%99%80-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95) 글에 적혀있다. Interface만 적용해서 해결이 가능하다면 그렇게 처리하고 싶었다. "등록" 및 "수정" 화면에서 `추가하기`, `수정하기` 버튼은 UI적으로 동일하게 되어 있었는데, 이러한 점에서 다음과 같은 생각을 했다.

 > 
 > 같은 버튼인데 다른 동작을 하네? 그럼 같은 interface를 만들고, 실제 구현만 EnrollViewModel, EditViewModel에서 다르게 하면 되겠다!

위는 그러한 생각을 기반으로 그려본 그림이다. 하지만 실제로는 "수정" 화면에는 `삭제 하기`도 있었고, 기존 생각을 적용할 경우 `추가 하기`, `수정 하기`, `삭제 하기` 세 개의 함수를 하나의 interface로 처리해야 한다는 문제가 있었다. 딱봐도 뭔가 이상하다.

일단 이게 맞다고 가정하더라도 **어떤 이름을 지어야 할지가 불분명했다.** 이미 여기서 이 방법에 모순이 있다는 것이다. 특정 함수가 **여러 동작을 한다는 것이 명백하게 드러나는 순간이다.** 그래도 일단 해봤다.

![](Thinking_01_InterfaceSeparationPrinciple_2.png)

`tempMethod`라고 임의로 칭한 상태에서 적용해보았다. 크게 3가지의 문제가 있었다.

1. Protocol은 기본 값을 가질 수 없다. 그렇기 때문에 두 구현체에서 일일해 Property를 만들어줬어야 했다. 접근 제어도 기본 구현과 달리 `internal`로만 적용이 가능했다.
1. 분명 중복되는 Method, `뒤로 가기`, `상세 보기`의 경우 같음에도 불구하고 두 구현체에서 같은 내용을 구현해주어야 했다. extension을 활용한 기본 구현을 활용할 수 있지만, 해당 구현이 몇 개의 상태값과 연관이 있었기 때문에 **기본 값을 가질 수 없는 Protocol에서 구현이 불가**했다.
1. 추가적으로 하나의 interface로 퉁치는 순간, "수정"화면에서는 분기가 필요했다.

이런 방식으로는 안되겠다는 생각을 하고 다음 방식을 시도하게 된다.

# 단순 Inherence

![](Thinking_01_InterfaceSeparationPrinciple_3.png)

하지말라던 상속을 한번 적용해보았다. 말만 하면 머리에 안남으니까. 일단 내가 원하는 방식은 ViewController에서 두 구현체를 모르더라도 같은 함수를 통해 동작을 처리하는 것이었다. (~~나중에 가보니 이 생각 자체가 잘못됐다는 것을 알았다~~) 

````swift
class ViewController: UIViewController {
    let viewModel: AncesterViewModel

    private productSelected() {
        self.viewModel.selectProduct()
    }

    private saveButtonTouched() {
        if self.viewModel is EnrollViewModel {
            self.viewModel.add()
        } else {
            self.viewModel.update()
        }
    }
}

class EnrollViewModel: AncesterViewModel {
    override func selectProduct() {
        // Enroll시 상품 선택했을 때 동작
    }

    override func add() {
        // 추가하자
    }
}

class EditlViewModel: AncesterViewModel {
    override func selectProduct() {
        // Edit시 상품 선택했을 때 동작
    }

    override func update() {

    }
}

// 사용하는 곳: 등록
let viewController = ViewController(viewModel: EnrollViewModel)

// 사용하는 곳: 수정
let viewController = ViewController(viewModel: EditViewModel)

````

이런 방식을 생각했다. 상품 선택의 경우 좋은 방법이었다. 두 구현체에서 사용하는 함수 자체는 같으나 실제 구현만 달라지니까. 그런데 `추가하기`, `수정하기`의 경우는 그렇지 못했다. 결국에는 넣어준 ViewModel이 어떤 녀석인지 파악하는 과정이 필요했다. 

# 분기를 없앨 수 있는가?

결과적으로 나는 분기를 없앨 수 있다고 판단했던 것이 오판이라는 결론에 이르렀다. 분기를 없앨 수 있기 위해서는 두 구현체에서 사용하는 interface자체가 동일해야 한다. 그래야 다형성을 통해 처리가 가능하다. 완전히 오판했다.

그렇다면 위와 같은 상황에서는 어떻게 처리해야 하는가? 그 분기는 현재 누가 가져가야 하는가?

일단 위와 같은 상황이라면 분기를 처리하는 곳은 한쪽으로 모는 것이 보다 맞다는 생각을 했다. 그리고 ViewModel을 분리하겠다는 의도 자체는 결국 이 분기 처리의 책임을 ViewController로 옮기겠다는 말이다. 그래서 VC가 이 분기를 처리하겠다고 약간의 방향을 조정했다.

# 좋은 코드의 조건

여기까지 시행착오를 겪으면서 어떤 코드가 좋은지에 대해 생각하게 되었다. 그러고 보니 이전에 공부했던 내용이었다. [OOP Implement Pattern](OOP%20Implement%20Pattern.md) 부근의 **구현에 있어 필요한 가치 3가지**를 읽어보자. 이를 기반으로 앞에서 나왔던 방식들을 살펴보고 문제를 짚어보려 한다.

## 기존의 경우

커뮤니케이션 관점에서 어느정도는 타협이 가능하다. 사실 지금의 경우 Method가 많지도 않고, 서로 소통하는데 크게 문제는 없다. 다만, 현재의 경우 같은 동작을 하더라도 enrollMode인지 그렇지 않은지에 대해 판단하여 처리하고 있기 때문에 불편할 수 있다.

어느 소스 파일 관점에서 보느냐에 따라 다를 것 같다. 단순함이 읽기 쉬움에 가깝다는 점에 근거해서 본다면 어느정도는 맞는 듯 하다. 

확장성의 관점에서는 좋지 않을 듯하다. 확장시 결국에는 동작이 중첩되는 친구에 계속해서 구현이 늘어가게 되는데, 그렇게 되면 어느 순간 소스코드를 이해하기 어려운 순간이 온다. 수정자가 본인이라 이해하는 거지 실제로 보면 뭔가 분리가 필요하다는 냄새가 난다.

## Naive Protocol 사용의 경우

이건 세 원칙에 근거해서 알아볼 필요도 없다. 이 방식은 아예 잘못 사용한 방식이다. 확장성이 있지도 않고 그냥 손이 움직여서 적용한 수준이다. 심지어 단순하지도 않다.

## 단순 Inherence의 경우

커뮤니케이션 측면과 단순함 측면에서 좋지 않다 생각한다. 일단 부모 class를 반복해서 살펴보아야 한다. 직관성이 떨어진다. 상속받은 구현체만 바라본다면 일시적으로 단순할 수 있지만, 실제로는 VC에서 조상 class의 method도 사용하기 때문에 읽기 쉽지 않다.

확장성에 부분에서는 가장 좋지 않다. **상속은 하나만 할 수 있다.** 이점이 정말 치명적이다. 그렇기 때문에 다른 구현체가 필요한데, 특정 부분이 다르다면 아예 구조자체를 틀어야 하는 경우도 나온다. [Object Oriented Programming](https://velog.io/@wansook0316/%EC%8A%A4%ED%8C%8C%EA%B2%8C%ED%8B%B0-%EC%BD%94%EB%93%9C%EC%9D%98-%EB%AC%B8%EC%A0%9C%EC%99%80-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95)을 다시한번 읽어보자.

# Interface Separation Principle

![](Thinking_01_InterfaceSeparationPrinciple_4.png)

그래서 마지막으로 나온 결론은 이거다. 잘 생각해보면 두 화면에서 사용하는 기능 자체가 **붙였다 떼었다**할 수 있다. 정확하게 특정 VC에서 사용하는 기능만 붙여서 제공하자. 그리고 VC에서 분기 처리를 하겠다고 했기 때문에, 특정 버튼이 눌렸을 때 Protocol Type Check를 통해 동작을 구분하자.

## 최선인가?

일단 커뮤니케이션 측면에서 "채택하고 구현"이라는 단순한 방식을 사용할 수 있다. 

단순함 측면에서는 사람마다 성향이 다를 듯하다. 오히려 protocol을 많이 만들어서 처리하기 때문에 처음의 하나의 ViewModel에 넣어두는 것보다 귀찮을 수 있다.

확장성 측면에서는 보다 좋다. 만약 read라는 (사실 없겠지만..) 녀석이 추가된다면 protocol추가하고 채택해서 구현하면 끝이다.

# 마무리

이 부분을 하면서 정말 어려웠다. 답이 없는 분야였기 때문이다. 그래도 다양한 분들과 함께 소통하면서 각자의 생각을 맞춰볼 수 있어 의미있었다. ISP를 잘 사용하는 것도 좋은 스낄이라는 생각이 들었다. 끝!