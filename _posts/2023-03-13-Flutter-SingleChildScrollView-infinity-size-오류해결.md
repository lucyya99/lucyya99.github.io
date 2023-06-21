---
layout: post
categories: flutter
tags: flutter flutter/scroll
---

# Flutter SingleChildScrollView infinity size 오류 해결
해결법을 바로 보고 싶은 분들은 *해결법 탭*으로 넘어가시면 됩니다.

## Task
1. 로그인 페이지이므로 처음 화면에서는 스크롤을 고정해야 함
2. 그러나 ID와 비밀번호를 입력할 때는 스크롤이 되어야 함. 그렇지 않으면 오버플로가 발생할 수 있음.
3. 간단한 페이지이므로 커스텀 위젯 대신 간단한 위젯을 사용하고 싶음.

## 문제점
### 1. SingleChildScroll은 child 내부에 Expanded 사용 불가
Expanded는 화면 크기를 비율로 나눠서 차지하는 위젯입니다. 스크롤 위젯과는 다르게 화면에 딱 고정시키는 역할을 합니다. 그래서 Android Studio에서는 오류를 내어 아예 사용하지 못하도록 하고 있습니다.
    
### 2. CustomScroll 위젯을 사용하고 싶지 않음
CustomScroll을 사용할 수도 있겠지만, 로그인이라는 간단한 페이지라서 CustomScroll은 사용하지 않고 싶었습니다. 또 처음 들어간 화면은 고정되어 있어야하기 때문에 스크롤을 사용하더라도 문제가 됩니다. 
    

## 해결법
### SingleChildScrollView란?
#### [기본 세팅] `physics: AlwaysScrollableScrollPhysics()`
- 컨텐츠가 화면 크기를 넘어가지 않을 때) 스크롤이 생기지 않습니다.
- 컨텐츠가 화면 크기를 넘어갈 때) 스크롤을 내려 모든 컨텐츠를 볼 수 있게 해줍니다.

#### [physics 파라미터 변경시]
1) `physics: NeverScrollableScrollPhysics()`  : 스크롤 생성 x

2) `physics: BouncingScrollPhysics` : iOS 스타일 스크롤
![Animation.gif](https://user-images.githubusercontent.com/80736490/224636350-419db1c0-37d4-4fcc-82b8-9f5eec9fe841.gif){: width="50%" height="50%"}

3) `physics: ClampingScrollPhysics` : Android 스타일 스크롤
![Animation.gif](https://user-images.githubusercontent.com/80736490/224636359-b3d8c133-6c94-4991-85c3-184a2e7be5f9.gif){: width="50%" height="50%"}

### SingleChildScrollView vs ListView
- SingleChildeScrollView : child 안에 있는 모든 컨텐츠를 렌더링
- ListView : 화면에 보이는 것만 렌더링

### 크기 무한대로 늘어나는 버그 해결
`Mediaquary.of(context).size.height` 를 사용하여 SizedBox의 height에 현재 디바이스의 높이를 지정해주면 크기가 무한대로 늘어나는 버그가 해결됩니다. 

```dart
double height = MediaQuery.of(context).size.height;

return GestureDetector(
  onTap: () => FocusManager.instance.primaryFocus?.unfocus(),
    child: Scaffold(
      body: SafeArea(
        child: SingleChildScrollView(
          child: SizedBox(
            height: height * 0.95,
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              crossAxisAlignment: CrossAxisAlignment.center,
              children: [
                _TopPart(),
                _MiddleLogin(),
                _BottomPart(),
              ],
            ),
          ),
        ),
      ),
    ),
  );
```
기본 세팅일 때 스크롤은 화면 최대 크기를 넘어가야 생성되므로 화면 크기를 넘어가지 않게 height를 설정하면 해결될 것이다라고 가정했는데 성공했습니다!

### 스크롤을 고정시키는 방법
해당 페이지의 높이를 `Mediaquary.of(context).size.height`를 사용하여 바로 지정하면, 안에 들어있는 자식 위젯의 크기에 따라 약간의 스크롤이 생깁니다.

제가 원하는 건 (1) 첫화면에서 스크롤이 생기지 않는 고정된 화면 (2) Textfield를 눌렀을 때 스크롤이 생겨 밑으로 내려볼 수 있어야 합니다.

스크롤은 높이 길이가 해당 디바이스의 크기를 벗어나기 때문에 생기는 것이므로 그냥 높이를 `height * 0.9` 혹은 `height * 0.95` 로 조금 줄여주면 해결됩니다. 

## 추가 참고문서
저는 이렇게 생각해서 오류를 해결했는데, 더 좋은 참고자료가 있어 공유합니다.

[참고자료 링크 - 09. SingleChildScrollView](https://wikidocs.net/168829)