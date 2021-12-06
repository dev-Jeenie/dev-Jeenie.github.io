---
title: "앱 만들기 끝판왕! 스토어 등록 🧡 1. Android(2)"
permalink: /cs/StoreForAndroid2
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-12-05
last_modified_at: 2021-12-05
---

![]()

## 1. 프로덕션 버전 만들기 ✨

<img src="/assets/images/A2-app-release-start.png" /><br/>

앱 서명 키는 따로 설정하지 않고 구글이 해주는 대로 설정한다.

<!-- 앱 서명 키는 따로 설정할 것이기 때문에  -->

React Native로 개발한 안드로이드 앱을 안드로이드 앱 스토어에 등록하기 위해서는, React Native를 안드로이드용으로 빌드해야한다.

(내가 진행중인 프로젝트에는 이미 이 단계가 완료되어있기 때문에 직접 추가하여 작업하지 않았다.)

### 안드로이드 서명키 등록하기

터미널로 들어가 등록을 원하는 프로젝트 경로로 간다.
```JS
cd [프로젝트 경로]/android/app
```

```C
# keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000

keytool -genkey -v -keystore [key-name].keystore -alias [key alias] -keyalg RSA -keysize 2048 -validity 10000

Enter keystore password:
Re-enter new password:
What is your first and last name?
  [Unknown]:
What is the name of your organizational unit?
  [Unknown]:
What is the name of your organization?
  [Unknown]:
What is the name of your City or Locality?
  [Unknown]:
What is the name of your State or Province?
  [Unknown]:
What is the two-letter country code for this unit?
  [Unknown]:
Is CN=*****, OU=Unknown, O=Unknown, L=*****, ST=*****, C=***** correct?
  [no]:

Enter key password for <my-key-alias>
    (RETURN if same as keystore password):
```

전부 입력이 끝나면, 프로젝트 폴더의 android/app 폴더에  `my-release-key.keystore` 파일이 생성되어 있다.

### gradle에 서명 키 설정
서명 키가 생성되면, gradle에 키를 설정해야한다. 아래의 코드를 `android/gradle.properties` 파일 안에 추가한다. <br/>

```C
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****
```

아래의 코드를 `android/app/build.gradle` 파일 안에 추가한다. <br/>

```C
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
                storeFile file(MYAPP_RELEASE_STORE_FILE)
                storePassword MYAPP_RELEASE_STORE_PASSWORD
                keyAlias MYAPP_RELEASE_KEY_ALIAS
                keyPassword MYAPP_RELEASE_KEY_PASSWORD
            }
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...

```

### 안드로이드로 빌드하기

해당 프로젝트의 android 폴더로 들어가서
`./gradlew assembleRelease`를 입력한다.
<br/>
약 3분정도의 시간이 지나면, 

`android/app/build/outputs/apk/release` 경로에 `app-release.apk` 파일이 생성되어있다.


eb10fe8f7c7c9df715022017b00c6471f8ba8170b13049a11e6c09ffe3056a104a3bbe4ac5a955f4ba4fe93fc8cef27558a3eb9d2a529a2092761fb833b656cd48b9de6a

### APK 파일 업로드하기

