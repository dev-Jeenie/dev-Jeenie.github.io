---
title: "앱 만들기 끝판왕! 스토어 등록 💜 2. ios(2)"
permalink: /cs/StoreForIos2
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-12-05
last_modified_at: 2021-12-05
---

![]()


React native로 개발한 앱을 스토어에 등록하려고 한다. android 버전과 ios 버전이 있기 때문에, 각각 google play store와 App store에 등록하는 과정을 기록한다.

# 그에 앞선 배경지식

App에는 release 버전과 debug 버전이 있다.

- Debug
  - 개발할 때 사용하는, 디버그 정보가 포함되어있는 apk 파일로 스토어에 등록할 수 `없다`

- Release
  - 용량이 줄어들고, `최적화` 된 apk 파일로 스토어에 올릴 수 `있다`

=> 바로 이 **Release 버전으로 `컴파일`**을 해야한다.




# 2. `ios` 버전 - App store







android App을 google play store에 등록하기 위해서는,<br/>
우선 `안드로이드 개발자 등록`(구글 플레이 개발자 등록)이 필요하다.
(당연하게도 필요한 구글 계정을 미리 준비하자)

## 1. 개발자 계정 등록하기 ✨

- 구글 플레이 콘솔에 접속한다.<br/>
https://play.google.com/console/about/

개발자 계정이 없다면, 아래와 같은 화면이 뜰 것이다.
<img src="/assets/images/1-create-developer-account-page.png" /><br/>
필요에 따라, 개인 / 조직 또는 비즈니스에서 시작하기를 누른다.<br/>

<img src="/assets/images/1-create-step1-1.png" /><br/>
<img src="/assets/images/1-create-step1-3.png" /><br/>
정보제공에서 개발자 이름, 담당자 이름, 연락처와 이메일, 주소, 웹사이트 주소 등을 입력한다.<br/>
입력을 완료하고, 계정 생성 및 결제버튼을 누른다.


<img src="/assets/images/1-pay-1.png" /><br/>

안드로이드 개발자 등록은 ios 개발자 등록과 마찬가지로 `등록 수수료가 발생`한다.<br/>
(미화 25달러, 한화로 현재기준 약 3만 216원)<br/>
마스터카드로 결제를 완료한다.

<img src="/assets/images/1-pay-2.png" /><br/>
결제를 완료하면 개발자 계정 생성이 완료된다.<br/>
나는 이제 언제든지 앱을 등록할 수 있는 개발자다!!<br/>
Play Console로 이동!


## 2. Play Console에서 앱 만들기 ✨


<img src="/assets/images/1-create-finish.png" /><br/>
Play Console로 이동하면 이런 화면이 나타난다.<br/>
앱만들기를 누른다.

<img src="/assets/images/2-create-app-1.png" /><br/>
앱 세부정보를 입력한다.<br/>
<img src="/assets/images/2-create-app-2.png" /><br/>
체크박스를 모두 체크한 뒤 앱만들기를 클릭한다.<br/>
<img src="/assets/images/2-create-app-finish.png" /><br/>
대시보드가 나타난다. 스크롤을 내려 앱설정을 보면<br/>
<img src="/assets/images/3-app-setting-todo-list.png" /><br/>
할일보기를 누르면, 해야할 일들의 목록이 나타난다. 하나하나 처리해주자.<br/>
<img src="/assets/images/3-app-setting-todo-list-step1.png" /><br/>
앱 액세스 권한 설정을 저장하고 대시보드로 돌아오면<br/>
<img src="/assets/images/3-app-setting-todo-list-step1-done-returnto-dashboard.png" /><br/>
진행도가 올라가있다! 이런식으로 하나하나 처리해주자.<br/>
광고, 콘텐츠 등급, 타겟층, 뉴스 앱, 코로나 19 접촉자 추적 앱 및 검사 결과 공유 앱등의 정보는 선택만 하면 넘길 수 있어서 기술하지 않았다.<br/>

- 데이터 보안 - 개인정보처리방침

