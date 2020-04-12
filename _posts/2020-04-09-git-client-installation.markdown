---
layout: post
title:  "Windows git client 설치하기"
date:   2020-04-09 11:45:00 +0900
categories: Developer
---

## Git client 설치하기

git은 linux를 개발한 리누스 토르발스(Linus Benedict Torvalds)가 개발한 분산형 버전 관리 시스템(VCS) 입니다.

다양한 git client가 있지만, Windows 환경에서 git을 사용하는 가장 간단한 방법은 [git 공식 사이트](https://git-scm.com/)에서 제공하는
Client 프로그램을 사용하는 것이 입니다.

<https://git-scm.com/downloads> 사이트에서 Windwos 버전을 선택하여 다운로드 후 실행 합니다.

![git_download](/img/git-download.png)

설치 과정의 선택 사항들은 기본적으로 선택되어 있는 항목을 특별히 변경하지 않고 "Next"를 선택해도 됩니다.
설치 과정을 설명하는 <https://goddaehee.tistory.com/216> 사이트를 참고하세요.

## Github GUI client 설치하기

[Github.com](https://github.com) 계정에 가입 합니다.

![github-sign-up](/img/github-sign-up.png)

깃허브 회원 가입절차는 [깃허브(GitHub) 회원 가입하기(계정 만들기)](https://goddaehee.tistory.com/218) 블로그 글을 참고 합니다.

Github에서 제공하는 [GitHub Desktop](https://desktop.github.com)을 다운로드 하여 설치 합니다.

![github-desktop](/img/github-desktop-download.png)

저장소(Repository)를 Local로 가져오기는 방법은 [깃허브 데스크탑(GitHub Desktop) 사용](https://github.com/cau-cmclab/sku-cmclab.github.io/wiki/깃허브-데스크탑(GitHub-Desktop)-사용#3-2-저장소repository-가져오기clone) 블로그 글을 참고 합니다.

## git SSL Certificate 에러 해결하기

git push 또는 pull 수행 시 다음의 에러가 발생한다면,

  ```
  SSL Certificate problem: unable to get local issuer
  ```

아래 global option을 사용하여 인증서의 유효성 검사를 수행하지 않도록 할 수 있습니다.

  ```
  git config --global http.sslVerify false
  ```

이 문제의 구체적인 해결 방법은 Bitbucket 지식 저장소 사이트의 [SSL certificate problem: Unable to get local issuer certificate](https://confluence.atlassian.com/bitbucketserverkb/ssl-certificate-problem-unable-to-get-local-issuer-certificate-816521128.html) 게시물에서 확인할 수 있습니다.
