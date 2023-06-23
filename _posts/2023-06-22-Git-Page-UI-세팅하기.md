---
layout: post
categories: github
tags: github gitpage
title: Git Page UI 세팅하기 (#2)
---

## 1. jekyll theme에 따라 세팅 과정이 다릅니다
제가 선택한 테마는 [yat](https://github.com/jeffreytse/jekyll-theme-yat) 테마 ([yat demo](https://jamstackthemes.dev/demo/theme/jekyll-theme-yat/)) 입니다.

기본적으로 테마가 html과 js, css로 만들어져있기 때문에 자신이 선택한 테마에 따라 설정을 다르게 하게 됩니다.

## 2. 길고 복잡한 페이지 설정
Gitpage를 처음 시작하는 분들을 위해 알려드립니다!

테마에 따라 설정이 조금씩 달라지니, 저와 완전히 똑같은 블로그 UI를 구성하고 싶다면 yat 테마로 시작하여 아래 글을 읽으면서 따라와주세요
다른 테마를 선택했다면 필요한 bundle 설치부터, 블로그 세팅까지 조금씩 달라집니다.

**※ 밑의 코드는 `{ %- include -% }` `{ }`와 `%- -%` 사이에 빈공간이 없으면 실제 파일을 include하라는 명령어로 인식해서 괄호 사이에 띄어쓰기 했습니다!**

### 2-1. _config.yml
_config.yml에서는 여러 설정을 변경할 수 있습니다. _config.yml의 전체 코드는 [여기](https://gist.github.com/lucyya99/3c1b8f07b2def834c149742dbbee1340)에서 확인할 수 있습니다!

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/1d4f1fac-352e-4d65-b231-6aa1b28cff1a">

저는 이 정도만 변경해주었습니다. 원작자분이 _config.yml 안에 바꿀 수 있는 설정을 꼼꼼히 적어주셨으니, 그 외에도 본인이 원하는 세팅에 맞게 변경해주세요

#### 첫페이지 설정
![설명](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/c254fbcd-d17d-4a02-8c18-0e56992e7862)

demo 페이지와 해당 설정을 비교하여 확인했습니다. _config.yml에서 해당 부분을 바꾸면 적용됩니다.

#### 기본 url 설정
```yaml
baseurl: "/"
url: "https://lucyya99.github.io"
```

#### favicon 설정
favicon은 페이지탭 옆에 나타나는 대표 이미지입니다. 보통 192x192 png 파일을 [favicon.io](https://favicon.io/)에서 favicon으로 변환하여 사용합니다.

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/1f50aab4-d2f4-45d8-8e22-2163478da568">

#### header_pages 설정

```yaml
- header_pages:
  - index.html
  - archives.html
  - tags.html
  - about.html
```

header_pages에서 페이지 순서를 바꾸면 네비게이션바에 그 순서가 그대로 나타납니다. categories는 배너를 없애면서 아직 작성한 글이 없어 레이아웃이 예쁘지 않아 삭제했습니다


#### lang: "ko" 설정

언어 설정 변경이 가능해서 기본 언어를 한국어로 바꿔주었습니다.

만약 nav에 있는 번역 설정 또한 기본을 한국어로 하고 싶다면, 추가적인 설정이 필요합니다.

_includes/views/header.html 파일 내에 `{ %- assign name = 'translate_langs' -% }`로 시작하는 코드가 있습니다.
여기에서 조금 더 밑으로 내려가, 

```html
{ %- include functions.html func='get_value' default='en' -% }
```

이 부분 또한 
```html
{ %- include functions.html func='get_value' default='kr' -% }
```
로 바꿔주어야 기본 설정이 끝납니다. 
저는 네비게이션 바에 번역이 들어가는 게 지저분해보여서 아예 제거했습니다.

### 2-2. _layouts/default.html

#### banner 삭제, 다크모드 삭제 & footer 삭제
<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/b693e59f-ddde-46d4-95fa-ed01a907b751">

비교를 위해 올렸지만, default.html에서 **[views/banner.html, extensions/theme-toggle.html]**을 없애면 됩니다. 블로그 글이 메인이라 글 위에 배너가 너무 크게 있으면 스크롤을 해야해서 불편하여 바꿔주었습니다

### 2-3. _includes/views/header.html

#### header 스크롤 수정

`initHeader`를 찾아, 함수가 정의된 부분에서 두 가지 부분을 수정해줍니다.

# 1. 이 부분을 삭제합니다
```html
{ %- if banner and header_transparent -% }
      documentElement.setAttribute("data-header-transparent", "");
{ %- endif -% }
```
배너 부분은 혹시 몰라 삭제해줍니다

# 2. `if (y <= 0)`를 `if (y < 0)`로 바꿔줍니다

스크롤이 배너 기준으로 설정되어 있어 변경해주었습니다. 배너가 없어지면서 이전 설정으로는 기본 화면에서도 네비게이션바가 없어져 네비게이션바를 통해 원하는 페이지로 이동할 수 없습니다. 따라서 y <= 0에서 y < 0으로 바꾸어 y = 0일 때도 네비게이션바가 나타나도록 만들었습니다

#### header 번역 삭제

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/e8bbe041-7fc7-4f54-89ec-70c0df40b60e">

네비게이션바가 불필요하게 늘어나는 것 같아 번역을 삭제했습니다.

## 3. _layouts/post.html

배너를 삭제하면서 배너에 글 제목을 가져오던 코드도 일반 제목으로 가져오도록 바꿔줍니다. 

배너에 글 제목을 가져오는 코드를 삭제해주면 됩니다. 밑의 코드를 삭제해주세요

```html
{ %- assign name = 'banner' -% }
{ %- include functions.html func='get_value' -% }
{ %- assign banner = return -% }
```

## 4. _includes/sidebar/article-menu.html

toc 검색 후 toc 부분을 Sub Titles로 변경합니다. 저는 TOC보다는 Sub Titles라는 제목이 더 친숙해서 바꿔주었습니다.
# 이전
```html
<div class="post-menu">
  <div class="post-menu-title">toc</div>
  <div class="post-menu-content"></div>
</div>
```

# 이후
```html
<div class="post-menu">
  <div class="post-menu-title">Sub Titles</div>
  <div class="post-menu-content"></div>
</div>
```


## 5. UI 완성!

이것으로 일단 제가 원하던 블로그의 형태를 완성했습니다 👏👏

yat 테마가 이것저것 지원중인 것이 많고 깔끔해서 선택했는데, 실제로 사용하려고 보니 쓸데없는 것들이 많아 설정을 몇가지 바꿔줘야 했네요 😅

바뀐 버전의 풀코드가 궁금하다면, 하단의 code link와 저의 [github](https://github.com/lucyya99/lucyya99.github.io)를 참고해주세요

## 6. _posts 폴더 하위에 .md 파일 작성

# 1. _posts 폴더 안에 있던 파일들을 전부 삭제합니다
# 2. 기존에 있던 형식처럼 [20**-**-**-titles.md] 이름으로 새로운 파일을 만듭니다. 특히 yat 테마에서는 파일명으로 날짜를 정해서 형식을 그대로 사용해주세요
# 3. md 파일에서 가장 처음에 이 부분을 넣어줍니다. `layout: post`는 블로그 글 작성이기 때문에 고정이고, 다른 부분은 수정해주세요
```
---
layout: post
categories: github
tags: github gitpage
title: Git Page UI 세팅하기
---
```
# 4. markdown 언어에 맞춰 글을 작성합니다.

yat 테마는 H1이 가장 작기 때문에 제목을 작성하려면 H2부터 작성하는 것이 좋습니다. 그 외의 markdown 예시는 [yat demo](https://jamstackthemes.dev/demo/theme/jekyll-theme-yat/)의 An exhibit of Markdown글을 참고해주세요!

## 7. about.html 글 수정

about 탭은 html 형식으로 본인의 프로필에 맞게 글을 수정해주세요!

## 정리
UI를 새로 정리하며 진행한 점들을 정리해보았습니다. GitPage를 처음 시작할 때 도움이 되었으면 좋겠습니다. 혹시 안되는 것이 있거나 빼먹은 점 있으면 댓글로 알려주세요! 😉

### code link
- [custom_config.yml](https://gist.github.com/lucyya99/3c1b8f07b2def834c149742dbbee1340)
- [custom_default.html](https://gist.github.com/lucyya99/07eafc479034c21dba8048cbacc01603)
- [custom_header.html](https://gist.github.com/lucyya99/07db444edf81c8fd8d2b753a8ebc2478)

### 참고링크
- [gist 코드 넣기](https://mrw0119.tistory.com/126)
- [소스코드 이미지 넣기](https://velog.io/@yeseolee/%EC%86%8C%EC%8A%A4%EC%BD%94%EB%93%9C%EB%A5%BC-%EB%B8%94%EB%A1%9C%EA%B7%B8%EC%97%90-%EC%98%AC%EB%A6%B4%EB%95%8C)


## 다음 편 예고
다음 편에서는 본격적으로 블로그 글을 작성할 때 알아두면 좋은 꿀팁을 소개하겠습니다!