---
layout: post
title:  "[Study2] 머신러닝 Hello World!!! MNIST 문자 인식"
date:   2020-04-16 22:00:00 +0900
categories: AI&QA
---

## Wrap-up : 전통적인 프로그래밍 접근방식 vs. 머신러닝 접근방식

![프로그래밍 접근 방식](/img/study2/original_program_vs_ml.png)

- 데이터로 부터

## 사람의 뉴런으로부터 딥러닝까지

- 뉴런과 사람의 학습
- 퍼셉트론(Perceptron, Artificial Neural Network)
- 활성화 함수 : Sigmoid
- 딥러닝
- Back Propagation

## 딥너닝의 작동 원리

- 신경망은 가중치를 파라미터로 가진다. (초기 가중치는 랜덤하게 정한다. 초기 가중치를 지정하는 다양한 알고리즘이 있다.)
- 손실 함수로 신경망의 출력 품질을 측정한다. (예측값과 실제 타깃값을 비교하여 손실 점수를 계산한다.)
- 손실 점수를 피드백 신호로 사용하여 손실 점수를 조정한다. (손실 점수가 작아지는 방향으로 가중치를 조정한다.)

![딥러닝 작동 원리](/img/study2/deep-learning-principle.png)

## 머신러닝 구축 로드맵

- 전처리 : 특성 추출 및 스케일 조정, 특성 선택, 차원 축소, 샘플링
- 학습 : 모델 선택, 교차 검증, 성능 지표, 하이퍼파라미터 최적화
- 모델 평가
- 예측

## MNIST 문자 인식

- Tensorflow MNIST 초급
  - <https://tensorflowkorea.gitbooks.io/tensorflow-kr/content/g3doc/tutorials/mnist/beginners/>
  - <https://www.tensorflow.org/tutorials/quickstart/beginner>
- Tensorflow MNIST 고급
  - <https://tensorflowkorea.gitbooks.io/tensorflow-kr/content/g3doc/tutorials/mnist/pros/>
  - <https://www.tensorflow.org/tutorials/quickstart/advanced>