<img src="/assets/images/3-personal-info-1.png" /><br/>
개인정보처리방침은 https://www.privacy.go.kr/a3sc/per/inf/perInfStep01.do에서 만들 수 있다.
<img src="/assets/images/3-personal-info-2.png" /><br/>
선택하지 않고 그냥 넘어갔다.
<img src="/assets/images/3-personal-info-3.png" /><br/>
개인정보 처리의 보유기간,
<img src="/assets/images/3-personal-info-4.png" /><br/>
개인정보 처리의 목적 등을 작성하고
<img src="/assets/images/3-personal-info-5.png" /><br/>
기타 여러 항목들을 작성하면 된다.
<img src="/assets/images/3-personal-info-6.png" /><br/>
대부분 빈칸인채로도 다음 버튼을 누를 수 있었다.
<img src="/assets/images/3-personal-info-7.png" /><br/>
<img src="/assets/images/3-personal-info-8.png" /><br/>
개인정보 필수항목 선택은 아래와 같이 이메일, 휴대전화번호, ID 비밀번호, 이름 정도만 체크하고 저장했다.
<img src="/assets/images/3-personal-info-9.png" /><br/>
<img src="/assets/images/3-personal-info-10.png" /><br/>
안정성 확보조치와 보호책임자 작성을 마치면
<img src="/assets/images/3-personal-info-finish.png" /><br/>

이렇게 처음에 입력했던 기관명으로 html 파일이 만들어진다. <br/>
다운로드를 누르고 해당 파일을 서버에 올리면 된다.( 나는 테스트용으로 만든 것이기 때문에 그냥 이 블로그 url을 올렸다.) <br/>

다시 play console의 데이터 보안 - 개인정보처리방침로 돌아와서 <br/>
url자리에 해당 개인정보처리방침이 올라가 있는 url을 입력하면 데이터 보안단계까지 완료된다! <br/>


- 스토어 등록 정보 설정


이미지 등록하는게 굉장히 불편하다.<br/>
보통 이렇게 사진을 등록하는 사이트는, 이미지를 올리면 자동으로 크기를 조절하거나 잘라서 업로드를 해주는데...<br/>
여기서는 내가 하나하나 사이즈를 다 조절해서 넣어야한다. 진짜 완전 불편함!!!<br/>
맥이 처음인 나는 이미지 조절하는게 굉장히 힘들어서 끙끙대다 앱 아이콘 이미지를 만들어주는 사이트를 발견했는데, 굉장히 유용하다.<br/>
<img src="/assets/images/4-appiconmaker.png" /><br/>
https://appiconmaker.co/ <br/>



<img src="/assets/images/4-graphic-image.png" /><br/>

여기서 말하는 그래픽 이미지란 스토어에 표시되는 것이 아닌, <br/>
플레이 스토어 출시 링크를 공유할 때 페이지 링크의 썸네일 이미지로 표시되는 것을 말한다.<br/>

앱 아이콘은 그렇다쳐도, <br/>
1024px X 500px의 그래픽 이미지는 어떻게 넣어야하지 고민을 했다.<br/>
역시나 맥이 처음인 나는 기본적으로 제공하는 응용 프로그램 `미리보기`를 이렇게 유용하게 쓸 수 있는지 몰랐다!<br/>
<img src="/assets/images/4-mac-thumbnail.png" /><br/>

저 `마크업 도구 막대 보기`를 누르면 사진 크기를 조절할 수 있는 편집모드가 된다. 사진 크기를 조절하면 간단하게 등록할 수 있다.
나는 이걸 몰라서 사진 때문에 시간을 엄청 썼다😭

<img src="/assets/images/4-screenshot.png" /><br/>
다음으로 휴대전화 스크린샷.<br/>
320px ~ 3840px이라는 것은 최소 크기, 최대 크기이다!<br/>
나처럼 320X3840에 맞추겠다고 끙끙대지말자. (어떻게 맞춰도 등록이 안된다)<br/>
사이즈를 딱 맞추려고 하지 않고, 그냥 대략 핸드폰 사이즈로는 이정도겠거니~하고 캡처해서 올렸다.<br/>

스토어 등록 정보 설정을 완료하고 다시 대시보드로 돌아온다.<br/>

<img src="/assets/images/5-production-app-apply.png" /><br/>

스크롤을 내려 **Google Play에 앱 게시**에서 할일 보기를 누르면, 아까와 마찬가지로 할일 목록이 나온다.<br/>

이제부터 본격적으로 개발자같은 일(?)을 한다!<br/>

2편에서 계속



















# 2. `ios` 버전 - App store



