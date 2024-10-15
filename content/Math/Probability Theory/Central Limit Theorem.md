---
title: Central Limit Theorem
thumbnail: ''
draft: false
tags:
- statistics
- central-limit-theorem
created: 2024-09-12
---


 > 
 > 어떠한 모집단이더라도, 모집단의 평균이 $\mu$ 이고, 분산이 $\sigma^2$ 일 때, 임의추출된 표본의 표본 평균 $\bar X$ 는 표본의 크기가 클 경우 정규분포를 따른다.

$$
Z = {\bar X - \mu\over {\sigma / \sqrt{n}}}
$$

매우 중요한 중심극한 정리이다. 중심극한 정리의 핵심은, 표본을 뽑은 통계량으로 우리는 모집단의 모수를 추론할 것인데, 어떠한 분포에서 표본을 뽑던 간에 무조건 표본 평균이라는 통계량이 따르는 분포가 정해졌다는 것이다. 이러한 점에서 우리는 통계량의 분포를 가지고 모평균을 추론할 수 있게 된다.

이 중심극한 정리의 증명은 적률 생성 함수를 가지고 할 수 있다. 자세한 점은 수리 통계학 책을 공부하기 바란다.