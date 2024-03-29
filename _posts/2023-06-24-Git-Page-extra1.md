---
layout: post
categories: github
tags: github gitpage
title: Git Page - Github Actions란 (#999)
---

## 0. 알아둘 점

이번 글은 의식의 흐름대로 작성하였습니다...

## 1. .github 폴더 삭제해야하는 이유
yat 테마를 다운로드 받으면, .github 폴더도 포함된다. 이게 중요한 이유는 .github 폴더 안에 yat demo에 대한 build and deploy 방식이 적힌 파일이 있다는 것이다. 

원래 문제점은, _posts 폴더 내에 md 파일을 작성해도 작성한 글이 GitPage에 나타나지 않는다는 것이었다.

사진은 yat github 화면이다. yat에만 있어야하는 분홍색 박스 부분이 {id}.github.io 부분에 그대로 나타나서 의문을 가지게 되었다.

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/a696d8c7-2edc-4926-bc86-014336c775ff">

코드를 하나하나 비교해 보았더니, .github 폴더만 달랐다.

.github 폴더 안을 대충 보니, 실행할 브랜치명도 다르고 딱 봐도 테마 원작자가 본인 데모용으로 만들어둔 코드같아 보여서 이걸 삭제하면 되겠다 싶었다.

.github 폴더를 삭제하니, 성공했다!

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/fbebf153-1c0c-45b1-a422-e826331e7d50">

## 2. 하지만 남은 의문점 ...

문제해결은 되었지만, 여전히 내 repo에서는 .github 폴더가 있고, 지인 repo에는 .github 폴더가 생성되지 않았다. 나는 이게 너무 이상하다고 생각해서 계속 차이점을 찾아보았다.

한가지 차이점을 발견했다. 브랜치에 배포했던 지인과는 다르게, 내 Actions 탭에는 commit 이름이 한번 더 뜬다는 것이었다.

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/76868a95-d07e-42b7-9ba0-44655e2ce4d2"> 

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/35f18bed-c958-4ead-9475-b768e5adfc60">

왼쪽 부분에서 내 repo에 Deploy Jekyll(이하 생략) 부분이 하나 더 많은 것을 볼 수 있다. 

혹시 new workflow를 눌러 생성하면 되는지 궁금해서 new workflow > Pages > Github Pages Jekyll > configure 버튼을 눌러 새로운 workflow를 생성했더니, 내 .github 폴더에 있던 파일과 똑같은 파일이 생성되었다.

**이 workflow라는 폴더 안의 파일이 무엇을 의미하는지, 원래 테마에서 사용하는 것과 내 것은 무엇이 다른지 궁금해져서 내 repo 코드와 yat repo 코드를 직접적으로 비교해보았다.**

- [lucyya99.github.io](https://github.com/lucyya99/lucyya99.github.io/blob/main/.github/workflows/jekyll-gh-pages.yml)
- [yat theme github](https://github.com/jeffreytse/jekyll-theme-yat/blob/master/.github/workflows/build-jekyll.yml)

### 처음 발견한 차이점

|차이점 |내 repo|yat repo|
|:--------------------------|:--------------------------|:--------------------------|
|push 확인 브랜치|main|master|
|build and deploy 과정|build와 deploy 과정으로 나뉨|build and deploy로 합쳐짐|

### + 각각 코드에 대한 대충 해석 (Github Actions 공부전)

#### 내 repo

build 과정에서 내 main 브랜치로 이동(Checkout), Jekyll이 정적 사이트 생성, 업로드. deploy 과정에서 Github Page로 배포.

#### yat repo

repo의 코드를 가져오기 위해 token을 이용하여 인증하고, gh-pages라는 브랜치를 따로 이용한다(?) 정도로 해석했음.

### 코드에서 찾은 공통점

아직 yat repo 이해는 안가지만 yat 테마와 내 repo에서 공통적으로 actions/****@v* 이런 형식이 나와서 이걸 알아보면 코드 동작방식을 이해할 수 있을 것 같았다.

```yaml
actions/checkout@v2
```

이에 관해 조금 더 자세히 알아보려면 Github Actions가 무엇인지, 어떻게 동작하는지 알아야한다고 생각했다.

언뜻 스쳐지나가는 기억에 Gitpage 만들면서 deploy from branch가 아니라 Github Actions를 눌러 블로그를 배포한 적이 있는데, 그래서 그 잔여물이 남아있는 것 같다

### 어쩌다보니 Github Actions 공부
[침고자료](https://www.daleseo.com/github-actions-basics/)로 Github Actions에 대해 간단히 자세히 알아보자

1. Github Actions란 코드 저장소에서 변화가 일어날 때마다 해야하는 작업들을 자동화해둔 것을 의미한다.

2. workflow는 변화 시점을, jobs는 작업을 의미한다

네이버 블로그와 같이 커스텀이 불가능한 블로그만 작성하다가, GitPage를 작성하면서 '배포'라는 것이 자동으로 일어나는 것이 아님을 손수 깨닫게 되는 것 같다 😅

#### 본격적인 코드 리뷰

글이 너무 길어져서 내 repo에 있는 코드만 이해해보려 한다.

코드가 무엇인지 이해하기 위해 글을 작성했는데, 명령어 하나하나가 무엇인지 알고 싶다면 [github docs](https://docs.github.com/ko/actions/examples/using-scripts-to-test-your-code-on-a-runner#features-used-in-this-example)를 참고하면 된다.

내 repo에서는 main 브랜치에 push될 때 작업을 실행한다!
```
on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]
```

작업은 build and deploy이다.

먼저 build를 살펴보자.

```
build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Build with Jekyll
        uses: actions/jekyll-build-pages@v1
        with:
          source: ./
          destination: ./_site
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
```

작업은 GitHub에서 호스트하는 ubuntu-latest 실행기에서 실행된다. `uses`는 해당 작업을 검색하도록 지시하는 명령어다. 여기에 지정된 actions는 [이미 Marketplace에 올라온 것들](https://github.com/actions/)을 사용할 수도 있고, [custom](https://docs.github.com/en/actions/creating-actions/about-custom-actions#using-release-management-for-actions)해서 사용할 수도 있다.

# 1. uses: actions/checkout@v3
리포지토리를 체크 아웃하고 실행기로 다운로드한다. git에서 `checkout`은  브랜치를 바꾸는 명령어다.

# 2. uses: actions/configure-pages@v3
[여기](https://github.com/actions/configure-pages/blob/main/action.yml)에서 확인해보면, GitPage에 관한 metadata를 생성한다고 한다. 어떤 metadata인지는 하단에 보기 쉽게 적어두었다.

|metadata|예시|_config.yml|
|:--------|:-----------------------------------|-----------|
|base_url|https://octocat.github.io/my-repo|base_url|
|origin|https://octocat.github.io||
|host|octocat.github.io||
|base_path|/my-repo|url|

_config.yml에서 `url`과 `base_url`로 지정해주었던 부분이 들어가는 것 같다. 

꽤 놀라운 점은, 무조건 Github token을 사용한다는 것이다. 

```
token:
    description: 'GitHub token'
    default: ${{ github.token }}
    required: true
```

token은 로그인을 인증하기 위한 것이라고 알고 있는데, [여기](https://zzsza.github.io/development/2020/06/06/github-action/)에서 확인할 수 있듯이, workflow에 사용할 수 있는 한도가 있기 때문인 것으로 추정된다.

# 3. uses: actions/jekyll-build-pages@v1
jekyll이 정적 페이지를 생성해주기 때문에, 마지막으로 페이지를 build하는 과정에서 필요한 것 같다.

deploy를 살펴보자.
```
deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```

마찬가지로 [actions/deploy-pages](https://github.com/actions/deploy-pages)가 무엇인지 확인하면 동작방식을 이해할 수 있다.

배포란, 사용자가 접근할 수 있는 환경에 배치시키는 일이다. 그래서 이 작업이 실행되면 접근 가능한 page_url을 결과로 얻을 수 있다고 한다. 

배포 과정에서 Actions 탭에 들어가면, 배포가 제대로 되었는지 아닌지 확인할 수 있다. [여기](https://github.com/actions/deploy-pages/blob/main/action.yml)에서 확인할 수 있듯이 배포가 제대로 되었는지 확인하는 과정에서 `timeout`이나 `error_count`를 사용하는 것 같다.

아마 처음 시작하면서 기본 설정을 그대로 사용했던 것 같은데, 덕분에 GitPage가 어떻게 자동으로 배포되는지 원리를 알 수 있었다.

### 추가적으로 알게된 사실들
#### `bundle exec jekyll serve`의 뜻

로컬 환경에서 jekyll 서버를 열겠다는 뜻이다. 

#### build and deployment에서 deploy
개발에서의 deploy = 배포

## 소감
CI/CD는 초보 개발자인 나에겐 아직 먼 길처럼 느껴져서 이쪽에 대한 공부는 거의 하지 않았었다. 그러나 플러터 배포부터 시작해서 우연히 Github Actions까지.. 갑자기 알게 되는 것들이 생겨 신기하다. 

사실 yaml 문법도 모르고 그저 탭을 사용해서 구분한다 정도만 알고 있었다. 그동안 코드 이해하고 내 블로그에 맞게 바꾸기만 급급했는데 Github Actions같은 배포 자동화 툴도 yaml로 작성되니 yaml 문법도 제대로! 알아두는 게 좋을 것 같다.

### 참고자료
- [github 공식 docs](https://docs.github.com/ko/actions/examples/using-scripts-to-test-your-code-on-a-runner)
- [github actions 개념 참고자료1 - 개념 이해](https://www.daleseo.com/github-actions-basics/)
- [github actions 개념 참고자료2 - 자세한 이해](https://zzsza.github.io/development/2020/06/06/github-action/)