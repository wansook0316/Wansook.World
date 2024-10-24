---
title: Algorithm Tips
thumbnail: ''
draft: false
tags:
- python
- algorithm
- strip
- lower-bound
- upper-bound
- combination
- permutation
- deep-copy
- queue
- priority-queue
- sort
- collection
- BFS
- Set
- Regex
created: 2023-10-04
---

# 문자열 처리는 파이썬으로

1. find()
1. isalpha()
1. isalnum()
1. for ~ in list, string으로 하나씩 꺼낼 수 있다.
1. ~ in list, string으로만 하면 t/f 반환한다.
1. string slicing할 때, 맨 앞의 substring은 `s[:1]`과 같이 표기하고 뒤에서 부터 끊을 때는 `s[-1:]` 과 같이 표기한다.
1. 빈 Sequence(String / Tuple / List)는 False 값을 가진다. if not x: ~ = 없다면~

## strip

````python
strip() # 인자를 전달하지 않았기 때문에 양쪽 공백만 제거
strip("{") # 해당 문자와 같은 것 모두 양쪽에서 제거
lstrip("{") # 왼쪽에서만 strip 수행
````

## 정규 표현식 re

````python
import re

s = 'apple orange:banana,tomato'

l = re.split(r'[ ,:]', s)
print(l)

'''
['apple', 'orange', 'banana', 'tomato']

'''

````

### 숫자가 아닌 연산자에 대해 나누기

````python
re.split(r'(\D)',expression)
````

# 2차원 리스트

````python
array = [[0 for col in range(11)] for row in range(10)]

array = [[0]*11 for i in range(10)]

array = [[0]*11 ]*10
````

단, 아래의 두 방법을 알고리즘 문제 해결 이외에 어떠한 객체를 넣을 경우라면 얕은 복사 때문에 값이 한꺼번에 변하니 주의할 것

# 리스트 method

1. pop()
   1. pop할 때 empty list가 걱정되면 요소를 하나 넣어둔다 기본으로 `[0]`
1. append()
1. 맨뒤 li\[-1\]

# 순열

````python
from itertools import permutations
a = [1,2,3]
permute = permutations(a,2)
print(list(permute))
'''
결과
'''
[(1,2),(1,3),(2,1),(2,3),(3,1),(3,2)]
````

# 조합

````python
from itertools import combinations
a = [1,2,3]
combi = combinations(a,2)
    
print(list(combi))
'''
결과
'''
[(1,2),(1,3),(2,3)]
````

# Product

데카르트 곱이라고도 하는 cartesian product를 표현할 때 사용하는 메소드이다(DB의 join, 관계 대수의 product를 생각하면 된다). 이 메소드의 특징은 두 개 이상의 리스트의 모든 조합을 구할 때 사용된다.

````python
from itertools import product

_list = ["012", "abc", "!@#"]
pd = list(product(*_list))
# [('0', 'a', '!'), ('0', 'a', '@'), ('0', 'b', '!'), ('0', 'b', '@'), ('1', 'a', '!'), ('1', 'a', '@'), ('1', 'b', '!'), ('1', 'b', '@')]
````

````python
from itertools import product

l = [(x, -x) for x in [1,2,3, 4, 5]]
list(product(*l))

````

````
[(1, 2, 3, 4, 5),
 (1, 2, 3, 4, -5),
 (1, 2, 3, -4, 5),
 (1, 2, 3, -4, -5),
 (1, 2, -3, 4, 5),
 (1, 2, -3, 4, -5),
 (1, 2, -3, -4, 5),
 (1, 2, -3, -4, -5),
 (1, -2, 3, 4, 5),
 (1, -2, 3, 4, -5),
 (1, -2, 3, -4, 5),
 (1, -2, 3, -4, -5),
 (1, -2, -3, 4, 5),
 (1, -2, -3, 4, -5),
 (1, -2, -3, -4, 5),
 (1, -2, -3, -4, -5),
 (-1, 2, 3, 4, 5),
 (-1, 2, 3, 4, -5),
 (-1, 2, 3, -4, 5),
 (-1, 2, 3, -4, -5),
 (-1, 2, -3, 4, 5),
 (-1, 2, -3, 4, -5),
 (-1, 2, -3, -4, 5),
 (-1, 2, -3, -4, -5),
 (-1, -2, 3, 4, 5),
 (-1, -2, 3, 4, -5),
 (-1, -2, 3, -4, 5),
 (-1, -2, 3, -4, -5),
 (-1, -2, -3, 4, 5),
 (-1, -2, -3, 4, -5),
 (-1, -2, -3, -4, 5),
 (-1, -2, -3, -4, -5)]
