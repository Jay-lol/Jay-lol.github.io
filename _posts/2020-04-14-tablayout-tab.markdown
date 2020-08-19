---
date: {}
layout: post
title: Tablayout에서 Tab클릭이 안되는 오류
subtitle: null
description: null
image: >-
  https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559820489/js-code_n83m7a.jpg
optimized_image: null
category: android
tags: Android Kotlin
author: null
paginate: false
published: true
---

기상시간 앱을 만드는데 Tablayout으로 상단에 탭을 만들어서 사용하려했는데 이게 슬라이드로는 프레그먼트전환이 잘 일어나지만 버튼 클릭으로는 전환이 이루어지지 않아서 해결해 보았다.

![링크](..\assets\img\Android\2020-04-14-23-12-01.png)
<br>(출처: <https://stackoverflow.com/questions/34959298/android-material-design-click-event-on-tabs>)

웹서핑을 해보니까 비슷한 사례가 많이 나왔다. 그 해결방법은 대략 3가지 정도가 있는거같다.

>1.해당 부분이 뒤쪽으로 위치해 있을 수 있으므로 bringtoFront를 사용하여 Tablayout을 맨앞으로 가져온다.

>2.다음 함수를 오버라이드로 추가한다

```java
tabLayout.setOnTabSelectedListener(new TabLayout.OnTabSelectedListener() {
    @Override
    public void onTabSelected(TabLayout.Tab tab) {
        viewPager.setCurrentItem(tab.getPosition());
    }

});
```

>3.레이아웃 xml 파일에서 사이즈 설정의 오류 (이때  1번의 방법으로 억지로 해결은 가능하다)

나는 2번을 먼저해보고 변화가 없어서 1번의 문제라고 생각을 했다.
그래서 1번을 통해서 임시방편으로 해결을 하고 다시 3번을 통해 완벽하게 해결했다.....

#### activity_main.xml
```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
        // 생략..... 
        <com.google.android.material.tabs.TabLayout
            android:id="@+id/main_tablayout"

    <androidx.viewpager.widget.ViewPager
            android:id="@+id/main_viewPager"
            android:layout_width="match_parent"
            android:layout_height="622dp"    // 높이를 강제로 할당
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintBottom_toBottomOf="parent"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```

초기 activity_main.xml 코드이다. viewPager의 높이를 강제로 622dp로 설정을 해버려서 위에 TabLayout을 침범해서 덮어버린 것이다.

따라서 이 부분을 다음과 같이 해결했다.

```kotlin
<androidx.viewpager.widget.ViewPager
            android:id="@+id/main_viewPager"
            android:layout_width="match_parent"
            android:layout_height="0dp" // 높이를 0으로설정후
            app:layout_constraintTop_toBottomOf="@id/main_tablayout"    // TabLayout밑을 시작점으로 설정
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintBottom_toBottomOf="parent"
            />
```

이를 통해 높이를 강제로 할당한 경우에 에뮬레이터에서는 정상동작 하지만, 기기별로 높이가 다르기 때문에 제대로 동작되지 않는 기기도 있어서 안좋은 설정방법임을 깨달았다.
