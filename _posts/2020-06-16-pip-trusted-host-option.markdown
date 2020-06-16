---
layout: post
title:  "pip PackagesNotFoundError 발생 시 --trusted-host option 사용방법"
date:   2020-06-16 13:30:00 +0900
categories: Developer Python
---

pip install 실행 시 아래와 같이 PackagesNotFoundError 에러가 나는 경우,

  ~~~bash
  Collecting package metadata (current_repodata.json): done
  Solving environment: failed with initial frozen solve. Retrying with flexible solve.
  PackagesNotFoundError: The following packages are not available from current channels:
  ~~~

아래와 같이 `--trusted-host` 옵션을 사용하여 설치 할 수 있다.

  ~~~bash
  pip --trusted-host pypi.org --trusted-host files.pythonhosted.org install <패키지명>
  ~~~
