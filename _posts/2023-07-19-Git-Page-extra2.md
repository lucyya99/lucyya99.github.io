---
layout: post
categories: github
tags: github gitpage
title: Git Page - Secrets 설정으로 앱 키 업로드 임시방편으로 막기 (#998)
---

## 💭 문제의식

[Git Page 추가 기능 구현하기 - 공유하기 (#5)편]()에서 카카오톡 공유 기능을 위해 카카오톡 앱 키가 필요한데, 이 앱 키가 노출되지 않도록 하고 싶었습니다

## 고민과 타협

javascript는 client단에 있는 코드라서 애초에 숨길수가 없습니다

근데 일단 서버없이 돌리고 싶어서 github에 올라가는것이라도 막기 위해 페이지가 빌드될 때 앱 키를 포함시키기로 결정했습니다

> 아직 프론트단 공부가 끝나지 않아서 서버단은 천천히 해볼 예정. 미래의 내가 업데이트 하겠지?..

## 🚩 목표

`_layouts/post.html`에 진짜 키 대신 `site.kakao_javascript_key`를 넣어서 직접적으로 key가 드러나지 않도록 만들기!

조금 더 구체적으로는 Jekyll이 페이지 빌드하기 전에 yaml 파일에 변수를 추가해서 `_layouts/post.html`에서도 해당 변수를 사용할 수 있게 하는 것!

대신 빌드하는 타이밍을 알아야하기 때문에 Github Actions를 사용해야하는데, Github Actions에 대한 개념은 나중에 살펴보도록 하고 본문에서는 방법만 소개할 예정입니다

## 본격적인 시작

### 1. Secret을 만든다

Github settings > Secretes and Variables > Actions > New Repository secret

![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/538d905c-3f7d-4857-bd02-e58583a16200)

![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/b5163af3-48a9-4834-a6f3-08a47769c202)

분홍색 네모 부분에 복사한 javascript key를 그대로 넣어주면 됩니다 (예시는 카카오톡 SDK 데모에 있는 앱 키입니다)

### 2. Actions 중 GitHub Pages Jekyll을 클릭해서 workflow를 새로 만들어준다

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/479be3b2-3fd3-47fe-bbcb-4e83f43d1d65" width="50%">

![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/14ed386b-4b5f-4747-adb1-387b712c2905)

![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/ccdb6c2a-9976-48b2-b23e-87cec6eea387)

여기에서 Actions 탭을 클릭해 에러안나는지 확인 & workflow에 추가되었는지 확인합니다

![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/ceaca2fd-06b1-4e5f-9b76-398ae248a682)

### 3. Jekyll이 페이지 빌드하는 부분 위에 해당코드를 넣어줍니다

새로 만든 workflow는 .github/workflow 폴더 밑에 생성된 yaml 파일에 적혀있습니다. 이 파일을 수정해줍니다

- 이 부분 추가

```yaml
- name: Update values.yaml
  uses: fjogeleit/yaml-update-action@main
    with:
      valueFile: '_config.yml'
      propertyPath: 'kakao_javascript_key'
      value: ${{secrets.KAKAO_JAVASCRIPT_KEY}}
      commitChange: false
```
yaml 문법은 들여쓰기를 엄격하게 보기 때문에 줄 맞추기를 잘 해주어야 합니다! [여기](https://github.com/lucyya99/lucyya99.github.io/blob/main/.github/workflows/jekyll-gh-pages.yml)에서 전체 코드를 확인할 수 있습니다

해당 코드는 yaml 파일을 생성 혹은 업데이트 해줍니다. 

- `valueFile: '_config.yml'` : 업데이트할 파일명
- `propertyPath: 'kakao_javascript_key'` : 변수명 -> site.???로 사용가능
- `value: ${{secrets.KAKAO_JAVASCRIPT_KEY}}` : 아까 secrets에 등록한 값
- `commitChange: false` : commit하게 되면 지금까지 깃허브에 올라가지 않도록 작업한 것들이 무용지물이 되므로 기본 설정 중 commit만 false로 설정해줍니다

해당 Github Action에 대해 자세히 알고싶다면 [여기](https://github.com/marketplace/actions/yaml-update-action)를 참고해주세요

### 4. `_layouts/post.html`에서 Kakao.init 부분 수정

```html
<script>
  var kakao = '{ { site.kakao_javascript_key } }'
  Kakao.init(kakao);
</script>
```

### 5. 결과

깃허브 코드상으로는 전혀 secret 값이 무엇인지 알 수 없습니다!

하지만 F12로 본다면..

![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/7197b076-6a71-403e-9e64-0fb85ec4fa4d)

다 보이는 것을 알 수 있습니다.. 😭

### 6. F12, 우클릭 막기

끝인줄 아셨나요..?! 저도 끝이라고 생각했어요

<script src="https://gist.github.com/lucyya99/933d416ed0b47ade1442a63c5f06c817.js"></script>

그렇다면.. 개발자 모드로 진입하는 것을 막으면 되지 않을까해서 찾아보니 다행히 코드가 있었습니다! 🤗 이걸로 Keydown 이벤트로 개발자 모드로 진입하는 것까지는 막을 수 있습니다

이 방법이 완전하지는 않지만, 되는 곳까지는 막아보았습니다 😭

## 정리

### 소감

F12로 계속 디버깅해보니까 _config.yml에 정의해둔 변수의 값이 바뀌지 않는게 이상했습니다. _config.yml을 수정하는 Action을 마켓플레이스에서 찾아서 겨우 성공할 수 있었습니다..!

처음으로 ChatGPT한테 의뢰하면서 해결해보았는데, 정말 도움되지 않았습니다.. 개인적으로 ChatGPT는 이미 만들어진 것들을 응용하는 것보다는 기초 문법 까먹었을 때나 코드 리뷰할 때 의뢰하는게 좋은 것 같아요

처음에는 yaml 파일을 수정하는게 아니라 env 파일을 만들어서 그 파일에 있는 것들을 사용하고 싶었는데, 이것도 서버가 존재해야 가능한 모양입니다.. 언젠가는 저의 서버를 이용해보겠습니다!!

솔직히 서버를 파서 하는게 가장 깔끔하고 노출도 안되는 방법일텐데 이렇게까지 해야되나 싶지만.. 일단 어떻게든 해결했으니 뿌듯하네요 😖

### 참고 link

#### Github Secrets
- [가장 도움됐던 글](https://stackoverflow.com/questions/76128023/how-do-i-pass-a-github-secret-into-kubernetes-yaml-files-using-github-actions-wo)
- [yaml-update-action](https://github.com/marketplace/actions/yaml-update-action)
- [secrets 관련 글](https://ji5485.github.io/post/2021-06-26/create-env-with-github-actions-secrets/)

#### F12, 우클릭 방지
- [F12, 우클릭 방지 참고글1](https://stackoverflow.com/questions/28575722/how-can-i-block-f12-keyboard-key-in-jquery-for-all-my-pages-and-elements)
- [F12, 우클릭 방지 참고글2](https://www.cluemediator.com/disable-right-click-and-f12-key-using-javascript)