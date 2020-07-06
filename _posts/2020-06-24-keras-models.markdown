---
layout: post
title:  "Keras 모델(keras.models)"
date:   2020-06-24 20:00:00
categories: Python AI
---

*(create: '20.6.24, update: '20.07.06)*

- [Keras 모델에 관하여](#keras-모델에-관하여)
- [Sequential 모델 API](#sequential-모델-api)
  - [compile 메소드](#compile-메소드)
  - [fit 메소드](#fit-메소드)
  - [evaluate 메소드](#evaluate-메소드)
  - [predict 메소드](#predict-메소드)
- [Keras 함수형 API(Model 클래스 API)](#keras-함수형-apimodel-클래스-api)
- [Model 하위 클래스 만들기](#model-하위-클래스-만들기)

-----

## Keras 모델에 관하여

(reference: <https://keras.io/ko/models/about-keras-models/>)

Keras가 제공하는 모델에는 [Sequential 모델](https://keras.io/ko/models/sequential/)과 [함수형 API와 함께 사용되는 Model 클래스](https://keras.io/models/model) 두 가지 종류가 있습니다.

이 모델들은 아래의 메소드들과 속성들을 공통적으로 가지고 있습니다.

- `model.layers`: 모델을 구성하는 층들이 저장된 1차원 리스트 입니다.
- `model.inputs`: 모델의 입력 텐서들이 저장된 1차원 리스트 입니다.
- `model.outputs`: 모델의 출력 텐서들이 저장된 1차원 리스트 입니다.
- `model.summary()`: 모델의 구조를 요약해 출력해 줍니다. `utils.print_summary(model)`로도 동일한 출력을 얻을 수 있습니다.
- `model.get_config()`: 모델의 설정이 저장된 딕셔너리를 반환합니다. 모든 모델은 다음과 같이 `from_config()` 메소드로 설정 내용으로부터 다시 인스턴스화 될 수 있습니다.

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

-----

## Sequential 모델 API

(reference: <https://keras.io/ko/models/sequential/>)

### compile 메소드

학습을 위해서 모델의 옵티마이저, 손실함수 등을 설정 합니다.

~~~ipython
compile(optimizer, loss=None, metrics=None, \
        loss_weights=None, sample_weight_mode=None, \
        weighted_metrics=None, target_tensors=None, **kwargs)
~~~

- optimizer: 문자열 (옵티마이저의 이름) 혹은 옵티마이저 인스턴스. [옵티마이저](https://keras.io/ko/optimizers)를 참고하십시오.

- loss: 문자열 (목적 함수의 이름) 혹은 목적 함수. [손실함수](https://keras.io/ko/losses)을 참고 하십시오. 모델이 다중 아웃풋을 갖는 경우, 손실의 리스트나 딕셔너리를 전달해서 각 아웃풋에 다른 종류의 손실을 사용할 수 있습니다. 그러면 모델이 최소화할 손실값은 모든 개별 손실의 합이 됩니다.

- metrics: 학습 혹은 테스트 과정에서 평가할 측정항목의 리스트. 보통은 metrics=\['accuracy'\]를 사용하게 됩니다. 다중 아웃풋 모델의 다양한 아웃풋에 각기 다른 측정항목을 특정하려면, metrics={'output_a': 'accuracy'}와 같은 딕셔너리를 전달하는 수도 있습니다.

### fit 메소드

정해진 수의 Epoch에 걸쳐 모델을 학습시킵니다(데이터셋에 대한 반복).

~~~ipython
fit(x=None, y=None, batch_size=None, epochs=1, verbose=1, \
    callbacks=None, validation_split=0.0, validation_data=None, \
    shuffle=True, class_weight=None, sample_weight=None, \
    initial_epoch=0, steps_per_epoch=None, validation_steps=None)
~~~

- 인수

  - x: (모델이 단일 인풋을 갖는 경우) 표적(라벨) 데이터의 Numpy 배열, 혹은 (모델이 다중 아웃풋을 갖는 경우) Numpy 배열의 리스트. 모델의 아웃풋 레이어에 이름이 명명된 경우는 아웃풋 이름을 Numpy 배열에 매핑하는 딕셔너리를 전달할 수도 있습니다. 프레임워크 네이티브 텐서(예. 텐서플로우 데이터 텐서)를 전달받는 경우 x를 None(디폴트 값)으로 둘 수 있습니다.
  
  - y: (모델이 단일 인풋을 갖는 경우) 표적(라벨) 데이터의 Numpy 배열, 혹은 (모델이 다중 아웃풋을 갖는 경우) Numpy 배열의 리스트. 모델의 아웃풋 레이어에 이름이 명명된 경우는 아웃풋 이름을 Numpy 배열에 매핑하는 딕셔너리를 전달할 수도 있습니다. 프레임워크 네이티브 텐서(예. 텐서플로우 데이터 텐서)를 전달받는 경우 y를 None(디폴트 값)으로 둘 수 있습니다.
  
  - batch_size: 정수 혹은 None. 경사 업데이트 별 샘플의 수. 따로 정하지 않으면 batch_size는 디폴트 값인 32가 됩니다.
  
  - epochs: 정수. 모델을 학습시킬 세대의 수. 한 세대는 제공된 모든 x와 y 데이터에 대한 반복입니다. initial_epoch이 첫 세대라면, epochs은 "마지막 세대"로 이해하면 됩니다. 모델은 epochs에 주어진 반복의 수만큼 학습되는 것이 아니라, 단지 epochs 색인의 세대에 도달할 때까지만 학습됩니다.
  
  - verbose: 정수. 0, 1, 혹은 2. 다변 모드. 0 = 자동, 1 = 진행 표시줄, 2 = 세대 당 한 라인.

- 반환값

  - `History` 객체. `History.history` 속성은 연속된 세대에 걸친 학습 손실 값과 측정항목 값, 그리고 (적용 가능한 경우) 검증 손실 값과 검증 측정항목 값의 기록입니다.

### evaluate 메소드

테스트 모드에서의 모델의 손실 값과 측정항목 값을 반환합니다.

계산은 배치 단위로 실행됩니다.

~~~ipython
evaluate(x=None, y=None, batch_size=None, verbose=1, \
        sample_weight=None, steps=None, callbacks=None)
~~~

- 인수

  - x: (모델이 단일 인풋을 갖는 경우) 표적(라벨) 데이터의 Numpy 배열, 혹은 (모델이 다중 아웃풋을 갖는 경우) Numpy 배열의 리스트. 모델의 아웃풋 레이어에 이름이 명명된 경우는 아웃풋 이름을 Numpy 배열에 매핑하는 딕셔너리를 전달할 수도 있습니다. 프레임워크 네이티브 텐서(예. 텐서플로우 데이터 텐서)를 전달받는 경우 x를 None(디폴트 값)으로 둘 수 있습니다.
  
  - y: (모델이 단일 인풋을 갖는 경우) 표적(라벨) 데이터의 Numpy 배열, 혹은 (모델이 다중 아웃풋을 갖는 경우) Numpy 배열의 리스트. 모델의 아웃풋 레이어에 이름이 명명된 경우는 아웃풋 이름을 Numpy 배열에 매핑하는 딕셔너리를 전달할 수도 있습니다. 프레임워크 네이티브 텐서(예. 텐서플로우 데이터 텐서)를 전달받는 경우 y를 None(디폴트 값)으로 둘 수 있습니다.
  
  - batch_size: 정수 혹은 None. 경사 업데이트 별 샘플의 수. 따로 정하지 않으면 batch_size는 디폴트 값인 32가 됩니다.
  
  - verbose: 0 혹은 1. 다변 모드. 0 = 자동, 1 = 진행 표시줄.

- 반환값 : (모델이 단일 아웃풋만 갖고 측정항목을 보유하지 않는 경우) 스칼라 테스트 손실, 혹은 (모델이 다중 아웃풋, 그리고/혹은 측정항목을 갖는 경우) 스칼라 리스트. model.metrics_names속성은 스칼라 아웃풋에 대한 디스플레이 라벨을 제공합니다.

### predict 메소드

인풋 샘플에 대한 아웃풋 예측을 생성합니다.

계산은 배치 단위로 실행됩니다.

~~~ipython
predict(x, batch_size=None, verbose=0, steps=None, callbacks=None)
~~~

- 인수

  - x: Numpy 배열 (혹은 모델이 다중 인풋을 갖는 경우 Numpy 배열의 리스트) 형태의 인풋 데이터.
  
  - batch_size: 정수. 따로 정하지 않으면 디폴트 값인 32가 됩니다.
  
  - verbose: 다변 모드, 0 혹은 1.
  
  - steps: 예측이 한 회 완료되었음을 선언하기까지 단계(샘플 배치)의 총 개수. 디폴트 값인 None의 경우 고려되지 않습니다.

- 반환값 : 예측 값의 Numpy 배열.

-----

## Keras 함수형 API(Model 클래스 API)

(reference: <https://keras.io/ko/models/model/>)

함수형 API에서, 인풋 텐서와 아웃풋 텐서가 주어졌을 때, Model을 다음과 같이 인스턴스화 할 수 있습니다:

~~~ipython
from tensorflow.keras.models import Model
from tensorflow.keras.layers import Input, Dense

a = Input(shape=(32,))
b = Dense(32)(a)
model = Model(inputs=a, outputs=b)
~~~

이 모델은 `a`를 받아 `b`를 계산하는데 필요한 모든 레이어를 포함합니다.

다중 인풋 혹은 다중 아웃풋 모델의 경우 아래와 같이 리스트를 사용할 수도 있습니다:

~~~ipython
model = Model(inputs=[a1, a2], outputs=[b1, b2, b3])
~~~

`Model`로 할 수 있는 작업에 대한 보다 자세한 설명은 [케라스 함수형 API 첫걸음](https://keras.io/ko/getting-started/functional-api-guide)과 [The Functional API](https://keras.io/guides/functional_api/)를 참조하십시오.

`Model 클래스 API`의 메소드는 `Sequential 모델 API`의 메소드와 거의 동일합니다.
[Sequential 모델 API](#sequential-모델-api) 부분을 참고하세요.

-----

## Model 하위 클래스 만들기

(reference: <https://keras.io/ko/models/about-keras-models/> > #Model-하위-클래스-만들기)

Keras 2.2.0 버전부터 `Model` 클래스의 하위 클래스를 만들어 모델을 구현할 수 있는 API가 추가되었습니다. 해당 API를 사용해 `Model`의 하위 클래스를 만들고, `call` 메소드에 사용자의 요구에 맞는 포워드 패스 과정을 구현하여 모델을 만들 수도 있습니다.

다음은 `Model`의 하위 클래스로서 만들어진 간단한 다층 퍼셉트론의 예제입니다.

~~~ipython
from tensorflow import keras

class SimpleMLP(keras.Model):

    def __init__(self, use_bn=False, use_dp=False, num_classes=10):
        super(SimpleMLP, self).__init__(name='mlp')
        self.use_bn = use_bn
        self.use_dp = use_dp
        self.num_classes = num_classes

        self.dense1 = keras.layers.Dense(32, activation='relu')
        self.dense2 = keras.layers.Dense(num_classes, activation='softmax')
        if self.use_dp:    # Dropout layer를 사용
            self.dp = keras.layers.Dropout(0.5)
        if self.use_bn:    # 배치정규화를 사용
            self.bn = keras.layers.BatchNormalization(axis=-1)

    def call(self, inputs):
        x = self.dense1(inputs)
        if self.use_dp:
            x = self.dp(x)
        if self.use_bn:
            x = self.bn(x)
        return self.dense2(x)

model = SimpleMLP()   # 모델 생성 시 Dropout, 배치정규화 옵션을 지정(True or False)
model.compile(...)
model.fit(...)
~~~

모델에 사용되는 각 층은 `__init__(self, ...)`에 정의되어 있고, 포워드 패스는 `call(self, inputs)`에 구현되어 있습니다. 임의의 층을 지정해 주는 것과 같이 사용자는 `call` 내부에서 self.add_loss(loss_tensor)를 호출함으로써 임의의 손실 함수를 지정해줄 수도 있습니다.( `__init__()`에 `loss_tensor`를 먼저 정의해야 함 )

위와 같이 모델을 구현할 때 모델의 구조는 정적 그래프가 아닌 Python 코드로서 정의되기 때문에, 모델의 구조를 확인하거나 저장할 수 없습니다. 결과적으로 해당 API를 사용하여 모델을 구현한 경우 다음의 메소드들과 속성들을 사용할 수 없습니다.

  - `model.inputs`, `model.outputs`, `model.to_yaml()`, `model.to_json()`, `model.get_config()`, `model.save()`

※ **중요한 점**: 작업에 적합한 API를 사용해야 합니다. Model 클래스의 하위 클래스를 만드는 API는 복잡한 모델을 구현하는데 있어서 높은 유연성을 제공해 줄 수는 있지만, 코드가 좀 더 길고 복잡해지며, 사용자 오류의 소지가 높아진다는 단점이 있습니다. 가능하면 사용자 친화적인 함수형 API를 사용하는 것이 좋습니다.
