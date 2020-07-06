---
layout: post
title:  "Keras 시각화(Visualization)"
date:   2020-06-24 21:30:00
categories: Python AI
---

*(create: '20.6.24, update: '20.07.06)*

(reference: <https://keras.io/ko/visualization/>)

- [1. Keras 모델 시각화](#1-keras-모델-시각화)
- [2. Keras 학습 히스토리 시각화](#2-keras-학습-히스토리-시각화)

## 1. Keras 모델 시각화

케라스는 (`graphviz`를 사용해서) 케라스 모델을 플롯팅하기 위한 유틸리티 함수를 제공합니다.

아래 예시는 모델의 그래프를 플롯팅하고 그 결과를 파일로 저장합니다:
 
~~~ipython
from tensorflow.keras.utils import plot_model
plot_model(model, to_file='model.png')
~~~

`plot_model`는 네가지 인수를 전달받습니다:

- `show_shapes`: (디폴트값은 False)는 결과의 모양을 그래프에 나타낼 것인지 조정합니다.
- `show_layer_names`: (디폴트값은 True)는 레이어의 이름을 그래프에 나타낼 것인지 조정합니다.
- `expand_nested`: (디폴트값은 False)는 중첩된 모델을 그래프상에서 클러스터로 확장할 것인지 조정합니다.
- `dpi`: (디폴트값은 96)는 이미지 dpi를 조정합니다.

또한 직접 `pydot.Graph`오브젝트를 만들어 사용할 수도 있습니다. 예를들어, ipython notebook에 나타내자면 아래와 같이 사용할 수 있습니다:

~~~ipython
from IPython.display import SVG
from tensorflow.keras.utils import model_to_dot

SVG(model_to_dot(model).create(prog='dot', format='svg'))
~~~

## 2. Keras 학습 히스토리 시각화

케라스 `Model`의 `fit()` 메소드는 `History` 오브젝트를 반환합니다. `History.history` 속성은 연속된 에폭에 걸쳐 학습 손실 값과 학습 측정항목값을 기록하는 딕셔너리로, 또한 (적용 가능한 경우에는) 검증 손실 값과 검증 측정항목 값도 기록합니다. 아래 간단한 예시에서는 `matplotlib`을 사용하여 학습과 검증에 대한 손실과 정확성 플롯을 만듭니다:

~~~ipython
import matplotlib.pyplot as plt

history = model.fit(x, y, validation_split=0.25, epochs=50, batch_size=16, verbose=1)

# 학습 정확성 값과 검증 정확성 값을 플롯팅 합니다. 
plt.plot(history.history['acc'])
plt.plot(history.history['val_acc'])
plt.title('Model accuracy')
plt.ylabel('Accuracy')
plt.xlabel('Epoch')
plt.legend(['Train', 'Test'], loc='upper left')
plt.show()

# 학습 손실 값과 검증 손실 값을 플롯팅 합니다.
plt.plot(history.history['loss'])
plt.plot(history.history['val_loss'])
plt.title('Model loss')
plt.ylabel('Loss')
plt.xlabel('Epoch')
plt.legend(['Train', 'Test'], loc='upper left')
plt.show()
~~~
