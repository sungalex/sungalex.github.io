---
layout: post
title:  "[Study9] Keras - 파이썬 딥러닝 라이브러리(작성중...)"
date:   2020-06-22 21:00:00
categories: Python AI AI&QA
---

*(create: '20.6.22, update: '20.6.24)*

reference : [Keras Documentation(Korean)](https://keras.io/ko/), [Keras Documentation(English)](https://keras.io/documentation/)

## 1. Keras 소개

### 1-1. [30초 케라스](https://keras.io/ko/#30)

케라스의 주요 데이터 구조는 [`models`](https://keras.io/ko/models/about-keras-models/)로 레이어를 조직하는 방식입니다. 가장 간단한 종류의 모델인 [`Sequential`](https://keras.io/ko/models/sequential/) 모델은 레이어를 선형적으로 쌓습니다. 보다 복잡한 구조를 만드려면, [Keras functional API](https://keras.io/guides/functional_api/)를 사용하여 레이어로 임의의 그래프를 구축하면 됩니다.

- `Sequential` 모델을 생성합니다:

  ~~~ipython
  from keras.models import Sequential

  model = Sequential()
  ~~~

- `add()` 메소드를 통해 레이어를 간단하게 쌓을 수 있습니다. 또는, `Sequential` 모델 생성 시 생성할 레이어를 인자로 전달할 수도 있습니다 :

  ~~~ipython
  from keras.layers import Dense

  model.add(Dense(units=64, activation='relu', input_shape=(28,28)))
  model.add(Dense(units=10, activation='softmax'))
  ~~~

- 모델을 만든 다음 `compile()` 메소드로 학습 과정을 조정하십시오(옵티마이저, 손실함수, 측정지표 등) :

  ~~~ipython
  model.compile(loss='categorical_crossentropy',
              optimizer='sgd',
              metrics=['accuracy'])
  ~~~

- 배치의 형태로 트레이닝 데이터에 대한 반복작업을 수행할 수 있습니다:

  ~~~ipython
  # Training을 수행하기 전에 학습 데이터를 읽어들여야 합니다.
  import tensorflow as tf

  mnist = tf.keras.datasets.mnist
  (x_train, y_train), (x_test, y_test) = mnist.load_data()
  x_train, x_test = x_train / 255.0, x_test / 255.0

  # fit() 메소드로 학습 합니다.
  model.fit(x_train, y_train, epochs=5, batch_size=32)
  ~~~

- 코드 한 줄로 모델의 성능을 평가해 보십시오:

  ~~~ipython
  loss_and_metrics = model.evaluate(x_test, y_test, batch_size=128)
  ~~~

- 혹은 새로운 데이터에 대해서 예측 결과를 생성해 보십시오:

  ~~~ipython
  classes = model.predict(x_test, batch_size=128)
  ~~~

### 1-2. [Keras 설치](https://keras.io/ko/#_4)

- Tensorflow를 설치 합니다. (Keras 벡엔드로 Tensorflow를 사용 합니다. Tensorflow 2.x latest 버전을 설치 합니다.)

  ~~~bash
  $ pip install tensorflow
  ~~~

  또는, 아래와 같이 tensorflow 버전을 명시적으로 지정하여 설치할 수도 있습니다.

  ~~~bash
  $ pip install tensorflow==2.1
  ~~~

- Keras를 설치 합니다.

  ~~~bash
  $ pip install keras
  ~~~

- 선택적으로, HDF5 and h5py(디스크에 케라스 모델을 저장하실 경우 필요합니다) 라이브러리와 graphviz, pydot(모델 그래프를 시각화하는 visualization utilities에 사용됩니다) 라이브러리를 설치하는 것도 고려해 보십시오:

  ~~~bash
  pip install h5py
  pip install pydot
  ~~~

## 2. Keras 시작하기

### 2-1. [케라스 Sequential 모델 시작하기](https://keras.io/ko/getting-started/sequential-model-guide/)

### 2-2. [케라스 함수형 API 첫걸음](https://keras.io/ko/getting-started/functional-api-guide/)

## 3. Keras models

### 3-1. [Keras 모델에 관하여](https://keras.io/ko/models/about-keras-models/)

### 3-2. [Sequential 모델 API](https://keras.io/ko/models/sequential/)

### 3-3. [Keras 함수형 API](https://keras.io/guides/functional_api/)

## 4. Keras layers

### 4-1. [Keras 레이어에 관하여](https://keras.io/ko/layers/about-keras-layers/)

### 4-2. [직접 케라스 레이어 만들기](https://keras.io/ko/layers/writing-your-own-keras-layers/)

## 5. [Keras Visualization](https://keras.io/ko/visualization/)

### 5-1. 모델 시각화

### 5-2. 학습 히스토리 시각화
