---
layout: post
title:  "Jupyter Notebook Interactive Widget 사용하기"
date:   2020-06-20 21:30:00
categories: Python Dev
---

## Jupyter Interactive Widget (ipyWidget)

### Jupyter Interactive Widget 개요

- 사용자로 부터 입력을 받을 수 있게 해주는 Jupyter UI Component

- 잦은 Hyper parameter 변경을 테스트 해야 하는 경우 사용하면 편리함

- Jupyter의 Interactive Widget(ipyWidget) Reference : https://ipywidgets.readthedocs.io/en/latest/examples/Using%20Interact.html

### Jupyter ipyWidget 설치

- Reference : https://ipywidgets.readthedocs.io/en/latest/user_install.html

- pip 설치 및 활성화

  ~~~bash
  $ pip install ipywidgets
  $ jupyter nbextension enable --py widgetsnbextension
  ~~~

  - virtualenv를 사용하고 활성화 된 가상 환경에서 작업 할 경우, widget을 활성화하고 가상환경을 격리시키기 위해 `--sys-prefix` 옵션을 사용해야 할 수 있습니다. (ex. `jupyter nbextension enable --py widgetsnbextension --sys-prefix`)

- conda 설치 (설치하면 자동으로 활성화 됨)

  ~~~bash
  $ conda install -c conda-forge ipywidgets
  ~~~

- multiple 환경에 설치하는 경우(notebook은 `base` 환경에 설치되어 있고, kernel은 `py36` 환경에 설치되어 있다면), `widgetsnbextension`을 Notebook이 설치된 환경에 먼저 설치 후, `ipywidgets`을 kernel이 설치된 환경에 설치

  ~~~bash
  $ conda install -n base -c conda-forge widgetsnbextension
  $ conda install -n py36 -c conda-forge ipywidgets
  ~~~

- Jupyter Lab을 사용하는 경우 labextension을 추가로 설치한다.

  - nldejs를 먼저 설치해야 한다.

    ~~~bash
    $ pip install nodejs
    ~~~

  - conda 환경을 사용하는 경우 nodejs 설치한다.

    ~~~bash
    $ conda install -c conda-forge nodejs
    ~~~

  - labextension jupyterlab-manager을 설치한다.

    ~~~bash
    $ jupyter labextension install @jupyter-widgets/jupyterlab-manager
    ~~~

## Interact 

- Reference
  - https://ipywidgets.readthedocs.io/en/latest/examples/Using%20Interact.html#
  - https://junpyopark.github.io/interactive_jupyter/
  - https://towardsdatascience.com/interactive-controls-for-jupyter-notebooks-f5c94829aee6

### Callback 방식

~~~ipython
from __future__ import print_function
from ipywidgets import interact, interactive, fixed, interact_manual
import ipywidgets as widgets

def f(x):
  return x

interact(f, x=10);    # UI control 생성
~~~

### Decorator 방식

~~~ipython
@interact(x=True, y=1.0)
def g(x, y):
  return (x, y)
~~~

### 그래프 예제

~~~ipython
from ipywidgets import interactive
import matplotlib.pyplot as plt
import numpy as np

def f(m, b):
  plt.figure(2)
  x = np.linspace(-10, 10, num=1000)
  plt.plot(x, m * x + b)
  plt.ylim(-5, 5)
  plt.show()

interactive_plot = interactive(f, m=(-2.0, 2.0), b=(-3, 3, 0.5))
output = interactive_plot.children[-1]
output.layout.height = '350px'
interactive_plot
~~~
