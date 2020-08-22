---
date: 2020-03-25T20:20:27.000+09:00
layout: post
title: "안드로이드 스튜디오 java.net.SocketException: socket failed: EPERM (Operation not permitted) 에러 해결"
subtitle: null
description: null
image: https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559820489/js-code_n83m7a.jpg  
category: android
tags: Android  Kotlin
author: null

---

안드로이드 공부중에 자꾸 까먹는 에러가 있어서 기록하려고 한다.

![에러]({{site.baseurl}}/assets/img/Android/1.JPG)

`Operation not permitted` 라는 에러가 발생하는데...

해결 방법은 해당 operation에 맞는 permission을 허가해주면 된다.

나는 소켓통신을 사용해서 통신시도를 하는 중 이였다.


`<uses-permission android:name="android.permission.INTERNET"/>`

그래서 바로 해당하는 permission을 추가해주었다.

하지만 그래도 계속 에러가 발생해서 신뢰의 구글링을 해본결과...

**에뮬레이터에있는 앱을 Uninstall한후 다시 실행해보라는 것이였다.**

 >![에러]({{site.baseurl}}/assets/img/Android/2.JPG "LogoActivity")
 >
 > 
 >![에러]({{site.baseurl}}/assets/img/Android/3.JPG "LogoActivity")

에뮬레이터에서 해당하는 앱을 선택하여 언인스톨 해준다

그후 다시 실행을 하면 앱이 생성되면서 에러없이 돌아간다.

아마 AndroidManifest.xml은 앱이 한번 생성되면 업데이트를 해주는 방법으로 처리를 해야되나보다.. 이부분은 공부가 필요하다고 느낀다.
