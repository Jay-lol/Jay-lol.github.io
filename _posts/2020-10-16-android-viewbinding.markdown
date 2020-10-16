---
layout: post
title: 안드로이드 ViewBinding
date: '2020-10-16 14:00:00 +0900'
description: null
img: androidlogo.jpg
tags:
  - Android
---

# [Android] 뷰 결합 ViewBinding


### ViewBinding  
 안드로이드 개발을 할때 뷰에 대한 인스턴스를 받기위해 `findViewById()`를 많이 사용한다.    
 
 ```kotlin
 val button : Button = findViewById(R.id.my_button)
 ```
하지만 일일이 인스턴스로 받다보면 코드도 길어지고 힘들다.  
그래서 코틀린에는`Kotlin Android Extension`을 활용하여 뷰 id로 바로 접근이 가능하다.  
<br/>
그래서 주로 이를 활용해서 개발을 해왔었다. 하지만 
kotlinx.android.synthetic은 더 이상 권장되지 않는다고 한다.  
>Synthetics 는 Google이 개발하지 않았으며 JetBrains가 제작 한 kotlin 안드로이드 확장의 일부이며 점차 Google Android 개발자는 데모 및 소스 코드에서 Synthetics를 ViewBinding로 대체하기 시작했습니다.  <br/><br/>
"지금 우리가 고려해야 할 질문이 있습니다."<br/><br/>
구글 (View binding, ButterKnife, Kotlin synthetics)에 따르면이 라이브러리는 많은 앱에서 성공적으로 사용되며 동일한 문제를 해결합니다.<br/><br/>
그러나 대부분의 앱에서 이러한 라이브러리 대신 ViewBinding을 사용해 보는 것이 좋습니다.  
ViewBinding은 더 안전하고 간결한 뷰 조회를 제공하기 때문입니다.<br/><br/>
사물을 빠르게 제거하기 위해 참조 이미지를 첨부했습니다.

![01]({{site.baseurl}}/assets/img/101605.png)  

ViewBinding을 공식문서에서는 다음과 같이 소개하고 있다.

> 뷰 결합 기능을 사용하면 뷰와 상호작용하는 코드를 쉽게 작성할 수 있습니다.   
모듈에서 사용 설정된 뷰 결합은 모듈에 있는 각 XML 레이아웃 파일의 결합 클래스를 생성합니다.  
바인딩 클래스의 인스턴스에는 상응하는 레이아웃에 ID가 있는 모든 뷰의 직접 참조가 포함됩니다.  
대부분의 경우 뷰 결합이 findViewById를 대체합니다.  

### 설정 방법

build.gradle에 viewBinding 요소를 추가해준다.
``` kotlin
android {
        ...
        viewBinding {
            enabled = true
        }
    }
```
binding클래스를 생성할때 무시하고 싶은 레이아웃은 `tools:viewBindingIgnore="true"`을 추가해준다.
``` kotlin
<LinearLayout
            ...
            tools:viewBindingIgnore="true" >
        ...
    </LinearLayout>
```
<br/>

### 사용

바인딩 된 클래스 의 이름은 XML 파일의 이름을 카멜 표기법으로 변환하고 끝에 'Binding'을 추가하여 생성됩니다.  
나의 메인액티비티 XML파일의 이름은 다음과 같다.  
![01]({{site.baseurl}}/assets/img/101702.PNG)  

그래서 ActivityMainBinding라는 바인딩 클래스가 생성된다.  
그리고 바인딩 클래스에는 해당 레이아웃 파일의 루트 뷰에 관한 직접 참조를 제공하는 getRoot() 메서드를 가지고 있다. 내 소스에서는 getRoot() 메서드가 ConstraintLayout 루트 뷰를 반환한다.
<br/>
<br/>

#### Activity에서 사용하기
바인딩 클래스를 만들었으니 이제 액티비티에서 사용해보자.  

onCreate() 메서드에서 차례대로 진행해보자.

1. 생성된 바인딩 클래스에 포함된 static inflate() 메서드를 호출. 그러면 액티비티에서 사용할 바인딩 클래스 인스턴스가 생성됩니다.  
    `binding = ActivityMainBinding.inflate(layoutInflater)`
 <br/><br/>

2. getRoot() 메서드를 호출하여 사용하여 루트 뷰를 가져옵니다.<br/>
    `binding.root`
 <br/><br/>

3. 루트 뷰를 setContentView()에 전달하여 화면상의 활성 뷰로 만듭니다.<br/>
    `setContentView(binding.root)`
 <br/><br/>

4. 만들어진 바인딩 클래스에 접근해서 뷰를 참조할 수 있다.<br/>
    `binding.hellotext.text = "Hello ViewBinding"`
<br/>    

![01]({{site.baseurl}}/assets/img/101701.PNG)

<br/><br/>
### findViewById와의 차이점

뷰 결합에는 findViewById를 사용하는 것에 비해 다음과 같은 중요한 장점이 있습니다.

* `Null 안전성` 뷰 결합은 뷰의 직접 참조를 생성하므로 유효하지 않은 뷰 ID로 인해 null 포인터 예외가 발생할 위험이 없습니다.   
 또한 레이아웃의 일부 구성에만 뷰가 있는 경우 결합 클래스에서 참조를 포함하는 필드가 @Nullable로 표시됩니다.  

* `Type 안전성` 각 바인딩 클래스에 있는 필드의 유형이 XML 파일에서 참조하는 뷰와 일치합니다.  
즉, 클래스 변환 예외가 발생할 위험이 없습니다.   
이러한 차이점은 레이아웃과 코드 사이의 비호환성으로 인해 런타임이 아닌 컴파일 시간에 빌드가 실패하게 된다는 것을 의미합니다.

### 참고
프레그먼트에서의 사용법과, 데이터바인딩과의 장단점도 있다.  
<a href="https://developer.android.com/topic/libraries/view-binding#kotlin" target="_blank">https://developer.android.com/topic/libraries/view-binding#kotlin</a>