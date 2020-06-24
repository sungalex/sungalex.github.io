---
layout: post
title:  "Jekyll Anchor links(Header IDs) 생성 Rules"
date:   2020-04-10 04:15:00 +0900
categories: Dev Jekyll
---

## Jekyll Header IDs and links

GitLab Flavored Markdown(GFM)은 표준 Markdown 표준을 확장하여, Markdown의 렌더링 된 모든 헤더에서 자동으로 ID를 가져오고, 그 ID로 페이지 내 헤더 위치를 연결할 수 있습니다. (주석은 제외)

마우스를 가져 가면 해당 ID에 대한 링크가 표시되어 다른 위치에서 사용하기 위해 링크를 더 쉽게 헤더에 복사 할 수 있습니다.

ID는 다음 규칙에 따라 헤더의 컨텐츠에서 생성됩니다.

>1. 모든 텍스트는 소문자로 변환됩니다.
>2. 단어가 아닌 텍스트(예 : 문장 부호 또는 HTML)는 제거됩니다.
>3. 모든 공백은 하이픈(-)으로 변환됩니다.
>4. 연속 된 둘 이상의 하이픈은 하나로 변환됩니다.
>5. 동일한 ID를 가진 헤더가 이미 생성 된 경우 1부터 시작하여 고유 한 증분 번호가 추가됩니다.

Markdown Header 사용 예:

~~~markdown
# This header has spaces in it
## This header has a :thumbsup: in it
# This header has Unicode in it: 한글
## This header has spaces in it
### This header has spaces in it
## This header has 3.5 in it (and parentheses)
~~~

위의 Markdown 코드는 다음과 같은 링크 ID를 생성합니다.

~~~markdown
this-header-has-spaces-in-it
this-header-has-a-in-it
this-header-has-unicode-in-it-한글
this-header-has-spaces-in-it-1
this-header-has-spaces-in-it-2
this-header-has-3-5-in-it-and-parentheses
~~~

문서 내에서 위의 링크 ID를 `[This header has spaces in it](#this-header-has-spaces-in-it)` 처럼 사용할 수 있습니다.

이모지(emoji) 처리는 헤더 ID가 생성되기 전에 발생하므로 이모지가 이미지로 변환 된 다음 ID에서 제거됩니다.

## 관련 참고 링크

- [What are the rules of converting one markdown title into an HTML anchor?](https://stackoverrun.com/ko/q/11899008)
- [GitLab documentation - Header IDs and links](https://gitlab.com/help/user/markdown.md#header-ids-and-links)
