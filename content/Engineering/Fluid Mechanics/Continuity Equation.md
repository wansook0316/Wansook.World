---
title: Continuity Equation
thumbnail: ''
draft: false
tags: null
created: 2023-10-04
---

# Continuity Equation

연속 방정식은 질량보존법칙을 오일러 표현으로 나타내 었을 때 어떤 모양이 되는지를 설명해주는 식이다. 라그랑지언 표현을 오일러 표현으로 바꾸어주는 RTT를 사용해 미소 면적을 표현해보자. 미소면적의 중앙에서 모든 Property의 값을 갖는다고 가정했을 때, 상하좌우에서 Property의 값은 테일러 급수를 통해 값을 근사해서 나타낼 수 있다. (1계 미분까지만 표현한 것은 2계미분 항부터는 너무 크기가 작아 무시할 수 있기 때문에)

![](Pasted%20image%2020231004121000.png)
![](Pasted%20image%2020231004121011.png)

이렇게 나온 식을 연속 방정식이라 부른다. 그런데 여기서 이 항을 조금더 풀게 되면 물질도함수의 모양으로 정리가 가능하다.다시 연속방정식을 이 모양으로 해석하게 되면, 특정 점에서 밀도의 시간에 따른 변화는 경계면에서의 속도의 발산(다이버전스)값에 밀도를 곱해준 것과 같다.로 해석할 수 있다. 여기서 만약 시간에 따라 밀도가 일정하다면, 즉, 특정점에서 밀도 변화가 없다면, (밀도 = 상수, 비압축성 유체)속도의 발산 값이 0, 즉 경계면에서 나가고 들어오는 양의 총합이 0, 우리가 생각하는 결과와 일치한다.

![](Pasted%20image%2020231004121027.png)
![](Pasted%20image%2020231004121038.png)