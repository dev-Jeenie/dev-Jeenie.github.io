---
title: "앱 만들기 끝판왕! 스토어 등록 💙 2. ios(1)"
permalink: /store/StoreForIos2
tags:
  - [store]

navigation: true
toc: true
toc_sticky: true

date: 2021-12-05
last_modified_at: 2021-12-05
---

![]()


React native로 개발한 앱을 스토어에 등록하려고 한다. android 버전과 ios 버전이 있기 때문에, 각각 google play store와 App store에 등록하는 과정을 기록한다.

# 2. `ios` 버전 - App store

앱스토어에 제출하기

## App store 등록 전, 사전지식
- 1. 앱 리뷰 가이드라인 확인하기

앱스토어 심사지침(https://developer.apple.com/kr/app-store/review/guidelines/)을 확인해야한다.<br/>

애플은, 다운받는 앱이 사용자한테 안전하다고 느껴야함.<br/>
그래서 애플이 안전하게 느낄 수 있는 기준을 정해서 앱스토어 심사지침에 정리해둔 것.<br/>

이 지침에 따라서 앱을 만들지 않으면 리젝시켜버림!<br/>

안정성 성과 비즈니스 디자인 법적 요구사항 등 중에서 맞지 않으면 리젝시켜버림. 꼭 필독할 것⭐️<br/>

- 2. 버그 & 크래시 찾기

버그가 보이거나 크래시가 나면 바로 리젝.

- 3. 애플 개발자 프로그램 가입

올리기 전에 애플 개발자 프로그램 가입을 해야한다.

개인 : 99달러<br/>
팀 : 299달러<br/>

- 4. Appstoreconnect에서 앱 생성

Appstoreconnect란? 웹 기반의 앱을 관리하는 툴.
애플 개발자 프로그램에 가입하면 Appstoreconnect을 쓸 수 있다.
앱스토어 커넥트에 마이앱 - 앱 만들기 - 뉴 앱 생성.

- 5. 앱 정보 넣기

출시하기 전, 추가적인 앱 관련 데이터를 넣어야한다.
아이콘, 스크린샷, 동영상 등.
동영상 한개에 스크린샷 다섯개가 가장 이상적인 형태.
앱 관련한 메타데이터 넣기.

아이콘 하나를 여러 사이즈로 준비해야함!
https://appicon.co/ 에서 여러 사이즈로 변환해준다.



## App store에 계정 등록하기 ✨

앱스토어에 앱을 등록하려면, 구글 플레이스토어처럼 개발자 계정을 만들어야한다.<br/>
애플 개발자 사이트:  https://developer.apple.com/ <br/>

구글 스토어는 25달러(약 3만원)이었지만, App store는 99달러(약 129,000원)이다. 그것도 매년 갱신해서 결제해야한다.<br/>

갱신되지 않으면 앱이 앱스토어에서 내려가고, 그 기간이 길어지면 계정이 삭제될 수 있다😱

애플 개발자 계정은 애플기기로 애플기기 인증을 받아야만 등록이 가능하다.

1. https://developer.apple.com/ 애플 개발자 사이트로 이동

<img src="/assets/images/apple-developer-site-account.png" /><br/>

`Account`를 클릭한다

애플 개발자 계약을 하고 가입을 완료한 뒤


<img src="/assets/images/apple-developer-site-account-1.png" /><br/>

하단의 `Join the Apple Developer Program` 클릭

<img src="/assets/images/apple-developer-site-program.png" /><br/>

Enroll 클릭


<img src="/assets/images/apple-developer-enroll-personal.png" /><br/>
<img src="/assets/images/apple-developer-enroll-company.png" /><br/>
개인으로 등록하기, 또는 조직으로 등록하기를 선택할 수 있다.
개인의 경우에는 무난하게 할 수 있지만, 기업은 D-U-N-S number(국제 사업자등록번호)를 발급받아야한다.
이미 발급받은게 있으면 사용할 수 있지만, 없을 경우는 신청을 해서 발급받아야 한다.(3-4일 시간 소요)


<img src="/assets/images/apple-developer-enroll-company-duns.png" /><br/>
https://developer.apple.com/enroll/duns-lookup/#!/search 에서 회사의 D-U-N-S를 찾을 수 있다.


<img src="/assets/images/apple-developer-site-select.png" /><br/>
개인인지 법인인지 선택을 한 뒤

- 법인으로 등록하기 위해서는
<img src="/assets/images/apple-developer-site-select-company-1.png" /><br/>
<img src="/assets/images/apple-developer-site-select-company-2.png" /><br/>

  - 법인 상태
  - 법적 계약에 서명할 권한
  - 웹 사이트
  - D-U-N-S® 번호

등이 필요하다.


<img src="/assets/images/apple-developer-site-select-info.png" /><br/>
정보를 입력한다.
<img src="/assets/images/apple-developer-site-developer-pay.png" /><br/>
1년 등록비를 결제하면 개발자 등록 완료.

* 주의!

결제가 완료되면 개발자 계정 등록이 완료되지만 바로 승인이 되는 것이 아님
일주일 ~ 3주까지 걸리기 때문에 실제 개발자 계정으로 승인되기까지는 시간이 걸림.
등록을 완료하더라도 승인되어 활성화됐다는 메일을 받기 전까지는 이용이 불가.


## App store에 등록하기 ✨