````

# while 문 사용법

````python
while y in li:
    li.index(y)
````

이런식으로 사용하게 되면 index를 사용했을 때 발생하는 에러를 넘어가는 것이 가능함

# Deepcopy 방법

````python
b = a[:]
b = copy.deepcopy(a)
````

# Queue

* 리스트로 사용하기

````python
a = [3, 4, 5]
a.pop(0)
a.insert(0, 5)

[5, 4, 5]
````

하지만 시간 복잡도 측면에서 O(n)이므로 정말 필요한 경우는 다음을 사용하자.

* deque

````python
from collections import deque

q = deque([3, 4, 5])
q.append(0) # 오른쪽 삽입
q.appendleft(7) # 왼쪽 삽입
q.pop() # 오른쪽 빼기
q.popleft() # 왼쪽 빼기
````

삽입과 빼는 것에 있어서 O(1) 하지만, 임의 원소접근에 있어서 O(n)

# 내림, 올림, 반올림

````python
import math
math.ceil()
math.floor()
round()
````

# 재귀에서 다음으로 정보 보내는 방법

재귀에서 다음으로 정보를 보낼때 특정 위치 자체를 보내는 것이 어려울 수 있다. 여러개의 인자를 함께 넘겨야 하기 때문. 이럴 경우 마스킹 기법을 쓰면 좋다. 맞는지 모르겠지만 3은 이진수로 11이다. 이 의미자체가 어떤 위치를 의미하는 것. 또다른 사용방법으로는 3x3 매트릭스가 있을 때, 이 정보를 재귀를 타면서 넘어가기 위해서는 i, j 위치를 넘겨줘야 한다. 이럴 경우 4라는 숫자를 넘기고 4/3 = 1, 1 이런식으로 몫과 나머지를 사용하여 위치를 파악할 수 있다.

# Reduce

````python
from functools import reduce
reduce(lambda x, y: x+y, [1, 2, 3, 4, 5])
# = ((((1+2)+3)+4)+5)

````

# 우선 순위 큐

````python
from queue import PriorityQueue

que = PriorityQueue()
que = PriorityQueue(maxsize=8) # 크기 정하기

que.put(4)
que.put(1)
que.put(7)
que.put(3)

print(que.get())  # 1
print(que.get())  # 3
print(que.get())  # 4
print(que.get())  # 7

````

만약 구조체 형태로 무언가를 하고 싶다면 다음과 같이 하면 된다.

````python
que.put((3, 'Apple'))
que.put((1, 'Banana'))
que.put((2, 'Cherry'))

print(que.get()[1])  # Banana
print(que.get()[1])  # Cherry
print(que.get()[1])  # Apple
````

앞에 숫자가 오는 형태로 한 뒤에 값을 읽어오자.

이게 속도가 느려서 이걸 쓰는 것이 낫다.

````python
import heapqh

heap = []
heapq.heappush(heap, 50)
heapq.heappush(heap, 10)
heapq.heappush(heap, 20)

print(heap)
[10, 50, 20]
````

이미 생성한 리스트가 있다면 다음과 같이 사용할 수 있다.

````python
heap2 = [50 ,10, 20]
heapq.heapify(heap2)

print(heap2)
````

자료를 삭제하기 위해서 다음과 같은 방법을 사용한다.

````python
result = heapq.heappop(heap)

print(result)
print(heap)
````

