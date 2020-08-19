---
date: 2020-03-27 07:45:40
layout: post
title: "AndroidManiFest.xml에 관한 정리"
subtitle:
description:
image: https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559820489/js-code_n83m7a.jpg
optimized_image: 
category: android
tags: Android Kotlin
author: 
paginate: false
---


안드로이드 개발시 main에 기본적으로 생성 되는 파일들은 다음과 같다

![이미지]({{site.baseurl}}/assets/img/Android/2020-03-27-19-13-15.png)


* java
* res
* AndroidManifest.xml 

 이중에서 안드로이드 개발을 하면서 `AndroidManiFest.xml` 파일을 많이
 수정해 보았는데 정확히 이 파일에서 어떤 일이 일어나는지 정리해 보려고 한다.

![meaning]({{site.baseurl}}/assets/img/Android/2020-03-29-15-29-47.png)

mainfest는 무언가를 명확히한다는 뜻을 가지고 있다.

따라서 Androidmanifest란 Android를 명확히 한다는 의미를 가지고 있다.
maifest는 27개의 속성을 가진다 ( https://developer.android.com/guide/topics/manifest/manifest-intro?hl=ko#reference )


![구성요소]({{site.baseurl}}/assets/img/Android/2020-03-29-15-41-01.png)

그중 manifest에는 위와 같이 7개의 속성이 있다. 
sharedUserLabel과 sharedUserId는 다음과 같은 이유로 요즘은 사용되지 않는거 같다.
![12]({{site.baseurl}}/assets/img/Android/2020-03-29-15-45-22.png)


<br/>


* ## 속성들의 의미

#### 1. xmlns

![이미지]({{site.baseurl}}/assets/img/Android/2020-03-27-17-20-15.png)



> xmlns:android="http://schemas.android.com/apk/res/android"
> xmlns는 XML NameSpace를 의미한다. 따라서 xmlns:android 는 android라는 네임스페이스를 선언하는것이다.


xmlns:[접두어]="문법 정의 URI"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {ex)=http://schemas.android.com/apk/(Package Name)}

schemas.android.com  안드로이드 스키마    
/apk/res ->  앱의 리소스
/android  -> 패키지명

위 URI를 풀어보면 안드로이드 스키마는 android라는 패키지명의 앱 리소스를  참조한다는 것이 된다!!

따라서 패키지명만 바꿔준다면 다른 앱의 리소스에 존재하는 문법도  충분히 이용 가능하다.

#### 2. package
> package="practice.kotlin.com.logoactivity"  이 정보로 앱을 식별하게 된다.

#### 3. versionCode

> android:versionCode
내부 버전 번호입니다. 이 번호는 한 버전이 다른 버전보다 최신인지 여부를 판단하는 데만 사용되며, 번호가 높을수록 더 최신 버전입니다. 이 버전 번호는 사용자에게 표시되지 않으며 사용자에게 표시되는 번호는 versionName 속성으로 설정됩니다.

#### 4. versionName
> android:versionName
사용자에게 표시되는 버전 번호입니다. 이 속성은 원시 문자열로 설정하거나 문자열 리소스의 참조로 설정할 수 있습니다. 문자열은 사용자에게 표시하는 것 이외에 다른 용도는 없습니다. versionCode 속성에는 내부적으로 사용되는 중요한 버전 번호가 포함되어 있습니다.

#### 5. installLocation
> android:installLocation
앱의 기본 설치 위치입니다.
다음 키워드 문자열을 사용할 수 있습니다.

| 값              | 설명                                |
| -------------- | --------------------------------- |
| internalOnly   | 앱은 내부 기기 저장소에만 설치해야 합니다(기본 설정)    |
| auto           | 기본적으로 내부에 설치. 용량이 가득차면 외부 저장소에 설치 |
| preferExternal | 외부에 설치                            |

<br/>
<br/>
<br/>
<br/>


> ### 참조 [https://developer.android.com/guide/topics/manifest/manifest-intro.html](https://developer.android.com/guide/topics/manifest/manifest-intro.html)