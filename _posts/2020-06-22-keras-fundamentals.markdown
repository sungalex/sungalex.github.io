---
layout: post
title:  "[Study9] Keras - 파이썬 딥러닝 라이브러리(작성중...)"
date:   2020-06-22 21:00:00
categories: Python AI AI&QA
---

*(create: '20.6.22, update: '20.6.22)*

reference : [Keras Documentation(Korean)](https://keras.io/ko/), [Keras Documentation(English)](https://keras.io/documentation/)

## 1. Keras 소개

### 1-1. [30초 케라스](https://keras.io/ko/#30)

케라스의 주요 데이터 구조는 model로 레이어를 조직하는 방식입니다. 가장 간단한 종류의 모델인 `Sequential` 모델은 레이어를 선형적으로 쌓습니다. 보다 복잡한 구조를 만드려면, [Keras functional API](https://keras.io/guides/functional_api/)를 사용하여 레이어로 임의의 그래프를 구축하면 됩니다.

- `Sequential` 모델을 생성합니다:

  ~~~ipython
  from keras.models import Sequential

  model = Sequential()
  ~~~

- `.add()`를 통해 레이어를 간단하게 쌓을 수 있습니다 :

  ~~~ipython
  from keras.layers import Dense

  model.add(Dense(units=64, activation='relu', input_shaoe=(28,28)))
  model.add(Dense(units=10, activation='softmax'))
  ~~~

- 모델이 마음에 드신다면, .compile()로 학습 과정을 조정하십시오:

  ~~~ipython
  model.compile(loss='categorical_crossentropy',
              optimizer='sgd',
              metrics=['accuracy'])
  ~~~

- 필요한 경우 한 걸음 나아가 옵티마이저를 조정할 수 있습니다. 케라스의 주요 철학중 하나는 사용자가 필요한 작업에 대해서는 완전한 제어권을 가질 수 있도록 하되 간결성을 유지하는 것입니다 (제어권의 궁극적인 형태로는 소스코드의 간편한 확장성이 있습니다).

  ~~~ipython
  model.compile(loss=keras.losses.categorical_crossentropy,
              optimizer=keras.optimizers.SGD(lr=0.01, momentum=0.9, nesterov=True))
  ~~~

- 배치의 형태로 트레이닝 데이터에 대한 반복작업을 수행할 수 있습니다:

  ~~~ipython
  # x_train and y_train are Numpy arrays --just like in the Scikit-Learn API.
  # Training을 수행하기 전에 학습 데이터를 읽어들여야 합니다. (코드 생략)
  model.fit(x_train, y_train, epochs=5, batch_size=32)
  ~~~

- 혹은, 모델에 배치를 수동으로 전달할 수도 있습니다:

  ~~~ipython
  model.train_on_batch(x_batch, y_batch)    # 사전에 x_batch, y_batch를 생성해야함
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

- Keras를 설치 합니다.

  ~~~bash
  $ pip install keras
  ~~~

- 선택적으로, HDF5 and h5py(디스크에 케라스 모델을 저장하실 경우 필요합니다) 라이브러리와 graphviz와 pydot(모델 그래프를 시각화하는 visualization utilities에 사용됩니다) 라이브러리를 설치하는 것도 고려해 보십시오:

  ~~~bash
  pip install h5py
  pip install pydot
  ~~~

## 2. Keras 시작하기

### 2-1. [케라스 Sequential 모델 시작하기](https://keras.io/ko/getting-started/sequential-model-guide/)

### 2-2. [케라스 함수형 API 첫걸음](https://keras.io/ko/getting-started/functional-api-guide/)

## 3. Keras 모델

### 3-1. [Keras 모델에 관하여](https://keras.io/ko/models/about-keras-models/)

Keras가 제공하는 모델에는 [Sequential 모델](https://keras.io/ko/models/sequential/)과 [함수형 API와 함께 사용되는 Model 클래스](https://keras.io/models/model) 두 가지 종류가 있습니다.

이 모델들은 아래의 메소드들과 속성들을 공통적으로 가지고 있습니다.

- `model.layers`: 모델을 구성하는 층들이 저장된 1차원 리스트 입니다.
- `model.inputs`: 모델의 입력 텐서들이 저장된 1차원 리스트 입니다.
- `model.outputs`: 모델의 출력 텐서들이 저장된 1차원 리스트 입니다.
- `model.summary()`: 모델의 구조를 요약해 출력해 줍니다. `utils.print_summary(model)`로도 동일한 출력을 얻을 수 있습니다.
- `model.get_config()`: 모델의 설정이 저장된 딕셔너리를 반환합니다. 모든 모델은 다음과 같이 설정 내용으로부터 다시 인스턴스화 될 수 있습니다.

  ~~~ipython
  config = model.get_config()
  model = Model.from_config(config)
  # 또는, Sequential 모델의 경우:
  model = Sequential.from_config(config)
  ~~~

- `model.get_weights()`: 모델의 가중치 텐서들이 NumPy 배열로 저장된 1차원 리스트 입니다.
- `model.set_weights(weights)`: 모델의 가중치 값을 NumPy 배열의 리스트로부터 설정합니다. 리스트에 있는 배열들의 크기는 `get_wieghts()`로부터 반환된 것과 동일해야 합니다.
- `model.to_json()`: 모델의 구조를 JSON 문자열로 반환합니다. 이때, 모델의 가중치는 제외되고 오로지 구조만이 포함됩니다. 이 JSON 문자열로부터 다음과 같이 동일한 모델을 (다시 초기화된 가중치와 함께)다시 인스턴스화 할 수 있습니다.
- `model.to_yaml()`: 모델의 구조를 YAML 문자열로 반환합니다. 이때, 모델의 가중치는 제외되고 오로지 구조만이 포함됩니다. 이 YAML 문자열로부터 다음과 같이 동일한 모델을 (다시 초기화된 가중치와 함께)다시 인스턴스화 할 수 있습니다.
- `model.save_weights(filepath)`: 모델의 가중치를 HDF5 파일로 저장 합니다.
- `model.load_weights(filepath, by_name=False)`: 모델의 가중치를 (save_weights에 의해 생성된) HDF5 파일로부터 불러옵니다. 기본 설정인 by_name=False는 모델과 가중치 파일의 네트워크 구조가 동일하다 가정합니다. 만약 구조가 다르다면, by_name=True를 사용해 동일한 이름을 가진 층들에 대해서만 가중치를 불러올 수도 있습니다.

### 3-2. [Sequential 모델 API](https://keras.io/ko/models/sequential/)

### 3-3. [Keras 함수형 API](https://keras.io/guides/functional_api/)

## 4. Layers

### 4-1. [Keras 층에 관하여](https://keras.io/ko/layers/about-keras-layers/)

### 4-2. [직접 케라스 레이어 만들기](https://keras.io/ko/layers/writing-your-own-keras-layers/)

Keras 2.0의 레이어는 다음의 메소드를 포함하고 있습니다. (세 가지 메서드만 구현하면 됩니다:)

- build(input_shape): 이 메서드에서 가중치를 정의합니다. 끝에서는 반드시 super(\[Layer\], self).build()를 호출해 self.built = True로 지정해야 합니다.
- call(x): 레이어의 논리의 핵심이 되는 메서드입니다. 마스킹을 지원하는 레이어를 만들 것이 아니라면 call의 첫 번째 인수에 전달되는 인풋 텐서만 주의하면 됩니다.
- compute_output_shape(input_shape): 레이어가 인풋의 형태를 수정하는 경우, 형태 변형 논리를 지정해야 합니다. 이는 케라스가 자동 형태 추론을 할 수 있도록 합니다.

~~~ipython
from keras import backend as K
from keras.layers import Layer

class MyLayer(Layer):

  def __init__(self, output_dim, **kwargs):
    self.output_dim = output_dim
    super(MyLayer, self).__init__(**kwargs)

  def build(self, input_shape):
    # 이 레이어에 대해 학습가능한 가중치 변수를 만듭니다.
    self.kernel = self.add_weight(name='kernel', 
                                  shape=(input_shape[1], self.output_dim),
                                  initializer='uniform',
                                  trainable=True)
    super(MyLayer, self).build(input_shape)  # 끝에서 꼭 이 함수를 호출하십시오

  def call(self, x):
    return K.dot(x, self.kernel)

  def compute_output_shape(self, input_shape):
    return (input_shape[0], self.output_dim)
~~~

## 5. [Visualization](https://keras.io/ko/visualization/)

### 5-1. 모델 시각화

### 5-2. 학습 히스토리 시각화

## 6. Examples

### 6-1. [Image classification from scratch](https://keras.io/examples/vision/image_classification_from_scratch/)

### 6-2. [Text classification from scratch](https://keras.io/examples/nlp/text_classification_from_scratch/)
