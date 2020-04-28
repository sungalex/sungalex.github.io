---
layout: post
title:  "[Study3] Python Fundamentals and Basic Librarys"
date:   2020-04-28 10:15:00 +0900
categories: AI&QA Python
---

*[AI와 QA의 만남] - Study Day3 (학습일: '20.04.28, create: '20.04.28)*

## Python 이란?

파이썬(Python)은 1990년 귀도 반 로섬(Guido Van Rossum)이 개발한 인터프리터 언어이다.

*※ 인터프리터 언어란 한 줄씩 소스 코드를 해석해서 그때그때 실행해 결과를 바로 확인할 수 있는 언어이다.*

파이썬은 머신러닝/딥러닝을 위해서는 거의 필수로 사용해야 하는 언어이다.

## Python Study 자료들

- [점프 투 파이썬(Jump to Python)](https://sungalex.github.io/python/2020/03/31/Jump-to-Python.html) : Python(파이썬)을 처음 접해보는 독자들과 프로그래밍을 한 번도 해 본적이 없는 사람들을 대상으로 하는 Python 안내서 이다.

- [회오리바람을 탄 파이썬(A Whirlwind Tour of Python)](https://sungalex.github.io/python/2020/04/06/WhirlwindTourOfPython.html) : 다른 프로그래밍 언어를 이미 알고 있는 연구자와 개발자들에게 파이썬의 핵심 요소를 빠르게 전달하기 위한 안내서 이며, 파이썬을 데이터 과학이나 과학 프로그래밍에 사용하는데 촛점을 맞춘 학습 안내서 이다. 제이크 반더플라스(Jake VanderPlas)의 원문과, 박해선 님의
한글 번역본을 이용할 수 있다.

## Python 필수 라이브러리들

numpy, matplotlib, pandas 학습을 위해 [Hands on Machine Learning Github 사이트(박해선 님의 Github을 Fork한 Repository)](https://github.com/sungalex/handson-ml.git)를 Local로 Clone 합니다.

```bash
git clone https://github.com/sungalex/handson-ml.git
```

### numpy

- NumPy는 다차원 데이터 배열을 위한 효율적인 저장과 연산을 제공합니다.

- 위에서 clone 한 Hands on Machine Learning Repository에 포함된 `tools_numpy.ipynb` 파일을 jupyter notebook 환경에서 학습 합니다. 박해선 님이 한글로 번역 하였습니다.

- numpy 공식 사이트 : <https://numpy.org>

### matplotlib

- Matplotlib은 출판 가능한 퀄리티의 그래프와 이미지를 만들기 위한 편리한 인터페이스를 제공합니다.

- 위에서 clone 한 Hands on Machine Learning Repository에 포함된 `tools_matplotlib.ipynb` 파일을 jupyter notebook 환경에서 학습 합니다.

- matplotlib 공식 사이트 : <https://matplotlib.org>

### pandas

- Pandas는 데이터의 조작, 필터링, 그룹핑, 변환을 위한 강력한 메서드를 가진 DataFrame 객체를 제공합니다.

- 위에서 clone 한 Hands on Machine Learning Repository에 포함된 `tools_pandas.ipynb` 파일을 jupyter notebook 환경에서 학습 합니다.

- pandas 공식 사이트 : <https://pandas.pydata.org/>
