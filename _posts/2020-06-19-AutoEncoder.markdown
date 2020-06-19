---
layout: post
title:  "AutoEncoder"
date:   2020-06-19 21:10:00 +0900
categories: RL_UL
---

## AutoEncoder

- 자기 자신을 학습하는 Unspervised Learning

  - 입력과 출력층의 뉴런 수가 동일
  - encoder 부분만 분리하면 Clustering model이 됨
  - decoder 부분만 만들면 Generation model이 됨
  - AutoEncoding 과정에 de-noising 처리됨(인코딩 과정에서 입력된 데이터의 핵심 Feature 정보만 Hidden Layer에서 학습하고, 나머지 정보는 손실시킴. 디코딩 과정에서 Hidden Layer의 출력값을 뽑았을 때 완벽한 값 복사가 아닌 입력값의 근사치가 됨)

  ![AutoEncoder](/img/AutoEncoder.PNG)

- AutoEncoder 종류 : <https://iq.opengenus.org/types-of-autoencoder>

### Anomaly Detection

- 정상 데이터에 비해 비정상 데이터 수가 너무 적으면(1만배 이상 차이가 나면) 지도학습으로 학습이 잘 안됨
- 정상을 학습 -> 구현시 재구성 Error가 크면 비정상 이라고 간주함
    
### Denoising Autoencoder

- 오토인코더가 의미있는 특성(feature)을 학습하도록 제약을 주는 다른 방법은 입력에 노이즈(noise, 잡음)를 추가
- 노이즈가 없는 원본 입력을 재구성하도록 학습시키는 것
- 노이즈 발생 방법
  - 입력에 가우시안(Gaussian) 노이즈를 추가
  - 드롭아웃(dropout)처럼 랜덤하게 입력 유닛(노드)를 끔
  