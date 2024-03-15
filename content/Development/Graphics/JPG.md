---
title: JPG
thumbnail: ''
draft: false
tags:
- jpg
- image
- graphics
- compression
- raster
- encoding
created: 2023-10-01
---

# JPG(Joint Photographic Experts Group)

* 정의: 정지 화상을 위해서 만들어진 손실 압축 방법 표준
* 핵심: 전체적 구조 손실보다 디테일 손실에 둔감하다는 점을 통해 압축
* 원리: 이미지의 고주파 성분의 일부를 제거함. 주파수 도메인으로 변환을 위해 이산 코사인 변환을 사용
  * 이미지 색공간 변환
    * RGB → Y(밝기), Cb, Cr(색차 정보)
    * 사람이 색상 성분보다 밝기에 더 민감하게 반응한다는 점을 이용하여 압축하기 위함
  * 다운 샘플링
    * 추출 전략 - J: a: b (픽셀 너비: 첫번째 샘플 개수: 두번째 샘플 개수) 보통 4:2:0 → 1/8 압축
  * 이산코사인 변환(District Cosine Transform)
    * 이제 해당 이미지를 주파수 대역에서 보고, 고주파영역(디테일)을 압축하는 과정이 남았다.
    * 각 채널을 8x8 블락으로 분할한다.
    * Element를 \[-128, 127\] 범위로 변경한다.
    * 2D 이산 코사인 변환을 적용한다.
  * 양자화
    * 8x8 행렬에 대해 양자화를 적용한다.
      * 각 계수에 대해 양자화 행렬로 나눈후 반올림한다.
      * 양자화 행렬은 좌상에서 우하로 갈수록 값이 커지는 경향이 있다. 이는 저주파일수록 더 작은 값으로 나눠주는 것을 의미한다.
      * 해당 행렬로 나눌 경우, 큰 값으로 고주파성분들을 나누기 때문에 많은 AC 계수들이 0이되어 버린다. 즉, 양자화를 통해 고주파 성분들을 손실시켰을음 말한다.
  * 지그재그 스캐닝
    * 2차원의 양자화된 DCT 계수들을 1차원의 데이터로 변환한다.
    * 지그재그 순서로 나열할 경우 1x64 크기의 벡터에 담을 수 있다.
    * 해당 이유는 낮은 주파수부터 순차적으로 나열하기 위함이다.
  * 양자화된 행렬 부호화
    * DC 부호화
      * 이전 양자화 벡터와 현재 양자화 벡터의 DC 값의 차로 대체한다.
      * 이는 허프만 부호화이다. 각 블럭의 DC의 차를 저장하는 방식을 도입하므로써 작은 크기의 값을 얻어내고, 이를 복호화함으로써 적은 비트를 차지하도록 함
        * 문자의 비트수가 길면 느려짐. 이에 문자를 부호화하는 방법을 고안
        * 아스키 코드: 고정길이 부호화
        * [Huffman coding](Huffman%20coding.md) 
    * AC 부호화
      * 랭스 부호화 적용
        * 일렬로 나열된 경우 0이 상당히 많을 것이다. 이렇게 0 자체를 압축할 때 해당 방법을 사용한다.
        * 0이 아닌 원소가 나올 때 마다 (0의 개수, 원소 값)의 형태로 압축하는 방법이다.
    * 부호화를 마친후, 계수들을 모두 붙이면 최종적으로 0, 1의 반복으로 이미지를 나타낼 수 있다. 기존의 8x8 블럭의 요소가 8비트라면, 8^3만틈의 비트가 필요한데, 압축하면 약 100비트 내외로 표현이 가능하다.
* 장점: 압축 속도가 빠르다.  디테일한 이미지의 경우 주파수가 높기 때문에 변환시 이득을 얻는다.
* 단점: 손실되는 압축 방법이기 때문에 원본으로 되돌리는 것이 불가능하다. RGB 색상 공간 사용 때문에 투명도를 사용불가하다.