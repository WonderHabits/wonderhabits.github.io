---
title: "Koin - android gradle dependencies setup"
header:
  image: /assets/images/koin.jpg
categories:
  - Koin
tags:
  - Dev
  - Koin
  - Android
toc: true
last_modified_at: 2020-03-30
---
# Gradle Dependencies Setup
Kotlin으로 Android 개발 시 가장 우선적으로 해야 할 것은 build.gradle (Module:app) 에 다음과 같이 dependencies setup을 해주어야 한다.

최신 버전은  ([Koin](https://doc.insert-koin.io/#/setup/index)) 에서 확인 가능하다.

```kotlin
// 최신 stable version
def koin_version= "2.1.5"
// Koin AndroidX Scope feature
implementation "org.koin:koin-androidx-scope:$koin_version"
// Koin AndroidX ViewModel feature
implementation "org.koin:koin-androidx-viewmodel:$koin_version"
// Koin AndroidX Fragment Factory (unstable version)
implementation "org.koin:koin-androidx-fragment:$koin_version"
```

실제 Android Empty Project 생성 후 gradle 파일에 koin관련 dependency적용 까지 실제 반영한 github commit ([commit-031014d](https://github.com/WonderHabits/koinAndroidExample/commit/031014dfb8b8fa12c9e35a12cb2042987578dad9#diff-39e7d8c00954e920b98e7636f0ac30b2))을 참고 바란다.