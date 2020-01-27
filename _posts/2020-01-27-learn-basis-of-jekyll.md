---
title: "Jekyll 기본 익히기"
date: 2020-01-27
categories: jekyll blog
---



이번 포스트에서 간단히  Jekyll 을 공부하고, 간단한 설정을 변경해 봅니다.



# 시작하기

지난 포스트(![첫번째 - 블로그 만들기]({{ site.baseurl }}{% post_url 2020-01-18-github-blog %})) 에서 간단한 블로그 사이트를 개설해 보았습니다.



이번에는 여기에 몇가지 사이트에서 보이는 링크 설정들을 변경해보려고 합니다.



# 기본 구조

프로젝트 파일에서 `index.md` 를 확인하면, 다음과 같습니다. 

```md
---
#
# By default, content added below the "---" mark will appear in the home page
# between the top bar and the list of recent posts.
# To change the home page layout, edit the _layouts/home.html file.
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
#
layout: home
---
```



 `---`  로 감싸고 있는 부분이 YAML 머리말(Front Matter) 라고 하며 이런 부분을 통해 각 파일의 메타파일을 저장할 수 있습니다.

- [Jekyll - 







여기에서는 `layout` 정보를 표시하고 있으며, 이를 따라가며 레이아웃의 계층구조를 파악해보면, 다음과 같습니다.

- `index.md` > `_layout/home.html` > `_layout/default.html`



# 변수

Jekyll 에서 사용하는 변수는 다음 사이트에서 확인할 수 있습니다.

- [Jekyll - 변수](https://jekyllrb-ko.github.io/docs/variables/)



## site

사이트 변수는 프로젝트 내 YAML 이 읽을 수 있는 값들을 나타냅니다.

현재 제 프로젝트의 `_config.yml` 은 다음과 같습니다.

```yml
title: 50dev's Stroy
author: 50dev
email: 
description: > # this means to ignore newlines until "show_excerpts:"
   평범한 개발자가 50살에도 개발을 할 수 있을까? 하는 궁금증을 갖고 살아가는 이야기를 담는 블로그입니다.

show_excerpts: false # set to true to show excerpts on the homepage

# Minima date format
# refer to https://shopify.github.io/liquid/filters/date/ if you want to customize this
minima:
  date_format: "%Y-%m-%d" #"%b %-d, %Y"

  # generate social links in footer
  social_links:
    twitter: jekyllrb
    github:  jekyll
    rss: rss
    
# 이하 생략 ...
```



이럴 때, 각 변수들은 다음과 같이 다른 파일에서 접근할 수 있습니다.

```
site.title
site.minima.date_format
site.minima.social_links
```



또는 프로젝트의 사전에 정의된 폴더 내 파일에도 접근할 수 있습니다.

`/_layouts_home.html` 일부를 살펴보면 다음과 같습니다.

```html
			{%- for post in site.posts -%}
      <li>
        <span class="post-meta">{{ post.date | date: date_format }}</span>
        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>
        {%- if site.show_excerpts -%}
          {{ post.excerpt }}
        {%- endif -%}
      </li>
      {%- endfor -%}
```



이 내용을 보시면, `site.posts` 는 `_posts/` 폴더의 파일들을 가르키고 있으며, 이에 대한 개별 파일을 `post` 로 선언하였습니다.

이때 각 파일들에 정의되어 있는 YAML 머리말을 `post.title` 과 같은 방법으로 읽어올 수 있습니다.



## page

최종 컨텐츠 영역에 정의된 YAML 머리말에 정의된 변수들을 상위 템플릿에서 읽어들일 때 사용합니다.

>  `md` 형식이 제가 현재 사용하는 일반적인 최종 컨텐츠 영역입니다. 그외의 케이스에 대해서는 추후에 확인이 필요합니다.

예를 들면 다음과 같습니다.

```
page.title
```



# 상단 메뉴 바꾸기

현재 기본 설정으로 상단 메뉴에 `About` 과 `HEAD` 메뉴가 있습니다.

이 설정을 한 파일 위치를 파악해서 다른 내용으로 바꾸려합니다.



상단 메뉴는 다음 파일에서 `_includes/header.html` 에서 다음과 같이 설정되어 있습니다.

```html
  	  {%- assign default_paths = site.pages | map: "path" -%}
      {%- assign page_paths = site.header_pages | default: default_paths -%}
				<!-- 중간생략... -->
				<div class="trigger">
          {%- for path in page_paths -%}
            {%- assign my_page = site.pages | where: "path", path | first -%}
            {%- if my_page.title -%}
            <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
            {%- endif -%}
          {%- endfor -%}
        </div>
```



> 해당 파일은 블로그 사이트의 검사에서 클래스를 확인한 후, 전체 단어검색에서 `trigger` 를 검색하여 찾았습니다.



위 문법은 [Liquid 문법](https://shopify.github.io/liquid/) 을 공부해야 하는데, 일부만 확인하도록 하겠습니다.

```html
{%- assign default_paths = site.pages | map: "path" -%}
```

- `site.pages` 정보 중에, `path` 속성값으로 배열을 만들어 이를 `defualt_paths` 변수에 할당합니다.

```html
{%- assign page_paths = site.header_pages | default: default_paths -%}
```

- `site.header_pages` 정보를 `page_paths` 변수에 할당하고, 만약 해당 값이 없을 경우,  `default` 값을 할당합니다.

```html
{%- assign my_page = site.pages | where: "path", path | first -%}
```

- `site.pages` 에서 `path` 속성이 변수 path 인 값을 필터링하여, 첫번째 파일을 `my_page` 에 할당합니다.



여러 테스트를 해서 알아낸 결과는, `site.pages` 는  `*.md` 또는 `*.markdown`  파일을 가르키며, `README.md` 와 `index.md`는 예외처리됩니다.

또한 `_layout/` 과 같은 `_` 로 시작하는 폴더 내의 파일도 예외 처리됩니다.

> 시스템에서 인식하는 몇가지 사전 설정이 있는 것으로 보입니다.



현재 `site.pages` 의 값을 바꾸는 법을 알지 못하므로, `common_pages` 폴더에 원하는 파일을 넣고, `_config.xml` 에 `header_pages` 속성을 정의하는 것으로 원하는 파일을 표시하도록 하였습니다.

```yml
# If you want to link only specific pages in your header, uncomment
# this and add the path to the pages in order as they should show up
header_pages:
 - common_pages/tooltips.md
```









