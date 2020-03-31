---
title: "Koin - DI(Dependency Injection) Framework"
header:
  image: /assets/images/koin.jpg
categories:
  - Koin
tags:
  - Dev
  - Koin
  - Android
  - DI(Dependency Injection)
toc: true
last_modified_at: 2020-03-31
---
# Dependency Injection
Koin은 DI(Dependency Injection) Framework이다. 그래서 DI의 개념을 잘 알고 왜 써야 하는지 그 필요성을 느껴야 Koin을 잘 사용할 수 있다. 그냥 다들 쓰니까 써봐야지 하는 것도 모 나쁘진 않다. 구글에서도 DI사용을 강력하게 권유하고 있다. Koin 말고 Dagger였지만 .. 모..

하여튼 본론으로 들어가서 아주 간단한 예시를 통해 DI가 무엇인지 알아보자
[![foo](https://cdn.pixabay.com/photo/2017/06/14/18/48/silhouette-2402991_960_720.png)](https://pixabay.com/)

요즘같은 디지털 노마드 시대에 프로그래머가 일을 하기 위해선 laptop, 책상, 의자 정도만 있으면 충분하다. 그래서 다음과 같은 class를 만들 수 있다.

```kotlin
class Laptop()
class Desk()
class Chair()
class Coffee()

class Programmer(){
    val laptop = Laptop()
    val desk = Desk()
    val chair = Chair()
    val coffee = Coffee()
    fun programming(){
        // do programming not coding
    }
}
```
근데 위 코드를 자세히 살펴보면 몬가 이상해 보인다. 프로그래머는 프로그래밍만 하면 되는데 그전에 laptop, 책상, 의자를 손수 만들고 있다. 모 coffee정도야 직접 내려 먹는건 이해할 수 있지만..

바로 이런 의존성(dependency)를 끊기 위해 도입된 개념이 바로 DI(Dependency Injection)이다. 다음 코드와 같이 주로 constructor또는 setter를 통해 이미 누군가에 의해 만들어진 필요한 모듈을 주입하게 된다. 누군가가 laptop도 주고 책상도 주고 의자도 주고 커피도 주고.... 프로그래머는 프로그래밍만 열심히 하면 된다.
```kotlin
class Laptop()
class Desk()
class Chair()
class Coffee()

class Programmer(val laptop: Laptop, val desk: Desk, val chair: Chair, val coffee: Coffee){
    fun programming(){
        //focus on only programming
    }
}
```
실제 Android Empty Project 생성 후 gradle 파일에 koin관련 dependency적용, DI 까지 실제 반영한 github commit ([commit-589e1bc](https://github.com/WonderHabits/koinAndroidExample/commit/589e1bc27c17b52d4f9e3e96a18ae088665c8b5e#diff-d2a57dc1d883fd21fb9951699df71cc7))을 참고 바란다.