최대 힙을 만들기 위해서는 트릭이 필요한데, 위에서 적은 것과 같이 튜플을 사용하여 만든다.

````python
heap_items = [1,3,5,7,9]

max_heap = []
for item in heap_items:
  heapq.heappush(max_heap, (-item, item))

print(max_heap)
````

# 정렬

* 원소의 길이 대로 정렬

````python
m = '나는 파이썬을 잘하고 싶다'
m = m.split()
m
['나는', '파이썬을', '잘하고', '싶다']
m.sort(key=len)
m
['나는', '싶다', '잘하고', '파이썬을']
````

## Dictionary Sort

딕셔너리를 정렬하고 싶은 경우 약간의 트릭이 필요하다. 이를 튜플 형태로 변환한 뒤, sort를 진행하는 것이다.

````python
score_dict = {
    'sam':23,
    'john':30,
    'mathew':29,
    'riti':27,
    'aadi':31,
    'sachin':28
}

new_dict = sorted(score_dict.items(), key=lambda x:x[1], reverse=True)
print(new_dict)
# [('aadi', 31), ('john', 30), ('mathew', 29), ('sachin', 28), ('riti', 27), ('sam', 23)]
````

아웃풋이 튜플 형태의 리스트로 나오게 된다. 만약 다시 dictionary로 만들고 싶다면(사실 그럴일은 없다) 다시 dict 자료형 안에 넣어주면 된다.

# collection

````python
import collections
import itertools

def solution(orders, course):
    result = []

    for course_size in course:
        order_combinations = []
        for order in orders:
            order_combinations += itertools.combinations(sorted(order), course_size)

        most_ordered = collections.Counter(order_combinations).most_common()
        result += [ k for k, v in most_ordered if v > 1 and v == most_ordered[0][1] ]

    return [ ''.join(v) for v in sorted(result) ]
````

이 문제에서 Counter를 사용하면 리스트 안에 있는 원소의 개수를 튜플 형태로 변환해준다.

# BFS

````python
from collections import deque
def solution(maps):
    answer = 0
    
    d = [[0, 1], [-1, 0], [0, -1], [1, 0]]
    n, m = len(maps), len(maps[0])
    visited = [[-1 for col in range(m)] for row in range(n)]
    
    q = deque()
    q.append([0, 0])
    visited[0][0] = 1
    while q:
        [y, x] = q.popleft()
        for i in range(4):
            ny, nx = y + d[i][0], x + d[i][1]
            if 0 <= ny < n and 0 <= nx < m:
                if maps[ny][nx] == 1 and visited[ny][nx] == -1:
                    visited[ny][nx] = visited[y][x] + 1
                    q.append([ny, nx])
    
    return visited[-1][-1]
````

# lower bound, upper bound

````python
from bisect import bisect_left, bisect_right 
nums = [0,1,2,3,4,5,6,7,8,9] 
n = 5 
print(bisect_left(nums, n)) 
print(bisect_right(nums, n)) 

결과값 
5 -> 원하는 값이상의 값의 처음 등장위치 
6 -> 원하는 값보다 큰 값의 index
````

````python
from bisect import bisect_left, bisect_right 
nums = [4, 5, 5, 5, 5, 5, 5, 5, 5, 6] 
n = 5 
print(bisect_left(nums, n)) 
print(bisect_right(nums, n)) 

결과값 
1 9
````

# 백준 입력 받기

````python
from sys import stdin

M = int(stdin.readline())
m = sorted(map(int, stdin.readline().split()))
N = int(stdin.readline())
n = list(map(int, stdin.readline().split()))
````

colab에서는 안된다.

# any

````python
a = [True,False,True] 
any(a) True
````

# Set

````python
A = set()

A.update([1, 2, 3])
A.add(4)
A.remove(4)
````

# 자료형의 참 거짓

|값|참 or 거짓|
|:--|:-----:------|
|"python"|참|
|""|거짓|
|\[1, 2, 3\]|참|
|\[\]|거짓|
|()|거짓|
|{}|거짓|
|1|참|
|0|거짓|
|None|거짓|
