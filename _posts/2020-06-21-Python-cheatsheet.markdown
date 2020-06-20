---
layout: post
title:  "Python 개발 Cheatsheet"
date:   2020-06-21 02:00:00
categories: Python Dev
---

*(create: '20.6.21, update: '20.6.21)*

## 편집기 다중선택 기능 사용하기

- 다중선택 : Ctrl + 클릭, 클릭, 클릭, ...

- 이동 : 방향키, Ctrl + 좌우 방향키 (Mac에서는 Alt)

- 범위지정 : Ctrl + Shift + 방향키, Shift + 방향키

## help/dir 확인 및 특정 속성/method 검색

- **dir() 내장함수** : 어떤 객체를 인자로 넣어주면 해당 객체가 어떤 변수와 메소드(method)를 가지고 있는지 나열해줍니다.

  ~~~ipython
  import numpy as np
  dir(np)
  ~~~

- **help() 내장함수** : 문자열을 전달하면 모듈, 함수, 클래스, 메서드, 키워드 또는 설명서 주제의 이름으로 조회하여, 도움말 페이지가 콘솔에 인쇄됩니다. 인자가 다른 종류의 객체면, 객체에 대한 도움말 페이지가 만들어집니다. `help()` 대신에 `?`를 사용할 수 있습니다.
  
  ~~~ipython
  ?np    # help(np)
  ~~~

- 특정 라이브러리의 특정 문자열이 포함된 속성이나 메소드 찾아보기1

  ~~~ipython
  # numpy에 array가 포함된 속성(함수) 찾기 예
  print('\n'.join([s for s in dir(np) if s.find("array") >= 0]))
  ~~~

- 특정 라이브러리의 특정 문자열이 포함된 속성이나 메소드 찾아보기2

  ~~~
  import pandas as pd

  data = {
  "Sepal_Length":[5.1,4.9,4.7,4.6,5  ,5.4,4.6,5  ],
  "Sepal_Width": [3.5,3  ,3.2,3.1,3.6,3.9,3.4,3.4]
  }

  df = pd.DataFrame(data = data)    
  _m = "df"       # 검색 대상 (DataFrame)
  _k = "to_"      # 찾을 속성이나 메소드: "to_"로 시작하는 함수
  print('\n'.join([s for s in dir(eval(_m)) if s.find(_k)  >= 0 ]))
  ~~~

