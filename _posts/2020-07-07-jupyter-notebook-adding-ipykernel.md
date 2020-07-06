---
layout: post
title:  "Jupyter Notebook에 가상환경 kernel 추가하기"
date:   2020-07-07 01:10:00
categories: Python Dev
---

가상환경에 개발환경이 세팅된 상황에서 jupyter notebook에서 가상환경을 사용하기 위해, Jupyter Notebook에 가상환경 kernel을 추가한다.

-----

## \[방법1\] ipykernel install 명령으로 추가하기

### 1. 가상환경 활성화

~~~bash
source activate [virtualEnv]
~~~

- \[virtualEnv\]는 실제 가상환경 이름으로 변경하여 사용 

  예:

  ~~~bash
  source activate pinwheel
  ~~~

### 2. 가상환경에 jupyter kernel 설치

~~~bash
pip install ipykernel
~~~

### 3. jupyter notebook에 가상환경 kernel 추가

~~~bash
python -m ipykernel install --user --name [virtualEnv] --display-name [displayKenrelName]
~~~

예:

~~~bash
python -m ipykernel install --user --name pinwheel --display-name venv_pinwheel
~~~

### 4. jupyter notebook 실행해서 kernel이 추가 됐는지 확인

~~~bash
jupyter notebook
~~~

- jupyter notebook 우측 상단에 `New` 버튼을 선택 하여, 위에서 추가한 커널로 새로운 노트북을 생성해본다.

-----

## \[방법2\] kernel.json file을 직접 생성하기

### 1. 가상환경 활성화

~~~bash
source activate [virtualEnv]
~~~

- \[virtualEnv\]는 실제 가상환경 이름으로 변경하여 사용 

### 2. 가상환경에 jupyter kernel 설치

~~~bash
pip install ipykernel
~~~

### 3. 가상환경의 설정을 확인한다.

Jupyter의 설정들을 보기 위해 터미널에서 `jupyter --paths`를 실행한다.

~~~bash
jupyter --paths
~~~

출력 결과는 대충 아래와 유사할 것이다. (아래는 Mac의 경우이다.)
~~~
config:
    /Users/alex/.jupyter
    /Users/alex/venvs/pinwheel/bin/../etc/jupyter
    /usr/local/etc/jupyter
    /etc/jupyter
data:
    /Users/alex/Library/Jupyter
    /Users/alex/venvs/pinwheel/bin/../share/jupyter
    /usr/local/share/jupyter
    /usr/share/jupyter
runtime:
    /Users/alex/Library/Jupyter/runtime
~~~

출력 결과 중에 `runtime:`의 경로인 `/Users/alex/Library/Jupyter/runtime`의 바로 상위 경로인 `/Users/alex/Library/Jupyter/` 아래에 `/Users/alex/Library/Jupyter/kernels` 경로로 이동하자. (`kernels` 디렉토리가 없으면 만들어준다.)

아래 명령으로 가상환경의 python 설치 경로를 확인한다.

~~~bash
which python
~~~

출력 결과는 대충 아래와 같을 것이다. (개인 마다 설치된 경로가 다를수 있다.)

~~~
/Users/alex/venvs/pinwheel/bin/python
~~~

### 4. kernel.json file 생성하기

마지막으로, `/Users/alex/Library/Jupyter/kernels` 경로에 `kernel.json` file을 하나 생성하고, 아래 내용을 추가해준다. ("argv" 인자에 위에서 확인한 가상환경의 python 설치경로를 지정해준다.)

~~~
{
 "argv": [ "/Users/alex/venvs/pinwheel/bin/python", "-m", "ipykernel",
          "-f", "{connection_file}"],
 "display_name": "venv_pinwheel",
 "language": "python"
}
~~~

jupyter notebook을 실행해서 가상환경이 추가되어 있는지 확인한다.
