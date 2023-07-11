---
layout: post
categories: github
tags: github gitpage
title: Git Page 글 작성하기 (#3)
---

## 1. Markdown이란?

Markdown이란 웹에서 문서를 더 간단하게 작성하기 위해 만들어진 언어입니다. html을 몰라도 Markdown 문법만 익혀 문서를 작성할 수 있다는 장점이 있습니다. 하지만 html을 안다면 문법을 조금 더 쉽게 이해할 수 있습니다

## 2. 글을 작성하기 위한 필수 Markdown 문법

Markdown 언어는 html에 비해 괄호를 작성하는 과정이 줄어들어 보다 편하게 글을 작성할 수 있습니다. 
Markdown 문법으로 표, 수식, 선, 인용 등등을 표시할 수 있지만, 제목, 목록, 코드, 링크와 같은 기본적인 것들만 준비했습니다
### 2-1. 제목(Header) : ## 부터

html의 h1부터 h6 태그를 Markdown에서는 #의 개수로 나타냅니다. 

예를 들어, `<h1>큰 제목</h1>` 은 `# 큰 제목`으로 표시합니다. 

yat 테마에서는 #이 너무 작고 목차에도 나타나지 않아, 제목은 ## 부터 사용하는 것을 추천합니다! 이와 관련해서는 css 파일을 이용하여 직접 커스텀할수도 있습니다

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/3d116177-8ecc-475f-82af-835b0b8eb816" width="70%">

작성된 예시를 이미지로 캡쳐해서 넣긴했는데, 이건 직접 작성하여 확인해보시는 것을 추천드립니다.

TOC는 Table Of Content의 약자로, h태그(#)를 기준으로 자동으로 목차를 만듭니다. 제목을 클릭하면 해당 제목으로 이동하는 링크 기능도 있습니다. 제 GitPage 오른쪽에 있는 Sub Titles도 TOC로 만들어졌습니다. 이처럼 TOC를 생성하는 기능이 적용된 페이지에서는 제목을 달아주면 목차를 자동으로 생성합니다!

### 2-2. 목록
숫자로된 목록(<ol>)과 문자로된 목록(<ul>)을 간단하게 작성할 수 있습니다.

#### 숫자로된 목록 (ordered list)
`1. `, `2. `, ... 으로 작성할 수 있으며, 탭을 하면 하위 목록을 작성할 수 있습니다.
1. 과일
    1. 바나나
    2. 딸기
    3. 사과
2. 채소

#### 문자로된 목록 (unordered list)
`- `, `+ `, `* `로 작성할 수 있습니다. 셋 중 어떤 문자를 사용해도 같은 문자로 나타납니다.
- `- `로 표시한 첫번째 상위 list
    + 첫번째 하위 list
        * 첫번째 하위 list의 하위 list

+ `+ `로 표시한 두번째 상위 list


### 2-3. 링크
링크는 `[링크를 표시할 텍스트](링크)`로 나타낼 수 있습니다. [여기](https://lucyya99.github.io/github/2023/06/24/Git-Page-step3.html#h-2-3-%EB%A7%81%ED%81%AC)를 누르면 2-3번 링크로 이동하는 것과 같이 현재 페이지 내에서도 이동할 수 있습니다

### 2-4. 이미지

이미지도 링크와 비슷한 문법으로 나타낼 수 있습니다. `![이미지를 가져올 수 없는 경우 나타낼 텍스트](이미지위치 혹은 링크)`로 나타낼 수 있습니다.

이미지 크기를 조절하려면, 이미지 태그를 직접 사용하면 됩니다. `<img src="이미지 위치/링크" width="10%">`와 같이 조절할 수 있습니다. 밑의 예시는 원본 이미지를 10%, 20%로 나타낸 모습입니다.

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/6cd79577-fabd-4694-ad84-035b267d7f6a" width="10%"> <img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/6cd79577-fabd-4694-ad84-035b267d7f6a" width="20%">

yat 테마에서는 이미지가 한 행을 전부 차지하고, 이미지를 행의 가운데에 위치하도록 합니다.


#### 이미지 Github issue에 올려서 사용하기!
# 📢 커스텀 도메인을 사용하지 않는 경우, 이미지는 경로에서 오류가 발생할 가능성이 있습니다. 따라서 저는 Github issue에 올려서 사용합니다!

보통 Github issue는 변경이 필요한 사항들을 작성하는 용도로 사용합니다. 여러명이 참여한 레포지토리의 경우, 자유롭게 답글을 달아 소통할 수 있습니다. 그리고 변경이 완료되면 이슈를 닫습니다.

lucyya99.github.io 레포지토리는 블로그 작성을 위한 것이니, 이미지를 올리기 위해 이슈를 생성하겠습니다.

# 1. 자신의 블로그를 연결한 레포지토리로 이동하여 이슈를 생성합니다.

![issue 생성하는법](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/a97fdc96-a381-4625-b730-045c44bd5b0d)

# 2. 제목과 내용을 입력하여 생성을 완료합니다.

![issue 생성하는법2](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/2f7b643c-1fb3-4c29-89ea-1dd63fd12bc5)

# 3. comment에 이미지를 drag&drop으로 올리고, 링크를 복사합니다. comment를 눌러 이슈에 새로운 글을 추가합니다.
![이미지업로드](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/2dbd9d30-b79f-42b2-9d42-aae9959c7b97)

# 4. `![텍스트](이미지링크)`에서 이미지링크 부분에 복사한 링크를 붙여넣어 원하는 곳에 이미지 업로드 완료!
이제 이미지 링크를 얻었으니, 원하는 곳에 넣어주면 끝입니다..! 사실 1번~3번은 이미지 링크를 얻기 위한 작업입니다. 솔직히 복잡하고 귀찮긴 한데, 이미지 경로 관련한 오류를 해결할 수 있어 좋습니다

저는 [링크](https://github.com/lucyya99/lucyya99.github.io/issues/2)와 같은 방식으로 gitpage에 대한 글에 관련된 이미지를 전부 같은 이슈에 업로드했습니다. 카테고리에 작성할 글을 전부 작성한 경우, 이슈를 닫아 comment가 더 작성되는 것을 막을 수도 있습니다.

그리고 한가지 더 주의할 점은, **로컬에서 같은 이름으로 저장했던 이미지를 수정해서 올리는 경우, 이미지가 수정되지 않는 버그**가 있습니다. 이슈에서 이미지링크를 생성할 때, 로컬에 저장된 이미지 이름을 사용하기 때문에 발생합니다. 이 경우 이슈에서 수정되지 않는 `![]()` 부분을 삭제한 후 다시 올려주면 해결되지만, **애초에 오류가 나지 않도록 하기 위해 이름을 다른 걸로 지정해줍시다.**

### 2-5. 볼드체
**가나다**처럼 사용하고 싶을때, `**강조를 원하는 텍스트**`와 같이 작성하면 됩니다!

### 끝!

코드는 밑에서 다룰 예정이고, 이외의 Markdown 문법은 필요할 때마다 검색해서 사용하면 됩니당 🤗

## 3. 코드 공유

저는 블로그를 작성하며 짧은 코드는 마크다운 언어를 이용하고, 중간 길이와 강조가 필요한 코드는 이미지를 이용하고, 긴 코드는 github gist로 공유하는 것으로 정했습니다.

### 3-1. Markdown으로 코드 보여주기

짧은 코드는 \`{나는 짧은 코드}\` 처럼 코드를 \`  \`로 감싸줍니다. `int v = 3;`과 같이 나타납니다.

처음에는 \`가 어떤 키인지 헷갈릴 수 있습니다. 키보드에서 ESC 바로 밑에 있고, 숫자 1 왼쪽에 있는 버튼을 누르면 됩니다. 

중간길이 코드는 다음과 같이 작성합니다. 첫번째 ```옆에 언어 이름을 써주면 해당 언어 문법에 맞게 색상이 바뀝니다. 이를 Syntax highlighting이라고 합니다.

\`\`\`{언어이름}

{나는 중간 길이 코드}

\`\`\`

예시입니다

```dart
void main() {  
    playAllStream().listen(
        (val){    print(val);  
        }
    );
}
```

# 📢 `{ %- include -% }`와 같이 html에서 사용하는 문법인 경우, 실제 코드가 삽입되어 굉장히 난감한 경우가 있습니다. 이는 이미지로 삽입하는 것을 추천합니다!

### 3-2 이미지로 코드 보여주기

저는 개인적으로 이미지로 코드를 공유하는 것을 선호하지 않습니다.. 그러나 이미지로 코드를 보여주어야하는 경우가 있습니다. 

이미지로 보여주는 것이 직관적으로 보이는 경우, 위에서처럼 html로 작성되어 이미지로 보여주지 않으면 정확한 코드를 공유할 수 없는 경우, 중간 정도의 길이라서 github gist로 공유하기엔 애매한 길이인 경우가 있습니다. 저는 이런 경우에만 이미지로 코드를 공유합니다

코드를 이미지로 보여주는 것은 vs code의 플러그인인 polacode를 이용합니다. 



# 1. Polacode-2022 설치
![Polacode 설치](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/babea6de-957e-4dcd-ae64-b49eed3d38e3)

제가 설치해보니 Polacode-2022를 설치해야 실행이 되더라구요. Polacode-2022로 설치해줍니다.

# 2. vs code를 재실행합니다

# 3. Ctrl+Shift+P 혹은 우클릭 > Command Palette에서 Polacode를 검색합니다.
<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/1177a616-bb31-4b75-a566-203ce3506e9d">

# 4. 이미지로 만들 코드를 드래그, 커스텀 후 저장
![Polacode 설명](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/9c874c86-bb4c-4a04-8aa9-28efa75f2c2d)

①번처럼 코드를 드래그해도 오른쪽 Polacode 탭에서 바뀌지 않는 경우가 있습니다. 이때는 vs code를 재실행(2번)한 후, Polacode를 다시 실행(3번)해주면 됩니다.

배경색과 그림자 넣을지 여부를 커스텀할 수 있습니다. 저는 기본으로 선택해주었습니다.

# 5. 저장된 이미지
![저장된 이미지](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/95602341-4003-4247-8b56-6731e00538bb)

이외에도 [소스코드 이미지 넣기](https://velog.io/@yeseolee/%EC%86%8C%EC%8A%A4%EC%BD%94%EB%93%9C%EB%A5%BC-%EB%B8%94%EB%A1%9C%EA%B7%B8%EC%97%90-%EC%98%AC%EB%A6%B4%EB%95%8C)를 참조하면, 다른 방식으로도 코드를 이미지로 넣을 수 있습니다.


### Github gist로 코드 보여주기
바로 본론으로 들어가겠습니다

# 1. 새로운 gist 생성
![gist 생성](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/797d1a86-1fcf-4973-a34d-46d0f328c7e2)

# 2. 코드 내용 작성
![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/e2e3f8ea-9e25-4f0b-af3a-e671c6210101)

secret으로 생성하면 검색 엔진에 올라가지 않는다는 차이만 있고, 정상적으로 공유가 되므로 secret으로 생성해줍니다!

# 3. 공유 방식 선택하여 업로드
![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/ddba6fd7-3399-4727-88fe-22044520394e)

# Embed 방식
<script src="https://gist.github.com/lucyya99/d465e0b93415019ffc9aadb55dfa36ea.js"></script>

# Link 방식
- [gist 링크](https://gist.github.com/lucyya99/d465e0b93415019ffc9aadb55dfa36ea)입니다

# Github gist에 대한 추가적인 사실

- 편집 버튼을 눌러 여러 파일을 올릴 수도 있습니다.
- 코드 전체를 다운받을 수 있습니다.

# 📢 Embed 방식을 사용했을 때 너무 긴 코드면 코드 전체가 보이기 때문에 글이 길어보일 수 있습니다. 둘 중 용도에 맞게 사용해주세요


## 정리
지금까지 필수 Markdown 문법, 이미지를 넣을 때 issue를 사용하는 법, 코드를 넣는 3가지 방법에 대해 정리해보았습니다!

### 소감

참조했던 여러 글을 모아모아 지금까지 Gitpage를 작성하며 필요했던 것들을 정리해보았습니다. 글이 너무 긴 것 같아 읽는 분들이 힘드실수도 있겠다는 생각이 드네요... 이 글은 링크를 저장해두고 필요한 부분만 보는 것을 추천드립니다!!

### link
- [TOC 설명](https://kyeoneee.tistory.com/56)
- [소스코드 이미지 넣기](https://velog.io/@yeseolee/%EC%86%8C%EC%8A%A4%EC%BD%94%EB%93%9C%EB%A5%BC-%EB%B8%94%EB%A1%9C%EA%B7%B8%EC%97%90-%EC%98%AC%EB%A6%B4%EB%95%8C)
- [github gist 사용법](https://brunch.co.kr/@mystoryg/146)


- [이미지 관련 이슈](https://github.com/lucyya99/lucyya99.github.io/issues/2)
- [작성된 gist 예시](https://gist.github.com/lucyya99/d465e0b93415019ffc9aadb55dfa36ea)