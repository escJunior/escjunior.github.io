---
title: '[iOS / Obj-C] Web Image 캐싱 문제'
excerpt: 'Web Image 캐싱 문제'

categories:
  - iOS
tags:
  - [iOS, Objecitve-C]

permalink: /iOS/Web Image Cahche Issue/

toc: true
toc_sticky: true

date: 2022-09-14
last_modified_at: 2022-09-14
---

처음 상태는 회사 로고만 기본으로 띄우고 메인화면으로 진입하였다.

앱 실행시 메인화면 진입 전 이벤트 이미지를 띄우고 싶다는 개발요청이 들어와서

Native 단 UIImageView에 이벤트 이미지를 넣었다.

이렇게 하니 이미지 교체시마다 앱 심사를 받아야했다. 생각이 짧았다.

그래서 현업이 사용하는 관리자페이지에서 WebServer에 이미지를 업로드 / 삭제 가능하도록 하고

앱실행시 이벤트 이미지를 가져와 띄울 수 있도록 하였다.

처음 업로드한 이미지는 잘 보였지만 이후 교체한 이미지가 바로보이지 않고

이전 이미지가 보이는 이슈에 직면하였다. 같은 경로를 호출하기 때문이다.

캐싱 때문에 웹소스 수정시 js, css에 쿼리스트링을 사용하는 것이랑 비슷하다.

여러 방법을 적용해봤지만 SDWebImage Lib 를 사용하여 해결하였다.

1. Podfile에 pod 'SDWebImage','~> 5.0’ 추가
2. terminal 에서 해당 프로젝트 폴더로 진입하여 pod update
3. #import <SDWebImage/SDWebImage.h> 선언
4. Code

```objectivec
[[SDImageCache sharedImageCache]clearMemory];
/* options:SDWebImageRefreshCached 로 해주어야한다.
This option helps deal with images changing behind the same request URL, e.g. Facebook graph api profile pics.
*/
[[SDWebImageManager sharedManager] loadImageWithURL:imageURL options:SDWebImageRefreshCached progress:^(NSInteger receivedSize, NSInteger expectedSize, NSURL * _Nullable targetURL) {
 } completed:^(UIImage * _Nullable image, NSData * _Nullable data, NSError * _Nullable error, SDImageCacheType cacheType, BOOL finished, NSURL * _Nullable imageURL) {

     if(data != nil && self->lsFlag == YES) {
         self->lsImageData = data;
     } else {
         self->lsImageData = nil;
     }

     self->lsFlag = YES;
}];
```
