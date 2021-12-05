---
title: "무지성 빌드 멈춰! gradle 🚨"
permalink: /cs/whatIsGradle
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-12-03
last_modified_at: 2021-12-03
---

![]()

1. android 폴더에 들어가서 `./gradlew assembleRelease` 을 하면 빌드가 뿅 된다.<br/>
2. 빌드가 끝났으면 /android/app/build/outputs/apk/release 위치로 간다<br/>
3. app-release.apk를 압축해서 카톡으로 보내기. 끝.<br/>
.<br/>
.<br/>
.<br/>

내가 아는 빌드란 오직 이 세단계 뿐이었다. 입력하라는 대로 입력만 하면 apk 파일이 뿅 나타났고, 그냥 그렇게 썼다. 만약 빌드가 실패한다면? 이유는 모르겠고 

## 1. gradle이란?

<img src="/assets/images/A2-app-release-start.png" /><br/>

앱 서명 키는 따로 설정하지 않고 구글이 해주는 대로 설정한다.