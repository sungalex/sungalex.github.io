---
layout: post
title:  "Python Virtualenv 환경 복제하기"
date:   2020-06-20 19:00:00
categories: Python Dev
---

## Python 가상환경에 설치된 패키지를 다른 가상환경에 설치하기

- vane과 pinwheel 이라는 virtualenv 가상환경이 설치되어 있는 상황을 가정합니다.

- vane 가상환경에 설치된 패키지들를 pinwheel 가상환경에 동일하게 설치하는 방법을 소개합니다.

- anaconda 가상환경을 사용하는 경우에도 아래의 Case1과 Case2의 방법을 사용할 수 있습니다.

### (Case 1) 전체 패키지 리스트 재설치하기

- "vane" 가상환경을 활성화 한 후 설치된 패키지 리스트(버전정보 포함)를 "requirement.txt"에 저장하기

  ~~~bash
  $ activate vane
  (vane)$ pip freeze > requirement.txt
  ~~~

- "pinwheel" 가상환경을 활성화 한 후 "requirement.txt"의 패키지 리스트를 설치하기

  ~~~bash
  $ activate pinwheel
  (pinwheel)$ pip install -r requirement.txt
  ~~~

### (Case 2) pinwheel 환경에 설치되지 않은 패키지 만 추가 설치하기

#### 가상환경에 설치된 패키지 리스트 저장하기

- "vane" 가상환경에 설치된 패키지 리스트 저장하기

  ~~~bash
  $ activate vane
  (vane)$ pip freeze > vnane_requirement.txt
  ~~~

- "pinwheel" 가상환경에 설치된 패키지 리스트 저장하기

  ~~~bash
  $ activate pinwheel
  (pinwheel)$ pip freeze > pinwheel_requirement.txt
  ~~~

#### pinwheel에 설치되지 않은 패키지 리스트를 requirement.txt로 만들기

- 아래 코드를 python 파일(.py 파일)로 저장한 후 실행하면 requirement.txt 파일이 생성됨

  ~~~python
  # 파일 읽어오기
  with open("vane_requirement.txt", 'r') as vane_file:
      vane_pkg = vane_file.read()
      
  with open("pinwheel_requirement.txt", 'r') as pinwheel_file:
      pinwheel_pkg = pinwheel_file.read()
  
  # vane 패키지 설치내역 리스트로 만들기(버전 정보 포함)
  vane_list = [_.split()[0] for _ in vane_pkg.split("\n") if _ is not ""]

  # pinwheel 패키지 설치내역 리스트로 만들기 (버전 정보 제외)
  pinwheel_list = [_.split()[0] for _ in pinwheel_pkg.split("\n") if _ is not ""]
  pinwheel_list = [_.split("==")[0] for _ in pinwheel_list]

  # 설치되지 않은 패키지 찾기
  requirement = []
  for _ in vane_list:
      if _.split("==")[0] not in pinwheel_list:
          requirement.append(_)

  # requirement.txt 저장하기
  with open("requirement.txt", "w") as f:
      for _ in requirement:
          f.writelines(_ + "\n")
  ~~~

#### "pinwheel" 가상환경을 활성화 한 후 "requirement.txt"의 패키지 리스트를 설치하기

~~~bash
$ activate pinwheel
(pinwheel)$ pip install -r requirement.txt
~~~

### (Case 3) virtualenvwrapper를 사용하는 경우 가상환경 복제하기

- 아래와 같이 cpvirtualenv 명령어로 가상환경을 복제할 수 있습니다.

~~~bash
(vane)$ cpvirtualenv vane pinwheel
(vane)$ activate pinwheel
(pinwheel)$
~~~

- [virtualenvwrapper 공식 도큐먼트](https://virtualenvwrapper.readthedocs.io/en/latest/command_ref.html#cpvirtualenv)에 따르면, 아래와 같은 주의사항이 있어서 이 명령을 사용하는 것은 권장되지 않습니다.

> (구글 번역) : 가상 환경 복사는 잘 지원되지 않습니다. 각 virtualenv에는 하드 코딩 된 경로 정보가 있으며, 복사 코드가 특정 파일을 업데이트해야한다는 것을 모르는 경우가 있습니다. 주의해서 사용하십시오.
