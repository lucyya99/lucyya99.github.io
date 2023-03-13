---
layout: post
categories: github
tags: github
---

# Git Page로 개발자 블로그 시작하기

## 1. {id}.github.io로 repository 생성
## 2. Settings - Pages에서 Deploy from branch로 선택, branch가 main인지 확인
## 3. jekyll theme 선택
[jekyllthemes.org](http://jekyllthemes.org/)에 접속하면 여러 테마를 확인할 수 있습니다.

제가 선택한 테마는 [yat](https://github.com/jeffreytse/jekyll-theme-yat) 테마입니다.
1. 카테고리, 날짜, 태그별로 글을 나눠 분류해준다.
2. Headline를 사용하면 오른쪽에 이동할 수 있는 링크가 생긴다.

이 두가지 편의성이 마음에 들어 테마를 선택했습니다.

## 4. 길고 복잡한 페이지 설정
_config.yml에서는 여러 설정을 변경할 수 있습니다.
```
title: Developer Lv1.
email: lucyya99@gmail.com
author: lucyya99

lang: "ko"

heading: "개발자 Lv1."
subheading: "안녕하세요, 개발자가 되기 위한 공부를 시작합니다."
banner: "skyblue.png"
```

저는 이 정도만 변경해주었습니다. 원작자분이 _config.yml 안에 바꿀 수 있는 설정을 꼼꼼히 적어주셨으니, 그 외에도 본인이 원하는 세팅에 맞게 변경해주세요

- lang: "ko"

저는 한국인이고 대부분 한국어로 포스팅할 예정입니다. 언어 설정 변경이 가능해서 기본 언어를 한국어로 바꿔주었습니다.

- banner: "skyblue.png"

banner는 ARCHIVES, CATEGORIES, TAGS와 같은 분류 항목들의 배경입니다. 기본으로 삽입된 동영상이 시끄러워서 그냥 색상만 있는 이미지를 넣어주었습니다.