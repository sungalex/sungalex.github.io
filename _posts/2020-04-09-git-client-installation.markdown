---
layout: post
title:  "Windows git client 설치하기"
date:   2020-04-06 22:50:00 +0900
categories: Developer
---

## Github client 설치하기

다양한 git client가 있지만, Github 사이트 위주로 이용한다면 Github에서 제공하는 GUI Client 프로그램을 사용하는 것이 가장 간단한 방법 입니다.

## git SSL Certificate 에러 해결하기

git push 또는 pull 수행 시 다음의 에러가 발생한다면,

  ```
  SSL Certificate problem: unable to get local issuer
  ```

아래 global option을 사용하여 인증서의 유효성 검사를 수행하지 않도록 할 수 있습니다.

  ```
  git config --global http.sslVerify false
  ```

이 문제의 구체적인 해결 방법은 [여기](https://confluence.atlassian.com/bitbucketserverkb/ssl-certificate-problem-unable-to-get-local-issuer-certificate-816521128.html)를 참고하세요.
