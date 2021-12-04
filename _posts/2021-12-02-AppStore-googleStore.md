---
title: "앱 만들기 끝판왕! 스토어에 등록하기 🧡"
permalink: /cs/AppStoreGoogleStore
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




## 1. `Android` 버전 - google play store


android App을 google play store에 등록하기 위해서는,<br/>
우선 `안드로이드 개발자 등록`(구글 플레이 개발자 등록)이 필요하다.
(당연하게도 필요한 구글 계정을 미리 준비하자)

1. 개발자 계정 등록하기 ✨

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


2. Play Console에서 앱 만들기 ✨

<img src="/assets/images/1-create-finish.png" /><br/>
Play Console로 이동하면 이런 화면이 나타난다.<br/>
앱만들기를 누른다.

<!-- <img src="/assets/images/1-create-finish.png" /><br/>
Play Console로 이동하면 이런 화면이 나타난다.<br/>
앱만들기를 누른다. -->





































## 2. `ios` 버전 - App store