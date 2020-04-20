---
layout: post
title:  "[Study1] 딥러닝 개발환경 & AI/머신러닝/딥러닝 개념 이해하기"
date:   2020-04-10 02:00:00 +0900
categories: AI&QA
---

*[AI와 QA의 만남] - Study Day1 (학습일: '20.04.13)*

## AI/머신러닝/딥러닝 개념 이해하기

- [머신러닝 vs 딥러닝 vs 인공지능? A.I. 개념정리!](https://www.youtube.com/watch?v=arbbhHyRP90) : 니콜라스의 초간단 설명, 다양한 이미지/영상을 포함하여 설명 (*인사 만 한국말... 한글 자막 있음*)

  [![AI 개념정리 동영상](/img/study1/ai-concept-youtube.png)](https://www.youtube.com/watch?v=arbbhHyRP90)

- [김형진님 유튜브 영상 보기](https://www.youtube.com/watch?v=aF03asAmQbY) : 우버 머신러닝 엔지니어가 실제 현업 엔지니어 관점에서 설명

  [![김형진 유튜브](/img/study1/hjkim-uber-ml.png)](https://www.youtube.com/watch?v=aF03asAmQbY)

- [Raj Ramesh 유튜브 영상 보기](https://www.youtube.com/watch?v=2ePf9rue1Ao) : AI 분류에 대해 그림으로 설명 (*그림 그리는 실력이 대단함. 배우고 싶네... 한글 자막이 없어서 아쉬움*)

  [![what-is-ai](/img/study1/what-is-ai.jpg)](https://www.youtube.com/watch?v=2ePf9rue1Ao)

- [김성훈 교수님의 유튜브 영상 보기](https://www.youtube.com/watch?v=qPMeuL2LIqY) : 교수님 답게 이론적인 설명에 충실함 (*재미는 없음!!!*)

  [![김성운 유튜브](/img/study1/hunkim-ml-basics.png)](https://www.youtube.com/watch?v=qPMeuL2LIqY)

- AI, Machine Learning, Deep Learning을 텍스트로 정리해보면...

    ![ai-machinelearning-deeplearning](/img/study1/ai-machinelearning-deeplearning.png)
    (그림 출처: <https://blogs.nvidia.co.kr/2016/08/03/difference_ai_learning_machinelearning/>)

  - **AI(Artifical Intelligence)**
    - 인공지능은 인간의 지능을 갖고 있는 기능을 갖춘 컴퓨터 시스템이나 인간의 지능을 기계 등에 인공적으로 시연(구현)한 것
    - 또는 그와 같은 지능을 만들 수 있는 방법론이나 실현 가능성 등을 연구하는 과학 분야
    - 분류 : 강인공지능(strong AI, 범용인공지능, AGI) vs. 약인공지능(weak AI), 또는 AGI(Artifical General Intelligence) vs. ANI(Artifical Narrow Intelligence)

  - **Machine Learning**
    - 명시적 프로그래밍(Explicit Programming)으로는 처리하기 어려운(because too many rules) 문제를 해결하기 위해, "명시적 프로그래밍 없이 컴퓨터가 학습하는 능력을 갖도록 하는 방법을 연구 분야"
    - AI를 구현하기 위한 방법. AI와 Machine Learning을 거의 동일한 개념으로 지칭하기도 함
    - 분류 : 지도 학습, 비지도 학습, 강화학습

  - **Deep learning**
    - Machine Learning 알고리즘의 집합. Machine Learning을 달성하기 위한 방법
    - 큰 틀에서 사람의 사고방식을 컴퓨터에게 가르치는 Machine Learning의 한 분야
    - 지금 우리가 학습하고자 하는 내용이 Deep Learning(Deep Neural Network, DNN) 기술들 임 (*딥러닝을 공부하자는 얘기~~~*)

- Artificial Neural Network(ANN), Deep Neural Network(DNN)에 대해 좀더 알아보자!!!

  - [인공지능, 기계학습 그리고 딥러닝 Slideshare, 이진원/SNU](https://www.slideshare.net/JinWonLee9/ss-70446412) : 8, 14~15, 23, 26~36페이지 참조

  - [[머신러닝] 머신러닝?!](https://devtimes.com/bigdata/2019/01/30/machine-learning/) : 스팸필터를 만들기 위해서는... 전통적인 접근 방식 vs. 머신러닝 접근 방식... 

  - [딥러닝의 기본 개념](https://www.youtube.com/watch?v=n7DNueHGkqE) (*김성훈 교수님의 강의, Neural Network(신경망) 개념부터 Deep Leaning까지 체계적인 정리*)

    [![딥러닝의 기본 개념](/img/study1/deep-neural-nets-for-everyone.png)](https://www.youtube.com/watch?v=n7DNueHGkqE)

  - [밑바닥부터 시작하는 딥러닝 도서 학습하기](https://nbviewer.jupyter.org/github/sungalex/deep-learning-from-scratch/tree/master/) (Notebook Viewer에서 보기)
    - [Github Repository에서 확인하기](https://github.com/sungalex/deep-learning-from-scratch/) (*Github Repository에서 직접 확인 시 Markdown으로 작성된 설명 부분이 깨져보이는 경우가 있음*)
    - Local에서 Jupyter Notebook을 통해 직접 확인하고 실행해보기 (*Github Repository를 Clone 할 폴더로 이동하여 아래 명령을 차례로 실행하기*)

      ~~~bash
      git clone https://github.com/sungalex/deep-learning-from-scratch.git

      cd deep-learning-from-scratch

      jupyter notebook
      ~~~

      - 위의 첫번째 명령은 학습할 Github Repository를 현재 폴더 아래에 deep-learning-from-scratch 이라는 폴더에 Clone 함 (폴더명을 지정하지 않으면, Repository 이름과 동일한 폴더에 Clone 함)
      - 세번째 줄의 `jupyter notebook` 명령으로 주피터 노트북을 실행하고, 브라우저에서 "_mystudy" 폴더 아래에 있는 파일들을 선택하여 학습

## 딥러닝 개발환경 이해하기

- [딥러닝 개발환경 구축하기](https://sungalex.github.io/developer/2020/04/06/딥러닝-개발환경-구축하기-Windows.html#ide(visual-studio-code)-설치하기)

- [Jupyter Notebook 기본 사용법](https://greeksharifa.github.io/references/2019/01/26/Jupyter-usage/#jupyter의-기본-사용법)

- [Google Colab(코랩) 환경설정 및 사용법](https://theorydb.github.io/dev/2019/08/23/dev-ml-colab/)

- [파이썬 초심자를 위한 PIP 그리고 Virtualenv 소개](https://medium.com/@dan_kim/파이썬-초심자를-위한-pip-그리고-virtualenv-소개-a53512fab3c2)

- [Docker란 무엇입니까?](https://aws.amazon.com/ko/docker/)

- [초보를 위한 도커 안내서](https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html)

## 추천 도서 및 추천 강좌

- [AI 초보자를 위한 추천 도서 및 추천 강좌][recommendation] 참조

[recommendation]: https://sungalex.github.io/ai&asr/ai&nlp/ai&qa/ai&vision/developer/python/2020/04/09/AI-추천도서-추천강좌.html
