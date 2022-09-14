---
title: '[iOS / Obj-C] wkWebView Youtube inline 재생'
excerpt: 'wkWebView Youtube inline 재생'

categories:
  - iOS
tags:
  - [iOS, Objecitve-C]

permalink: /iOS/wkWebView Youtube inline/

toc: true
toc_sticky: true

date: 2022-09-14
last_modified_at: 2022-09-14
---

웹뷰 화면에서 유튜브 영상 재생시 전체 화면으로 재생되어 기본 크기로 재생되도록 수정하는 문의가 왔다.

이 경우 Web 과 App 모두 수정이 필요하다.

**Web**

1. iframe 옵션에 webkit-playsinline="1" 설정

```html
<iframe
  webkit-playsinline="1"
  width="100%"
  height="auto"
  src="https://www.youtube.com/embed/Qc0zvvqm8Vg"
  title="YouTube video player"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen=""
></iframe>
```

**App**

1. WKWebViewConfiguration 변수 선언
2. allowsInlineMediaPlayback = YES;
3. Frame 생성시 Config 값 전달, configuration: theConfiguration

```objectivec
WKWebViewConfiguration *theConfiguration = [[WKWebViewConfiguration alloc] init];
theConfiguration.allowsInlineMediaPlayback = YES;
self.wkWebView = [[WKWebView alloc]initWithFrame:CGRectMake(0, 0, self.webGuideView.frame.size.width, self.webGuideView.frame.size.height) configuration: theConfiguration];
```

정의를 따라가면 기본 값은 NO 이며 전체화면으로 재생된다는 것을 알 수 있다.

```objectivec
#if TARGET_OS_IPHONE
/*! @abstract A Boolean value indicating whether HTML5 videos play inline
 (YES) or use the native full-screen controller (NO).
 @discussion The default value is NO.
 */
@property (nonatomic) BOOL allowsInlineMediaPlayback;
```
