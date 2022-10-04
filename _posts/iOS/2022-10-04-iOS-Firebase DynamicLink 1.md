---
title: '[iOS / Obj-C] Firebase DynamicLink 생성(1)'
excerpt: 'Firebase DynamicLink'

categories:
  - iOS
tags:
  - [iOS, Obj-C]

permalink: /iOS/firebase-dynamiclink-1/

toc: true
toc_sticky: true

date: 2022-10-04
last_modified_at: 2022-10-04
---

이벤트 또는 타사와 제휴 서비스등으로 링크를 이용해 앱을 실행 할 수 기능이 필요할 때가 있다.

뿐만 아니라 링크를 이용하여 앱 실행후에 특정 메뉴로 이동이 필요할 때도 DynamicLink 로 해결이 가능하다.

이 때 링크를 이용해 앱을 실행 할 수 있는 방법

1. App Scheme
   제일 간단하지만, 해당 앱이 설치 되어 있지 않은 경우 차선책이 없다.
   PROJECT → TARGETS → Info → URL Types 에서 설정 가능
2. Deep Link
   Google Firebase DynamicLink를 이용하거나, 다른 Third Party 서비스를 이용해야 한다.
3. Universal Link
   iOS만 가능한 Custom Link 이지만 WebServer 설정도 필요하고 조금 복잡하다.

2, 3 번은 모두 앱이 설치 되지 않은 경우 앱 스토어로 이동이 가능하다.

나는 Firebase를 사용하여 Deep Link를 구현하기로 하였다.

참고사이트

### Firebase DynamicLinks Set up

[https://firebase.google.com/docs/dynamic-links/ios/receive#objective-c_3](https://firebase.google.com/docs/dynamic-links/ios/receive#objective-c_3)

### Firebase Quick Start Obj-C

[https://github.com/firebase/quickstart-ios/blob/master/dynamiclinks/DynamicLinksExample/AppDelegate.m](https://github.com/firebase/quickstart-ios/blob/master/dynamiclinks/DynamicLinksExample/AppDelegate.m)

### 구현방법

1. Firebase Console 접속, iOS 프로젝트 클릭

   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193738702-aa69a16e-34b5-4887-9933-3686539ee626.png">

2. 참여 → Dynamic Links 클릭

   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193738825-0d8761d6-62b2-4756-aac5-53858c408b2b.png">

3. URL Prefix 추가 클릭(링크 앞 부분 고정 주소), URL Prefix + Custom text 로 여러 링크 생성이 가능하다.

   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193739167-b6b73a27-f841-4ecf-8ff6-051a8ede09a3.png">
   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193739222-46cbc2fc-e419-4f66-9b20-9771b81b1b0f.png">
   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193739228-8a9cbe52-772b-457a-b21f-46b2a9bb66f3.png">

4. 새 동적 링크 클릭

   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193739384-203593b9-6db0-48e3-b94c-a63ee6075fb0.png">

5. 프리픽스 뒤 주소는 custom 입력 가능
   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193739389-240d3e18-5121-4b44-bedd-2d5ff1af166d.png">

   딥 링크 URL: 실제 띄우고 싶은 URL
   동적 링크 이름: 딥 링크 URL 구분하기 위한 이름

    <img width="70%" src="https://user-images.githubusercontent.com/46982959/193739391-f0a6e8c0-c117-4949-baaa-91fdf3f077c5.png">

   iOS, AOS 모두 설정이 가능하다. 앱이 없을 경우에도 가능하다.(갓구글…)

    <img width="70%" src="https://user-images.githubusercontent.com/46982959/193739398-20dc851c-e518-4eb4-991f-fe0e69ba088d.png">
    <img width="70%" src="https://user-images.githubusercontent.com/46982959/193739409-fb558654-068f-4704-9c4c-e4112d8d5450.png">
    
    DynamicLink 생성완료.  
    
    <img width="70%" src="https://user-images.githubusercontent.com/46982959/193739412-188b4f54-bafe-44f1-ae3a-48a586b76ad0.png">

Firebase DynamicLink 생성(2) 로 넘어가자 ✅
