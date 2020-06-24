---
layout: post
title:  "Keras 모델(keras.models)"
date:   2020-06-24 17:00:00
categories: Python AI
---

*(create: '20.6.24, update: '20.6.24)*

- [Keras 모델에 관하여](#keras-모델에-관하여)
- [Sequential 모델 API](#sequential-모델-api)
- [Keras 함수형 API](#keras-함수형-api)

---

## Keras 모델에 관하여

(reference: <https://keras.io/ko/models/about-keras-models/>)

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

---

## Sequential 모델 API

(reference: <https://keras.io/ko/models/sequential/>)




---

## Keras 함수형 API

(reference: <https://keras.io/ko/models/model/>)


