---
layout: post
title:  "Welcome to Jekyll !"
date:   2019-04-19 20:26:44 +0900
categories: Dev Jekyll
---
이 게시물은 `_posts` 디렉토리에서 찾을 수 있습니다. 계속해서 수정하고 사이트를 다시 빌드하여 변경 사항을 확인하십시오. 여러 가지 방법으로 사이트를 재구성 할 수 있지만, 가장 일반적인 방법은 웹 서버를 시작하고 파일이 업데이트 될 때 사이트를 자동으로 재생성하는 `jekyll serve`(또는 `bundle exec jekyll serve`)를 실행하는 것입니다.

새 게시물을 추가하려면, `YYYY-MM-DD-name-of-post.ext` 규약을 따르고, 필요한 [YAML 머리말(front matter)][yaml-header]을 포함하는 파일을 `_posts` 디렉토리에 추가하십시오. 이 게시물의 출처를 보고 어떻게 작동하는지에 대한 아이디어를 얻으십시오.

Jekyll은 코드 스니펫(code snippets)에 대한 강력한 지원도 제공합니다:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Jekyll을 최대한 활용하는 방법에 대한 자세한 정보는 [Jekyll 문서][jekyll-docs]를 확인하십시오. 모든 버그/기능 요청은 [Jekyll’s GitHub repo][jekyll-gh]에 제출하십시오. [Jekyll Talk][jekyll-talk]에 질문 할 수도 있습니다.

[jekyll-docs]: https://jekyllrb-ko.github.io/
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
[yaml-header]: https://jekyllrb-ko.github.io/docs/frontmatter/
