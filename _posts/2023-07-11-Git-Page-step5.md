---
layout: post
categories: github
tags: github gitpage
title: Git Page 추가 기능 구현하기 - 공유하기 (#5)
---

## 동기

블로그에 공유하기 기능이 없어서 참고할만한 UI를 찾다가, velog의 공유하기 UI를 발견했습니다. 이걸 보고 저도 버튼을 누르면 다른 옵션이 뜨도록 만들어야겠다고 생각했습니다..!

![velog](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/30eda8e7-9ba0-4f9b-a471-128aae2719c9)

velog랑 똑같이 버튼이 왼쪽에 있었으면 했지만, 기존 테마가 반응형으로 만들어져있다보니 창이 줄어들면서 왼쪽에 있던 버튼이 이상한 곳으로 가버려서 기존 버튼의 위에 있도록 만들었습니다.

## 공유하기 버튼 추가 (UI 변경)
- 변화 체험하기

# Before
![Before](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/b5426626-36c3-43ee-854e-46af92d12b04)

# After
![After](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/55f1fbb4-8402-4cb7-be85-8e33ec65d408)

<br>

# 📢 UI 부분은 패치노트처럼 뭘 바꿨는지만 공지할테니, 나머지는 코드를 통해 확인해주세요. 정리 > 👁‍🗨 바뀐 코드 확인하기 보시면 됩니당


### 1. 반응형 웹에 맞게 버튼 크기와 위치 조절
기존 테마가 반응형 웹으로, media-query를 통해 총 3가지 버전으로 크기를 조정해주고 있었기 때문에 3가지 버전으로 전부 확인해보는 것이 필요했습니다.

기존 테마에서는 공유 버튼이 없었기 때문에 ⬆버튼은 무조건 오른쪽 밑에 위치를 고정시켜두면 되었습니다. 하지만 공유 버튼이 생기고 세 버전으로 전부 확인해보니, 버튼 사이에 빈칸이 생겨 위치를 조금씩 변경해주어야 했습니다.

이 부분은 yat 테마에서 click-to-top.scss를 조금씩 수정했기 때문에 생각보다는 어렵지 않았습니다. `position`과 `width`를 확인하면서 계속 바꾸는 약간의 디테일과 노동이 필요했습니다.

### 2. 버튼 관련 애니메이션 추가

= 버튼이 눌릴 때 진해지는 효과 + 버튼이 눌리는 듯한 효과 추가 + 버튼이 Fade-in, Fade-out되는 효과 입니다

버튼이 눌리는 효과는 `transform: translateY(2px) translateX(2px);`으로 만들 수 있습니다! 버튼 안의 아이콘이 살짝 아래로 내려가게 만들어서 버튼이 눌리는 것 같이 보입니다. 

버튼 애니메이션 효과는 `transition`과 `opacity`, `position`을 활용하여 완성해주었습니다.

`position`은 `visibility: hidden`일 때는 right과 bottom 속성을 기존 공유버튼과 똑같이, `visibility: visible`일 때는 이동하고 싶은 위치로 설정하면 됩니다!

그리고 transition과 opacity를 각각 이렇게 조정해주면, 애니메이션 완성입니다! 😊
```css
opacity: 0.5;
transition: ease-in 200ms;
```

```css
opacity: 1;
transition: ease-out 300ms;
```


### 3. 해당 버튼들은 전부 첫번째 우선순위로!
이전에는 버튼 대신 TOC가 눌렸습니다. 첫번째 우선순위를 가져 무조건 버튼이 눌릴 수 있도록 변경해주었습니다. 

z-index는 기본값이 0이기 때문에 `z-index: 1;`을 추가해주면 간단하게 해결됩니다

### 4. 스낵바 추가
링크 복사에 대한 피드백이 없어서 추가했습니다. 노트북에서 확인하다보니 피드백이 없는 것이 허전해서 추가했는데, 알고보니 안드로이드 환경에서는 복사되면 자동으로 스낵바에 뜨도록 되어 있었습니다. 그래서 휴대폰에서는 중복되어 나타나긴하지만, 일단 표시해주었습니다

스낵바는 [예제 코드](https://www.w3schools.com/howto/howto_js_snackbar.asp)를 이용하여 만들었습니다

## 클립보드에 링크 복사하기

### 코드 설명
현재 deprecated 되었다는 코드이지만, 밑에서 설명할 이유로 인해 어쩔 수 없이 사용하였습니다.

```javascript
    share.addEventListener('click', () => {
    // click시 내 링크 클립보드로 복사하는 코드
    var text = window.location.href;
 
    // 1. input 태그 생성
    var dummy = document.createElement('input')
    document.body.appendChild(dummy);

    // 2. 태그 값을 링크주소로 설정
    dummy.value = text;

    // 3. 태그 내 값을 복사하는 기능 사용
    dummy.select();
    var success = document.execCommand('copy');
    
    // 4. 필요없어진 태그 삭제
    document.body.removeChild(dummy);
  });
```

1. 쓰레기(더미) 태그를 하나 생성한다
2. 쓰레기 태그에 내가 복사하고 싶은 값을 넣는다
3. 해당 태그의 복사 기능을 사용한다
4. 쓰레기 태그를 삭제하여 중간 코드 과정을 밖으로 나타내지 않는다


clipboard api를 사용하는 코드는 조금 더 간결합니다.
```js
window.navigator.userAgent.toLowerCase();
```

### 왜 deprecated된 document.execCommand('copy') 코드를 사용하였는가?

카카오톡 공유하기 기능을 넣으면서 카카오톡 웹뷰에서도 해당 기능이 잘 동작하는지 확인해봤는데 복사가 안됐습니다. 😭

[카카오 개발자님의 답변](https://devtalk.kakao.com/t/topic/115766/2)을 확인해보면, 카카오톡뿐만 아니라 어플리케이션 내에서 웹뷰를 사용하는 경우, clipboard api를 사용하면 작동하지 않을 수 있다고 합니다.

이러한 이유로 브라우저에 따라 execCommand 혹은 Clipboard api를 골라 사용하는 것도 생각해봤는데, 모바일 환경에서 크롬을 사용할때도 Clipboard API가 동작하지 않아서 그냥 전체적으로 deprecated된 코드를 사용하기로 하였습니다. (더 잘 아는 분이 계시다면 댓글 부탁드립니다 🙏)

결론적으론 제가 테스트해 본 곳에서 전부 동작하는 deprecated된 코드를 사용하게 되었습니다.

다른 분이 작성하신 [공유하기 최종본](https://velog.io/@otterji/navigation.share-copyClipboard)에서는 각 환경에 네이티브한 Web Share API > 안되면 ClipBoard API > 안되면 Deprecated API를 사용해서 해결하신 것 같습니다

## 카카오톡 공유하기

### 대략적인 설명

카카오톡에서 제공하는 공유하기 API는 2가지로 카카오톡 공유 API와 카카오톡 메세지 API가 있습니다. 저희는 친구 목록을 따로 만들지 않아도 동작하는 **카카오톡 공유 API**를 사용할 예정입니다. 이와 관련한 정보는 [카카오톡 공유 이해하기](https://developers.kakao.com/docs/latest/ko/message/common#intro)를 참고해주세요

API 종류를 선택했다면, js 코드를 통해 실제로 공유하기 기능을 넣을 차례입니다. 친절하게도 카카오에서는 [카카오 개발자 - 카카오 공유 데모](https://developers.kakao.com/tool/demo/message/kakaolink?message_type=custom)를 통해 **두 가지 옵션**을 선택하면, **데모 코드**를 제공해줍니다.

![카카오톡 공유 데모](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/a988bad1-6648-4eb5-8110-3b472a6ebb7c)

**1. 버튼 커스텀 여부** : 공유하기 버튼을 추가하고 메세지 보내기 / 직접 만든 버튼으로 메시지 보내기

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/a1e02777-c20c-4c4b-8ef6-4e38a85f45b6" width="30%" alt="커스텀버튼">

분홍색 박스 안에 보이는 버튼을 커스텀할지에 대한 부분입니다

**2. 공유 서식** : 기본 메세지 / 스크랩 메세지 / 사용자 정의 메세지

<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/2d5a3c35-50fd-49e6-a80a-4ee0cd9ce3de" width="40%" alt="템플릿공유">

실제로 카카오톡 방에서 공유된 메세지가 어떻게 보일지에 대한 부분입니다.

위의 예시는 [직접 만든 버튼으로 메시지 보내기/스크랩 메세지]를 선택해서 넣었습니다. 저는 블로그 대표 이미지가 들어가지 않고 **글 제목과 내용만 깔끔하게 들어갔으면 좋겠**어서 [직접 만든 버튼으로 메시지 보내기/사용자 정의 메세지]를 선택해서 진행했습니다.

### 참고글 따라하기
우선 [참고글](https://seungwubaek.github.io/blog/share_on_kakao/)에서 7번까지 과정을 따라해줍니다. 

참고글 7번 이후로는 카카오톡 버튼을 커스텀하는 과정이나, 카카오톡 sdk 사용범위 제한, 공유하기 버튼 넣는 코드가 있습니다. 제 블로그는 HOME, ARCHIVES, TAGS 탭, 즉 3가지 페이지 외에는 전부 공유하기 버튼이 삽입될 예정이라 굳이 사용범위를 제한하는 코드는 넣지 않았습니다.

### 버튼 커스텀 + 템플릿 사용

# 결과
<img src="https://github.com/lucyya99/lucyya99.github.io/assets/80736490/621ae78b-c031-47f4-8919-3e2be2784741" width="40%" alt="공유결과">

# 1. 버튼 커스텀

버튼은 커스텀한다기보다는 카카오에서 제공하는 이미지를 사용해서 이슈에 붙여넣어 사용했습니다. 하지만 js로 나중에 버튼을 만드는 것보다는 미리 이미지로 넣는게 더 좋을 것 같아 이렇게 만들었습니다.

```html
<a id="kakao-share" class="share-small-button kakao" href="javascript:scrapKakao()">
    <img src="{이미지링크}" width="24px">
</a>
```

이미지는 [여기](https://developers.kakao.com/tool/resource/talk)에서 다운받을 수 있습니다.

# 2. 템플릿 사용

이 코드는 post.html 가장 위에 넣어야합니다.
```javascript
<script>
  Kakao.init([Javascript 키]); // 이거 안보이도록 해야됨
</script>
```
Javascript 키는 [요약정보 > 앱키 > javascript 키]에서 확인할 수 있습니다

참고글을 잘 따라왔다면, 템플릿을 만들 때 3가지 변수를 사용했을 것입니다. title, description, pagePathname인데, 저는 다음과 같이 설정해주었습니다.
```javascript
<script>
  // 카카오톡 공유
  var content30 = document.getElementsByClassName("post-content")[0].textContent.substr(0, 30);
  function scrapKakao() {
    Kakao.Share.sendCustom({
      templateId: [템플릿 id],
      templateArgs: {
        title: document.title,
        description: content30,
        pagePathname: location.pathname.substr(1)
      },
    });
  }
</script>
```

- `description: content30` : 현재 테마에서는 `post-content`부분에 블로그 내용이 포함되도록 되어있습니다. 너무 많은 문자를 보내지 못하도록 카카오톡에서 막아두었기 때문에 블로그 내용 중 30자만 보냅니다.

- `pagePathname: location.pathname.substr(1)` : `location.pathname`은 도메인 뒤의 url을 의미하는데, 맨 앞 부분에 `/`가 포함되어 있어서 url이 합쳐지면 이상한 url이 되어 첫번째 문자를 없애 주었습니다.
    - before : `lucyya99.github.io/` + `/sub.html` = `lucyya99.github.io//sub.html`
    - after : `lucyya99.github.io/` + `sub.html` = `lucyya99.github.io/sub.html`


# 3. 테스트
Javascript Key를 일단 넣어서 테스트 해봅니다. 성공이면 카카오톡 로그인 화면이 뜹니다!

### ⭐ Javascript Key는 노출하지 말자!

![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/9054943e-beca-4867-a21a-1862eceaf069)

키가 노출되면 재발급받아 사용하라는 경고 문구에 Javascript Key가 유출되는 것을 막고 싶었습니다 😱

다른 블로그글을 보니 노출시킨 곳도 많은 것 같아서 어떻게 해야하나 고민하다가 프론트단에서 막을 수 있는 만큼 막아보기로 했습니다!

이 부분은 [Secrets 설정으로 앱 키 업로드 막기]()에서 다루겠습니다!

## 정리

### 소감

참고글들을 읽고 그대로 복붙하다가 시간이 오래걸렸습니다......ㅠㅠㅠㅠ 역시 복붙은 악마의 유혹이네요..

카카오톡 메세지가 버전이 업그레이드되면서 함수명인 `Kakao.Link.Scrap()`이 `Kakao.Share.Scrap()`으로 변환된 모양입니다.

![](https://github.com/lucyya99/lucyya99.github.io/assets/80736490/7c237d4c-0f79-4a7e-9030-4147f14f21d3)

카카오에서는 친절하게 설명해주었는데, 차근차근 읽어볼걸 그랬네요.. 아무튼 공유하기 기능을 추가해서 기쁩니다 🤗

### 👁‍🗨 바뀐 코드 확인하기
- [_includes/custom-head.html](https://github.com/lucyya99/lucyya99.github.io/blob/main/_includes/custom-head.html) 코드 변경
- [_layouts/post.html](https://github.com/lucyya99/lucyya99.github.io/blob/main/_layouts/post.html) 코드 변경
- [_sass/misc/alpha-function.scss](https://github.com/lucyya99/lucyya99.github.io/blob/main/_sass/misc/alpha-function.scss) 코드 추가

### 참고 link

#### 링크복사 & 스낵바
- [링크복사 참고글](https://curryyou.tistory.com/480)
- [카카오 개발자님의 답변](https://devtalk.kakao.com/t/topic/115766/2)
- [dummy 생성 후 클립보드 복사](https://stackoverflow.com/questions/49618618/copy-current-url-to-clipboard)
- [deprecated된 함수 사용해도 문제가 없을까?](https://web.dev/async-clipboard/)
- [snackbar 만들기 참고글](https://www.w3schools.com/howto/howto_js_snackbar.asp)
- [공유하기 최종본](https://velog.io/@otterji/navigation.share-copyClipboard)

#### 카카오 공유하기
- [공유하기 참고글](https://abangpa1ace.tistory.com/255)
- [카카오 개발자 - 카카오 공유 가이드](https://developers.kakao.com/docs/latest/ko/message/js-link#custom-template-msg-custom)
- [카카오 개발자 - 카카오 공유 데모](https://developers.kakao.com/tool/demo/message/kakaolink?message_type=custom)
- [카카오톡 공유하기 참고글](https://seungwubaek.github.io/blog/share_on_kakao/)
- [카카오톡 공유하기 참고글2](https://pozafly.github.io/blog/jekyll-kakao-share-button/)