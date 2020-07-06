---
layout: post
title:  "[Study9] Keras 소개 및 학습 레퍼런스"
date:   2020-06-22 21:00:00
categories: Python AI AI&QA
---

*(create: '20.6.22, update: '20.07.06)*

reference : [Keras Documentation(Korean)](https://keras.io/ko/), [케라스에 대하여](http://keras-ko.kr/about/), [Keras Documentation(English)](https://keras.io/documentation/)

## 1. Keras 소개

### 1.1. 케라스 맛보기

(reference: <https://keras.io/ko/#30>)

케라스의 주요 데이터 구조는 [`models`](https://keras.io/ko/models/about-keras-models/)로 레이어를 조직하는 방식입니다. 가장 간단한 종류의 모델인 [`Sequential`](https://keras.io/ko/models/sequential/) 모델은 레이어를 선형적으로 쌓습니다. 보다 복잡한 구조를 만드려면, [Keras functional API](https://keras.io/guides/functional_api/)를 사용하여 레이어로 임의의 그래프를 구축하면 됩니다.

- 필요한 모듈을 import 합니다. tensorflow를 keras backend로 사용하는 경우는, `import keras` 보다는 `from tensorflow import keras` 처럼 tensorflow API 형태로 import 하는 방식을 추천 합니다.([참고](https://github.com/keras-team/keras/releases/tag/2.3.0))

  ~~~ipython
  from tensorflow import keras
  ~~~

- keras `Sequential` 모델을 생성합니다:

  ~~~ipython
  model = keras.models.Sequential()
  ~~~

- `add()` 메소드를 통해 레이어를 간단하게 쌓을 수 있습니다. 또는, `Sequential` 모델 생성 시 생성할 레이어를 인자로 전달할 수도 있습니다 :

  ~~~ipython
  model.add(keras.layers.Flatten(input_shape=(28, 28)))
  model.add(keras.layers.Dense(64, activation='relu'))
  model.add(keras.layers.Dense(10, activation='softmax'))
  ~~~

- 모델을 만든 다음 `compile()` 메소드로 학습 과정을 조정하십시오(옵티마이저, 손실함수, 측정지표 등) :

  ~~~ipython
  model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
  ~~~

- 배치의 형태로 트레이닝 데이터에 대한 반복 학습을 수행할 수 있습니다. `fit()` 메소드로 학습 합니다:

  ~~~ipython
  model.fit(x_train, y_train, epochs=5, batch_size=32)
  ~~~

- `evaluate()` 메소드로 학습된 모델의 성능을 평가해 보십시오:

  ~~~ipython
  loss_and_metrics = model.evaluate(x_test, y_test, batch_size=32)
  ~~~

- `predict()` 메소드로 새로운 데이터에 대해서 예측 결과를 생성할 수 있습니다:

  ~~~ipython
  classes = model.predict(x_test, batch_size=32)
  ~~~

### 1.2. Keras 설치

(reference: <https://keras.io/ko/#_4>)

- Tensorflow를 설치 합니다. (Keras 벡엔드로 Tensorflow를 사용 합니다. Tensorflow 2.x latest 버전을 설치 합니다.)

  ~~~bash
  $ pip install tensorflow
  ~~~

  또는, 아래와 같이 tensorflow 버전을 명시적으로 지정하여 설치할 수도 있습니다. (`tensorflow==latest` 형태로 가장 최신 버전을 설치할수도 있습니다.)

  ~~~bash
  $ pip install tensorflow==2.1
  ~~~

- Keras를 설치 합니다. keras 버전을 2.3으로 지정해서 설치 합니다. keras 버전 2.4부터 더이상 멀티 백엔드를 지원하지 않습니다. keras 2.4 [Release Note](https://github.com/keras-team/keras/releases/tag/2.4.0)와 [박해선님의 텐서 플로우 블로그](https://tensorflow.blog/2020/06/18/케라스-2-4-0-버전이-릴리스되었습니다/)를 참고 하세요.

  ~~~bash
  $ pip install keras==2.3
  ~~~

  - 케라스는 텐서플로 2.0에 tensorflow.keras로 포함되어 있으므로 케라스를 사용하려면 텐서플로 2.0을 설치하면 됩니다. (multi backend를 사용할 필요가 없는 경우, 즉 tensorflow backend 만 사용할 경우 keras를 별도로 설치할 필요가 없습니다.)

- 선택적으로, HDF5 and h5py(디스크에 케라스 모델을 저장하실 경우 필요합니다) 라이브러리와 graphviz, pydot(모델 그래프를 시각화하는 visualization utilities에 사용됩니다) 라이브러리를 설치하는 것도 고려해 보십시오:

  ~~~bash
  pip install h5py
  pip install pydot
  ~~~

---

## 2. Keras 학습 레퍼런스

- [Keras 시작하기](https://sungalex.github.io/python/ai/ai&qa/2020/06/24/keras-getting-started.html)

  - [케라스 Sequential 모델 시작하기](https://sungalex.github.io/python/ai/ai&qa/2020/06/24/keras-getting-started.html#케라스-sequential-모델-시작하기)

  - [케라스 함수형 API 첫걸음](https://sungalex.github.io/python/ai/ai&qa/2020/06/24/keras-getting-started.html#케라스-함수형-api-첫걸음)

- [Keras models](https://sungalex.github.io/python/ai/2020/06/24/keras-models.html)

  - [Keras 모델에 관하여](https://sungalex.github.io/python/ai/2020/06/24/keras-models.html#keras-모델에-관하여)

  - [Sequential 모델 API](https://sungalex.github.io/python/ai/2020/06/24/keras-models.html#sequential-모델-api)

  - [Keras 함수형 API(Model 클래스 API)](https://sungalex.github.io/python/ai/2020/06/24/keras-models.html#keras-함수형-apimodel-클래스-api)

- [Keras layers](https://sungalex.github.io/python/ai/2020/06/24/keras-layers.html)

  - [Keras 레이어에 관하여](https://sungalex.github.io/python/ai/2020/06/24/keras-layers.html#1-keras-레이어에-관하여)

  - [직접 케라스 레이어 만들기](https://sungalex.github.io/python/ai/2020/06/24/keras-layers.html#2-직접-케라스-레이어-만들기)

- [Keras Visualization](https://sungalex.github.io/python/ai/2020/06/24/keras-visualization.html)

  - [모델 시각화](https://sungalex.github.io/python/ai/2020/06/24/keras-visualization.html#1-keras-모델-시각화)

  - [학습 히스토리 시각화](https://sungalex.github.io/python/ai/2020/06/24/keras-visualization.html#2-keras-학습-히스토리-시각화)
