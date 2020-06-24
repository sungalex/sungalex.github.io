---
layout: post
title:  "Keras 레이어(keras.layers)"
date:   2020-06-24 21:00:00
categories: Python AI
---

*(create: '20.6.22, update: '20.6.22)*

- [1. Keras 레이어에 관하여](#1-keras-레이어에-관하여)
- [2. 직접 케라스 레이어 만들기](#2-직접-케라스-레이어-만들기)

---

## 1. Keras 레이어에 관하여

(reference: <https://keras.io/ko/layers/about-keras-layers/>)

Keras의 모든 층들은 아래의 메소드들을 공통적으로 가지고 있습니다.

- `layer.get_weights()`: NumPy형 배열의 리스트 형태로 해당 층의 가중치들을 반환합니다.

- `layer.set_weights(weights)`: NumPy형 배열의 리스트로부터 해당 층의 가중치들을 설정합니다 (get_weights의 출력과 동일한 크기를 가져야 합니다).

- `layer.get_config()`: 해당 층의 설정이 저장된 딕셔너리를 반환합니다. 모든 층은 다음과 같이 설정 내용으로부터 다시 인스턴스화 될 수 있습니다.

  ~~~ipython
  layer = Dense(32)
  config = layer.get_config()
  reconstructed_layer = Dense.from_config(config)
  ~~~

  또는,

  ~~~ipython
  rom keras import layers

  config = layer.get_config()
  layer = layers.deserialize({'class_name': layer.__class__.__name__,
                              'config': config})
  ~~~

만약 어떤 층이 단 하나의 노드만을 가지고 있다면 (즉, 공유된 층이 아닌 경우), 입력 텐서, 출력 텐서, 입력 크기 및 출력 크기를 다음과 같이 얻어올 수 있습니다.

- `layer.input`
- `layer.output`
- `layer.input_shape`
- `layer.output_shape`

만약 해당 층이 여러 개의 노드들을 가지고 있다면, 다음의 메소드들을 사용할 수 있습니다. ([케라스 함수형 API 첫걸음](https://keras.io/ko/getting-started/functional-api-guide/)의 `공유 레이어` 부분과 `레이어 "node"의 개념` 부분 참조)


- `layer.get_input_at(node_index)`
- `layer.get_output_at(node_index)`
- `layer.get_input_shape_at(node_index)`
- `layer.get_output_shape_at(node_index)`

### 1.1 Dense

보통의 밀집 연결 신경망 레이어 입니다.

~~~ipython
keras.layers.Dense(units, activation=None, use_bias=True, \
                  kernel_initializer='glorot_uniform', \
                  bias_initializer='zeros', kernel_regularizer=None, \
                  bias_regularizer=None, activity_regularizer=None, \
                  kernel_constraint=None, bias_constraint=None)
~~~

- `units`: 양의 정수, 아웃풋 공간의 차원
- `activation`: 사용할 활성화 함수. 따로 정하지 않으면, 활성화가 적용되지 않습니다. (다시 말해, "선형적" 활성화: a(x) = x)
- `use_bias`: boolean. 레이어가 편향 벡터를 사용하는지 여부
- `kernel_initializer`: kernel 가중치 행렬의 초기값 설정
- `bias_initializer`: 편향 벡터의 초기값 설정
- `kernel_regularizer`: kernel 가중치 행렬에 적용되는 정규화 함수
- `bias_regularizer`: 편향 벡터에 적용되는 정규화 함수
- `activity_regularizer`: 레이어의 아웃풋(레이어의 “활성화”)에 적용되는 정규화 함수
- `kernel_constraint`: kernel 가중치 행렬에 적용되는 제약 함수
- `bias_constraint`: 편향 벡터에 적용하는 제약 함수

`Dense`는 다음과 같은 작업을 구현합니다: 

~~~
output = activation(dot(input, kernel) + bias)
~~~

여기서 activation은 activation 인수로 전달되는 성분별 활성화 함수이고, kernel은 레이어가 만들어낸 가중치 행렬이며, bias는 레이어가 만들어낸 편향 벡터입니다 (use_bias가 True인 경우만 적용 가능합니다).

참고: 레이어의 인풋이 2를 넘는 계수를 갖는 경우 kernel과의 초기 점곱(dot 연산) 전에 직렬화됩니다.

- 인풋 형태 : (batch_size, ..., input_dim) 형태의 nD 텐서. 가장 흔한 경우는 (batch_size, input_dim) 형태의 2D 인풋입니다.

- 아웃풋 형태 : (batch_size, ..., units) 형태의 nD 텐서. 예를 들어, (batch_size, input_dim) 형태의 2D 인풋에 대해서 아웃풋은 (batch_size, units)의 형태를 갖게 됩니다.

### 1.2 Flatten

인풋을 직렬화 합니다. 배치 크기에는 영향을 주지 않습니다.

~~~ipython
keras.layers.Flatten(data_format=None)
~~~

- `data_format`: 문자열, channels_last (디폴트 값) 혹은 channels_first 중 하나. 인풋 차원의 순서. 이 인수의 목적은 모델을 하나의 데이터 형식에서 다른 형식으로 바꿀 때 가중치 순서를 보존하는 것입니다. channels_last는 (batch, ..., channels) 형태의 인풋에 호응하고, channels_first는 (batch, channels, ...) 형태의 인풋에 호응합니다. 디폴트 값은 ~/.keras/keras.json에 위치한 케라스 구성 파일의 image_data_format 값으로 지정됩니다. 따로 설정하지 않으면, 이는 "channels_last"가 됩니다.

### 1.3 Input 

`Input()`으로 케라스 텐서를 인스턴스화합니다.

~~~ipython
keras.engine.input_layer.Input()
~~~

- `shape`: 배치 크기를 제외한 형태 튜플 (정수). 예를 들어 `shape=(32,)`는 예상되는 인풋이 32차원 벡터의 배치라는 것을 나타냅니다.
- `batch_shape`: 배치 크기를 포함한 형태 튜플 (정수). 예를 들어 `batch_shape=(10, 32)`는 예상되는 인풋이 10개의 32차원 벡터로 이루어진 배치라는 것을 나타냅니다. `batch_shape=(None, 32)`는 임의의 수의 32차원 벡터로 이루어진 배치를 나타냅니다.
- `name`: 레이어에 대한 선택적 이름 문자열. 모델 내에서 고유해야 합니다 (동일한 이름을 두 번 재사용하지 마십시오). 따로 제공되지 않는 경우, 자동으로 생성됩니다.
- `dtype`: 문자열, 인풋으로 예상되는 데이터 자료형 (`float32`, `float64`, `int32`, ...)
- `sparse`: 불리언, 만들어 낼 플레이스홀더가 희소한지 여부를 특정합니다.
- `tensor`: `Input` 레이어로 래핑할 선택적 기존 텐서. 따로 설정하는 경우, 레이어는 플레이스홀더 텐서를 만들어 내지 않습니다.

케라스 텐서는 기저 백엔드(Theano, 텐서플로우 혹은 CNTK)에서 비롯된 텐서 객체로, 모델의 인풋과 아웃풋을 아는 것만으로도 케라스 모델을 만들 수 있도록 하는 특정한 속성을 부여해 증강시킵니다.

예를 들어 a, b와 c가 케라스 텐서라고 하면 다음을 수행할 수 있습니다: `model = Model(input=[a, b], output=c)`

추가된 케라스 속성은 다음과 같습니다: 

- `_keras_shape`: 케라스 쪽의 형태 유추를 통해 전파되는 정수 형태 튜플
- `_keras_history`: 텐서에 적용된 마지막 레이어. 해당 레이어에서 레이어 그래프 전체를 재귀적으로 회수할 수 있습니다.

반환값은 텐서 입니다.

### 1.4 Embedding

양의 정수(색인)를 고정된 크기의 밀집 벡터로 전환합니다. 예. [[4], [20]] -> [[0.25, 0.1], [0.6, -0.2]]

~~~ipython
keras.layers.Embedding(input_dim, output_dim, \
                      embeddings_initializer='uniform', \
                      embeddings_regularizer=None, \
                      activity_regularizer=None, \
                      embeddings_constraint=None, mask_zero=False, \
                      input_length=None)
~~~

- `input_dim`: 정수 > 0. 어휘목록의 크기, 다시 말해, 최대 정수 색인 + 1
- `output_dim`: 정수 >= 0. 밀집 임베딩의 차원
- `embeddings_initializer`: embeddings 행렬의 초기값 설정
- `embeddings_regularizer`: embeddings 행렬에 적용되는 정규화 함수
- `embeddings_constraint`: embeddings행렬에 적용되는 제약 함수
- `mask_zero`: 인풋 값 0을 마스크 처리해야 할 특수 "패딩"값으로 다룰 것인지 여부. 순환 레이어를 사용해 가변적 길이의 인풋을 전달받을 때 유용합니다. 이 값이 True인 경우 모델 내 차후 레이어는 마스킹을 지원해야 하며 그렇지 않은 경우 예외가 발생됩니다.` mask_zero`가 참으로 설정된 경우, 색인 0은 어휘목록에서 사용할 수 없습니다 (input_dim이 vocabulary + 1과 동일한 크기를 가져야 하기 때문입니다).
- `input_length`: 인풋 시퀀스의 길이로, 그 길이가 불변해야 합니다. 상위 `Dense` 레이어와 `Flatten` 레이어를 연결하려면 이 인수가 필요합니다
(그렇지 않고서는 밀집 아웃풋의 형태를 계산할 수 없습니다).

이 레이어는 모델의 첫 번째 레이어로만 사용할 수 있습니다.

- 인풋 형태 : 2D 텐서. (batch_size, sequence_length)의 형태

- 아웃풋 형태 : 3D 텐서. (batch_size, sequence_length, output_dim)의 형태

### 1.5 기타 레이어들

RNN, LSTM 등 기타 레이어들에 대한 설명은 <https://keras.io/ko/layers/about-keras-layers/>를 참고 하세요.

---

## 2. 직접 케라스 레이어 만들기

(reference: <https://keras.io/ko/layers/writing-your-own-keras-layers/>)

학습 가능한 가중치를 수반하는 커스텀 운용을 하려면 자신만의 레이어를 만들 필요가 있습니다.

Keras 2.0의 레이어는 다음의 메소드를 포함하고 있습니다. (세 가지 메서드만 구현하면 됩니다:)

- `build(input_shape)`: 이 메서드에서 가중치를 정의합니다. 끝에서는 반드시 `super([Layer], self).build()`를 호출해 `self.built = True`로 지정해야 합니다.

- `call(x)`: 레이어의 논리의 핵심이 되는 메서드입니다. 마스킹을 지원하는 레이어를 만들 것이 아니라면 call의 첫 번째 인수에 전달되는 인풋 텐서만 주의하면 됩니다.

- `compute_output_shape(input_shape)`: 레이어가 인풋의 형태를 수정하는 경우, 형태 변형 논리를 지정해야 합니다. 이는 케라스가 자동 형태 추론을 할 수 있도록 합니다.

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

기존의 케라스 레이어를 보시면 대부분의 기능을 어떻게 구현해야 하는지 참고할 수 있습니다.
