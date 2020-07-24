---
layout: post
title:  "Jupyter Notebook에 가상환경 kernel 추가하기"
date:   2020-07-07 01:10:00
categories: Python Dev
---

가상환경에 개발환경이 세팅된 상황에서 jupyter notebook에서 가상환경을 사용하기 위해, Jupyter Notebook에 가상환경 kernel을 추가한다.

아래와 같이 Jupyter Notebook에 가상환경 kernel을 추가해두면, Jupyter notebook을 사용중에 다른 가상환경의 노트북 파일을 생성하여 실행할 수 있다. Jupyter Notebook 실행 중에 가상환경을 전환하지 않고, Jupyter Notebook 우측 상단에 `New` 버튼을 선택 하여 원하는 가상환경의 노트북 파일을 생성할 수 있다. (예로, tensorflow 1.0 환경을 사용중에, tensorflow 2.0 환경으로 전환하여 작업할 수 있다.)

아래의 방법1과 방법2의 실행 결과는 동일하며, 방법2의 경우 Jupyter Notebook kernel 환경설정에 대한 이해에 도움이 되며, `kernel.json`에 다양한 옵션을 자유롭게 설정할 수 있다.

아래의 예는 Mac 환경의 경우이지만, Windows 환경에서도 동일한 방법으로 kernel을 추가할 수 있다. (파일의 경로와 가상환경 activate 명령이 조금 다름)

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

## \[참고\] Jupyter Notebook에 추가된 가상환경 kernel 삭제하기

위의 "4. kernel.json file 생성하기"에서 설명한 `/Users/alex/Library/Jupyter/kernels` 아래에 있는 폴더 중 삭제하고자 하는 가상환경 커널의 폴더를 아래의 명령으로 삭제한다.

~~~bash
rm -rf <폴더명>
~~~

- `rm -rf' 명령은 실수로 잘못된 폴더를 삭제하지 않도록 사용 시 각별한 주의가 필요하다.
