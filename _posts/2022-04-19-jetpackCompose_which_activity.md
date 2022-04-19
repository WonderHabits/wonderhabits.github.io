---
title: "Jetpack Compose - ComponentActivity vs AppCompatActivity"
header:
  # image: /assets/images/koin.jpg
categories:
  - Android
tags:
  - Android
  - Jetpack Compose
toc: true
last_modified_at: 2022-04-19
use_math: true
---


Android Jetpack Compose 를 시작하기 위해 Empty Compose Activity로 프로젝트를 생성했다.

![](https://user-images.githubusercontent.com/60498900/163928292-5767bb9b-32d1-411c-abe8-c8d14dcca4e0.png)

생성된 코드를 보면 다음과 같이 ComposeActivity를 상속 받는 MainActivity가 생성된다.

![](https://user-images.githubusercontent.com/60498900/163929249-ff0db5e5-9f7b-4efb-8ae6-e7cc9d0425b3.png)

그런데 다른 Jetpack Compose 프로젝트를 보면 AppCompatActivity를 상속받는 경우가 많이 있었다. 

과연 어떤걸 상속 받아서 사용해야 할까?

결론은 ***AppCompatActivity***는 ***FragmentActivity***를 상속받고 ***FragmentActivity***는 ***ComponentActivity***를 상속받는다.

***ComponentActivity***를 상속받는 경우는 ***오직 Jetpack Compose만***을 사용해 앱을 만들 때 밖에 없다.
AppCompat을 사용하고 싶다던지 MaterialTheme을 사용하거나 xml과 혼용하여 앱을 만들고 싶은 다른 경우는 그냥 ***AppCompatActivity***를 상속받아 만들면 된다.
주의 할 점은 ***AppCompat*** 버전이 1.3.0 이상이어야 한다.

![](https://user-images.githubusercontent.com/60498900/163936150-0b9c35b9-c6af-4bd3-91c2-677fca7817f5.png)




