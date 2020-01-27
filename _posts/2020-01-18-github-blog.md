---
title: "첫번째 - 블로그 만들기"
date: 2020-01-18
categories: jekyll blog
---

간단하게 `github` 를 통해서 블로그를 만드는 과정을 포스팅합니다.  



# 시작하는 글

 `github` 은 `GitHub Pages` 라는 서비스를 제공합니다.

간단히 `github` 저장소에 형식에 맞게 프로젝트를 구성하면, 자동으로 웹서버를 배포(Publishing) 해줍니다.

이때  웹서버를 구성하기 위한 프레임워크로 `ruby`기반의 `jekyll` 라이브러리를 지원합니다.

이를 이용해서 현재 블로그 사이트를 개설한 과정을 이번 포스트에 작성하려고 합니다.



# 테마 선택

`jekyll` 을 사용한다고 해도, 처음부터 모든 것을 다 개발하기에는 너무 많은 공부가 필요합니다.

다행히, `jekyll` 은 여러가지 테마 템플릿을 제공하며, 이를 사용하면, 쉽게 기본 블로그를 만들 수 있습니다.

다만, `GitHub Pages` 서비스에서는 `jekyll` 의 확장 기능(라이브러리)들을 전부 지원하는 것이 아니기 때문에, 지원하는 테마에서 자신의 블로그 테마를 설정하는 것이 좋습니다.

> 지원 가능한 테마는 아래 사이트에서 확인이 가능합니다.
>
> - [Supported themes](https://pages.github.com/themes/)



## ~~Cayman~~

~~저는 이번에 `Cayman` 테마를 선택했습니다.~~

> ~~해당 템플릿 소스는 아래 사이트에서 확인이 가능합니다.~~
>
> - ~~[Cayman repository](https://github.com/pages-themes/cayman)~~



~~[ `Cayman` 데모 사이트](https://pages-themes.github.io/cayman/) 에서 `Download .tar.gz` 버튼을 클릭하여 해당 소스의 압축파일을 받습니다.~~

~~이를 압축해제하여 제 블로그 프로젝트에 덮어쓰기를 합니다.~~



~~제대로 덮어쓰기를 했다면, 제 블로그 사이트 주소에서 `Cayman` 테마 사이트가 그대로 보이게 됩니다.~~

> - ~~`Settings` 에서 주소를 확인할 수 있습니다.~~
> - ~~프로젝트 이름을 `{블로그명}.github.io` 으로 작성하면 기본적으로 `GitHub Pages` 로 인식하며, 별도의 설정없이 `https://{블로그명}.github.io/` 경로로 배포됩니다.~~



## minima

 앞서 설정한 `Cayman` 의 경우, 시작 페이지가 기본 웹사이트 처럼되어 있어, 블로그 형식으로 바꾸기 위해서는 레이아웃 구조를 변경해야합니다. 

레이아웃 구조를 하나씩 바꾸기엔 아직 `jekyll` 에 대한 지식이 낮으므로, 블로그 형식이 되는 기본 템플릿을 사용하도록 변경하였습니다.

> `minima` 소스는 다음 저장소에서 확인이 가능합니다.
>
> - [minima repository](https://github.com/jekyll/minima)



위와 마찬가지 방법으로, minima 저장소에서 해당 소스를 다운로드 받아, 블로그 프로젝트에 덮어 씌웁니다.



## 기본 설정 변경

`_config.yml` 에서 기본적인 정보를 입력합니다.

```yml
title: 50dev's Stroy
author: 50dev
email: 
description: > # this means to ignore newlines until "show_excerpts:"
   평범한 개발자가 50살에도 개발을 할 수 있을까? 하는 궁금증을 갖고 살아가는 이야기를 담는 블로그입니다.
```



`./posts/2020-01-18-github-blog.md` 현재 보이고 있는 블로그 내용을 `markdown` 언어로 작성을 합니다.



아래는 이렇게 작성할 경우, 실제 <https://50dev.github.io/> 에서 보이는 시작화면입니다.

---

![시작페이지]({{"assets/images/2020-01-18-01.png" | relative_url}})

---



## 날짜 포멧 변경

템플릿의 기본 날짜 포멧은 `%b %-d, %Y` 입니다. 이 경우, "월(영문명) 일 년" 과 같은 형식으로 표현되기 때문에, 이를 변경해줍니다.

`%Y-%m-%d` 로 변경하면, `2020-01-18` 과 같은 형식으로 보이게 됩니다. 

`_config.yml` 에서 다음과 같이 변경해줍니다.

```yml
minima:
  date_format: "%Y-%m-%d" #"%b %-d, %Y"
```



# 마치는 글

이제 `_posts/` 폴더에 포스트를 `yyyy-mm-dd-{포스트제목}.md` 형식으로 작성하고, 포스트 상단에 다음과 같은 ymal 머리말을 덧붙이면, 기본적인 포스트글을 작성할 수 있게 되었습니다.

```markdown
---
title: "첫번째 - 블로그 만들기"
date: 2020-01-18
categories: jekyll blog
---
```

> 이에 대한 가이드는 다음을 참고하시면 됩니다.
>
> - [포스트 작성하기](https://jekyllrb-ko.github.io/docs/posts/)



아직 화면 상단이나, 하단의 공통화면 정리가 필요하지만, 일단 포스트를 작성할 수 있는 공간을 만들어 놓은 것으로 이번 포스팅을 마칠까 합니다.



# 참고 사이트

- [Working with GitHub Pages](https://help.github.com/en/github/working-with-github-pages)
- [Jekylly 한국어 사이트](https://jekyllrb-ko.github.io/)
