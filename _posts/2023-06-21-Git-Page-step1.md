---
layout: post
categories: github
tags: github gitpage
title: Git Page 처음 시작하기 (#1)
---

## 0. 시작하기 전
저는 windows 환경에서 진행합니다. 참고해주세요!

기술 블로그를 시작하면서 다음과 같은 기준으로 GitPage를 선택했습니다

1. 비용이 들지 않는다
2. 커스텀이 가능하다
3. 댓글 기능과 같은 기본적인 블로그 기능을 사용할 수 있다

특히 GitPage는 비용이 안들지만 커스텀이 가능하다는 것이 큰 장점입니다. 커스텀이 가능한 덕분에 처음 시작할 때 할 일이 많긴 합니다..

## 1. GitPage의 개념
GitPage는 사용자가 작성한 정적페이지를 웹으로 호스팅해주는 서비스입니다.

정적페이지이기 때문에 서버와 연동해서 데이터를 저장하는 등의 작업은 할 수 없지만, 블로그 글과 같이 간단한 위키를 작성할 때 적합합니다.
정적페이지이지만 추가적으로 다른 곳에서 제공하는 utterance와 같은 서비스를 이용하면 댓글 기능도 넣을 수 있습니다.

전체적으로 [여기](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-2/)에서 참고해서 진행하였습니다!

## 2. GitPage 생성하기

### 2-1. repository로 운영하는 방법
# 1. {id}.github.io 이름으로 repository 생성

public으로 생성해야합니다! {id}.github.io라는 이름으로 id당 하나의 대표 GitPage를 생성할 수 있습니다

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/1aedc389-7b37-4cc5-afb0-fa08626d5a62">

# 2. Settings - Pages에서 Deploy from branch로 선택, branch가 main인지 확인

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/fe3fa79c-2362-4ceb-b618-c50afb67139e">

저는 저의 대표 블로그이기 때문에 {id}.github.io로 시작하는 repository를 파서 진행하였습니다.

### 2-2. 따로 브랜치를 파서 운영하는 방법
이번 학기에 진행했던 프로젝트에서 사용했던 방법입니다. 제가 만든 [팀 프로젝트 소개페이지](https://kookmin-sw.github.io/capstone-2023-08/)입니다. 팀 프로젝트 Github는 프론트, 백엔드, ML로 브랜치를 나누어서 PR을 넣도록 만들고, 마지막에 master 브랜치에 병합하도록 규칙을 정했습니다. GitPage는 프로젝트와 독립적으로 존재한다고 생각해, 병합하지 않고 따로 브랜치를 운영하는 것이 좋을 것이라 판단했습니다.

방법은 간단합니다. Settings > Pages > Build and deployment에서 Branch를 원하는 것으로 선택해주면 됩니다.

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/ab1006ee-5b05-4bc9-b691-4e9141910d72">

이와 같이 프로젝트의 간단한 소개페이지도 GitPage로 만들 수 있습니다.

### 2-3. 하위 폴더를 하나 더 만들어서 운영하는 방법
Settings > Pages > Build and deployment에서 branch 옆에 있는 폴더를 설정해주면 됩니다. 2-2번에 있는 그림을 참조해주세요.

팀 프로젝트 블로그를 어떻게 만들어야하나 고민이 되었는데, 이와 같이 브랜치나 폴더를 설정해서도 호스팅을 할 수 있습니다!

## 3. Jekyll Theme 선택
[jekyllthemes.org](http://jekyllthemes.org/)에 접속하면 여러 테마를 확인할 수 있습니다. 이외에도 jekyll theme best를 검색하면 무료이지만 좋은 테마들을 많이 찾을 수 있습니다.

제가 선택한 테마는 [yat](https://github.com/jeffreytse/jekyll-theme-yat) 테마 ([yat demo](https://jamstackthemes.dev/demo/theme/jekyll-theme-yat/)) 입니다.
1. 카테고리, 날짜, 태그별로 글을 나눠 분류해준다.
2. 오른쪽에 제목별로 이동할 수 있는 링크가 생긴다. (=toc라고 부름)

이 두가지 편의성이 마음에 들어 테마를 선택했습니다.

# 1. 선택했다면 해당 테마를 다운받습니다. 

[yat github](https://github.com/jeffreytse/jekyll-theme-yat)으로 이동해서 code > download zip을 선택해주세요. 해당 repository를 fork하는 방법도 있지만, yat 테마를 변경해서 다시 yat github에 반영할게 아니라면 그냥 다운로드받는 것을 추천합니다.

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/b538ca84-9a76-47ce-bec5-b20a56757878">

# 2. 압축을 풀고, .github 폴더를 삭제합니다. 

.github 폴더를 제거하지 않으면, GitPage 설정이 테마를 제작하신 분의 설정으로 들어갑니다.

# 3. git clone으로 생성했던 repository를 로컬에 가져옵니다.
```git
git clone https://github.com/lucyya99/lucyya99.github.io
```

# 4. window 탐색기에서 clone한 폴더로 이동 후, 폴더 안에 파일들을 전부 넣어줍니다

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/25368431-3644-4bd6-84b3-5fed72169de3">

## 4. Ruby 설치

블로그 글을 올리기 전에, 로컬에서 확인하는 것은 필수입니다! 서버에서 페이지를 build and deploy하는 데 시간이 약간 걸리기 때문에 무조건 ruby를 설치하여 로컬에서 확인 후 서버에 올리는 것을 추천합니다. 

jekyll은 마크다운 언어를 html로 바꿔주는 변환기라고 생각하면 됩니다. jekyll은 ruby라는 언어로 만들어졌기 때문에 로컬에서 GitPage를 확인하기 위해서는 ruby를 설치해야 합니다. (ruby 설치만으로 안될 때는 jekyll도 설치해주세요. 저는 설치하지 않아도 잘 작동해서 굳이 설치하지 않았습니다.. )

# 1. ruby 설치
[ruby](https://rubyinstaller.org/downloads/)로 이동 후, with devkit에 있는 것 중에 환경에 맞는 것을 선택해주세요. 저는 귀찮아서 가장 위에 있는 `Ruby+Devkit 3.2.2-1 (x64)`를 설치해주었습니다

기본적인 설정은 원하는 것을 선택해줍니다. 저는 대부분 기본 설정으로 선택했습니다. 다른 것은 대충 넘겨줘도 되지만, 환경변수는 windows에서 따로 설정하기 귀찮으므로 설치할 때 체크가 되어있는지 확인합니다. 전부 설치된 후 나오는 cmd에서 3번 옵션을 선택해 설치를 마무리합니다.

# 2. ruby prompt 실행
windows 검색창에서 **ruby**를 검색해, Start Command Prompt With Ruby를 선택합니다

# 3. clone한 폴더로 이동

`cd {경로}`라는 명령어로 원하는 경로로 이동할 수 있습니다. 제 컴퓨터의 기본 경로가 `C:\Users\{username}`이기 때문에 `cd lucyya99.github.io`라는 명령어를 통해 원하는 폴더로 이동했습니다. 저는 상대경로를 사용하지만, 절대경로로 이동해도 됩니다. windows에서 절대 경로를 복사하는 방법은 [여기](https://mainia.tistory.com/5112)를 참고해서 `cd {절대경로}`를 입력해주세요.
```ruby
cd lucyya99.github.io
```

# 4. 처음 시작하는 경우, bundle install을 진행합니다
```ruby
bundle install
```

# 5. 로컬 jekyll 서버를 실행합니다
```ruby
bundle exec jekyll serve
```
<br><br>
해당 캡처처럼 `http://127.0.0.1:4000/`로 접속하라는 문구가 뜨면 성공입니다!

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/34b8d914-df06-4965-b62a-57deaedc0004">

다른 jekyll 테마 중 최신 업데이트가 안되어있는 경우, bundle이 설치되지 않았다는 오류가 뜨는 경우가 있습니다. yat 테마는 다행히 warning만 발생하고 다른 문제는 없네요. warning을 굳이 해결해주진 않겠습니다

성공했다면 브라우저에 `http://127.0.0.1:4000/`을 입력하여 블로그 화면을 확인해줍니다.

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/1d9b127e-1d93-479d-850e-76f53fb18f77">

## 5. Github Repository에 push
로컬에서의 작동을 확인했다면, github에 해당 코드를 올려야 실제 GitPage에 반영이 됩니다. 여기에서부터는 github 동작 방식을 알고 있어야 합니다. [git 동작원리](https://jow1025.tistory.com/344)를 이해할 수 있는 링크를 같이 올려둘테니 참고해주세요.

# 1. git 작동 툴을 열고, clone한 폴더로 이동합니다.
```git
cd lucyya99.github.io
```

# 2. add, commit, push해서 github repository에 코드를 올려줍니다. 
```git
git add .
git commit -m "GitPage yat 테마로 시작!"
git push origin main
```

## 6. GitPage 확인!

해당 파일들을 Github에 올렸다면, Actions탭에서 페이지 생성이 되었는지 확인할 수 있습니다. 보통 1분 정도 기다리면 성공했다는 표시가 뜹니다

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/13f6d6dd-cc15-4ff1-9d6c-bec756da3baa">

만약 실패했다면 원인과 함께 이메일이 옵니다.. 보통은 bundle 미설치 오류입니다.

build가 되었는지 확인한 후, 생성했던 repository 이름을 주소창에 입력하면 드디어 생성된 페이지를 확인할 수 있습니다. 저의 경우는 `https://lucyya99.github.io/`입니다.

되었다면 1단계 성공입니다! 👏👏

## ⭐7. 앞으로 GitPage 수정하는 과정 요약

지금까지 원하는 GitPage를 구축하는 것에는 성공했지만, 앞으로는 구축된 GitPage를 수정하여 사용해야합니다.

# 1. ruby prompt에서 git clone한 폴더로 이동, `bundle exec jekyll serve`로 로컬 서버를 엽니다
# 2. 브라우저에서 `http://127.0.0.1:4000/`를 입력하여 로컬에서 화면이 어떻게 나오는지 확인합니다

특히 **_config.yml 파일을 수정하는 경우, ruby prompt에서 로컬 서버를 종료한 후 재실행해주세요.** 먼저 수정한 _config.yml을 저장합니다. ruby prompt에서 ctrl+c를 2번 눌러 로컬 서버를 종료한 후, 키보드에서 ⬆를 눌러 이전에 입력했던 명령어인 `bundle exec jekyll serve`를 재입력합니다. 브라우저를 새로고침하면 수정된 화면이 보입니다!

**다른 파일을 수정할 때**는 종료 후 재실행하는 과정 없이, **[파일 저장 + 브라우저 새로고침]**하면 변경된 화면을 바로 확인할 수 있습니다!

# 3. git 작동 툴을 이용해 코드를 github repository에 push합니다
# 4. `https://lucyya99.github.io/`와 같은 GitPage 주소에 접속해 서버에서도 화면이 제대로 나오는 지 확인합니다

이 4가지 과정을 계속 반복하여 글을 게시할 수 있습니다

## 정리
GitPage를 처음 만들어봐서 모르는 점이 많아 저도 처음에는 많이 헤맸는데, 이 글을 보시는 분들은 덜 헤맸으면 좋겠습니다. 테마마다 오류나는 부분이 조금씩 다른데, 위에서 언급했다시피 대부분 bundle 미설치 때문인 것을 알아두고 검색하시면 좋을 것 같아요!

### 참고자료
- [전체적인 참고](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-2/)
- [git 동작원리](https://jow1025.tistory.com/344)