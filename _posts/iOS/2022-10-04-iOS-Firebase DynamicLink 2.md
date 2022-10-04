---
title: '[iOS / Obj-C] Firebase DynamicLink 생성(2)'
excerpt: 'Firebase DynamicLink'

categories:
  - iOS
tags:
  - [iOS, Obj-C]

permalink: /iOS/firebase-dynamiclink-2/

toc: true
toc_sticky: true

date: 2022-10-04
last_modified_at: 2022-10-04
---

이제 반은 성공이다. Firebase console 에서 설정 완료후 네이티브 소스를 진행하는 단계이다.

참고사이트

### Firebase DynamicLinks Set up

[https://firebase.google.com/docs/dynamic-links/ios/receive#objective-c_3](https://firebase.google.com/docs/dynamic-links/ios/receive#objective-c_3)

### Firebase Quick Start Obj-C

[https://github.com/firebase/quickstart-ios/blob/master/dynamiclinks/DynamicLinksExample/AppDelegate.m](https://github.com/firebase/quickstart-ios/blob/master/dynamiclinks/DynamicLinksExample/AppDelegate.m)

### 구현방법

1. Associated Domains, URL Types 추가
   Associated Domains 에 applinks:escjunior.page.link 추가
   (Associated Domains 없을 경우 Capability 옆 + 버튼 눌러서 추가)

   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193742003-d33360a9-3240-447b-aa93-5d8f6010060a.png">

   Targets → Info → URL Types 에서 URL Schemes 등록

   **_중요! 앱 Bundle ID 로 입력해야 함_**

   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193742013-2b2bec75-fab9-4aa6-82ba-a2e09916c6ab.png">

2. Podfile import
   FirebaseFirestore, FirebaseAuth, FirebaseDynamicLinks Podfile에 입력후
   terminal 앱에서 해당 프로젝트 경로 진입후 pod install 진행

   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193741089-6a7e0561-b16f-419a-aff3-00c01dbbb55d.png">
   <img width="70%" src="https://user-images.githubusercontent.com/46982959/193741093-5b09cc9c-415e-416e-8419-f08ad4d73fe1.png">

3. AppDelegate.m 소스 추가

```objectivec
static NSString *const CUSTOM_URL_SCHEME = @"dlscheme";

// [START openurl]
- (BOOL)application:(UIApplication *)app
            openURL:(NSURL *)url
            options:(NSDictionary<NSString *, id> *)options {
  return [self application:app
                  openURL:url
        sourceApplication:options[UIApplicationOpenURLOptionsSourceApplicationKey]
                annotation:options[UIApplicationOpenURLOptionsAnnotationKey]];
}

- (BOOL)application:(UIApplication *)application
            openURL:(NSURL *)url
  sourceApplication:(NSString *)sourceApplication
        annotation:(id)annotation {
  FIRDynamicLink *dynamicLink = [[FIRDynamicLinks dynamicLinks] dynamicLinkFromCustomSchemeURL:url];

  // ***여기가 dynamicLink 실행부분
  if (dynamicLink) {
    if (dynamicLink.url) {
      // Handle the deep link. For example, show the deep-linked content,
      // apply a promotional offer to the user's account or show customized onboarding view.
      // [START_EXCLUDE]
      // In this sample, we just open an alert.
      [self handleDynamicLink:dynamicLink];
      // [END_EXCLUDE]
    } else {
      // Dynamic link has empty deep link. This situation will happens if
      // Firebase Dynamic Links iOS SDK tried to retrieve pending dynamic link,
      // but pending link is not available for this device/App combination.
      // At this point you may display default onboarding view.

    }
    return YES;
  }
  // [START_EXCLUDE silent]
  // Show the deep link that the app was called with.
  //[self showDeepLinkAlertViewWithMessage:[NSString stringWithFormat:@"openURL:\n%@", url]];
  // [END_EXCLUDE]
  return NO;
}
// [END openurl]

// [START continueuseractivity]
- (BOOL)application:(UIApplication *)application
continueUserActivity:(nonnull NSUserActivity *)userActivity
restorationHandler:
#if defined(__IPHONE_12_0) && (__IPHONE_OS_VERSION_MAX_ALLOWED >= __IPHONE_12_0)
(nonnull void (^)(NSArray<id<UIUserActivityRestoring>> *_Nullable))restorationHandler {
#else
    (nonnull void (^)(NSArray *_Nullable))restorationHandler {
#endif  // __IPHONE_12_0
  BOOL handled = [[FIRDynamicLinks dynamicLinks] handleUniversalLink:userActivity.webpageURL
                                                          completion:^(FIRDynamicLink * _Nullable dynamicLink,
                                                                      NSError * _Nullable error) {
                                                            // [START_EXCLUDE]
                                                            [self handleDynamicLink:dynamicLink];
                                                            // [END_EXCLUDE]
                                                          }];
  // [START_EXCLUDE silent]
  if (!handled) {
    // Show the deep link URL from userActivity.
    NSString *message = [NSString stringWithFormat:@"continueUserActivity webPageURL:\n%@",
                        userActivity.webpageURL];
    [self showDeepLinkAlertViewWithMessage:message];
  }
  // [END_EXCLUDE]
  return handled;
}
// [END continueuseractivity]

- (void)handleDynamicLink:(FIRDynamicLink *)dynamicLink {
  NSString *matchConfidence;
  if (dynamicLink.matchType == FIRDLMatchTypeWeak) {
    matchConfidence = @"Weak";
  } else {
    matchConfidence = @"Strong";
  }
  NSString *message = [NSString stringWithFormat:@"App URL: %@\n"
                      @"Match Confidence: %@\nMinimum App Version:%@",
                      dynamicLink.url, matchConfidence, dynamicLink.minimumAppVersion];
  //[self showDeepLinkAlertViewWithMessage:message];
    NSString *myString = dynamicLink.url.absoluteString;
    [[DataManager getInstance].webViewController loadURL:myString];
}

- (void)showDeepLinkAlertViewWithMessage:(NSString *)message {
  NSString *title = @"Deep-link Data";
  NSString *buttonTitle = @"OK";

  if ([UIAlertController class]) {
    UIAlertController *alert =
    [UIAlertController alertControllerWithTitle:title
                                        message:message
                                preferredStyle:UIAlertControllerStyleAlert];
    [alert addAction:[UIAlertAction actionWithTitle:buttonTitle
                                              style:UIAlertActionStyleDefault
                                            handler:nil]];
    UIViewController *rootViewController = self.window.rootViewController;
    [rootViewController presentViewController:alert animated:YES completion:nil];
  } else {
    UIAlertView *alertView = [[UIAlertView alloc] initWithTitle:title
                                                        message:message
                                                      delegate:nil
                                              cancelButtonTitle:buttonTitle
                                              otherButtonTitles:nil];
    [alertView show];
  }
}
```

끝! 이제 1단계에서 설정한 https://escjunior.page.link/Tbeh 링크 접속시 앱 또는 해당 URL이 브라우저에서 열림!😆😆
