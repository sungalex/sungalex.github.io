---
layout: post
title:  "conda install 시 SSL Certificate Error 처리 방법"
date:   2020-06-16 12:30:00 +0900
categories: Developer Python
---

conda 명령어 사용 시 아래와 같은 SSL Certificate 오류가 발생하는 경우는,

  ~~~bash
  > Could not fetch URL https://pypi.org/...: There was a problem confirming the ssl certificate: HTTPSConnectionPool(host='pypi.org', port=443): Max retries exceeded with url: ... (Caused by SSLError(SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate (_ssl.c:1076)')))
  ~~~

임시 해결책으로 아래와 같이 ssl_verify 설정을 false로 변경하면 문제를 비켜갈 수 있습니다.(보안상 권장되지는 않습니다.)

  ~~~bash
  conda config --set ssl_verify false
  ~~~

<https://rfriend.tistory.com/304> 블로그에서 이 문제의 다양한 해결 방법을 확인 할 수 있습니다.
