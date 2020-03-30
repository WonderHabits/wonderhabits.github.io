---
title: "Koin 왜 쓰나요?"
header:
  image: /assets/images/koin.jpg
categories:
  - Koin
tags:
  - Dev
toc: true
last_modified_at: 2020-03-27
---

Kotlin으로 Android 개발 시 사용가능항 DI(Dependency Injection) framework에는 dagger2, Koin, kodein등이 존재한다. 어떤것을 사용해야 가장 효율적이고 가장 빠르게 구현할 수 있을까 하는 의문점에 수 많은 개발 블로그, 유투브를 검색한 결과 Koin 가장 좋다는 결론을 갖게 되었다.
누구 말 맞다나 Koin의 네이밍은 kotlin에서 'tl' 만 빼서 이름을 지은거라고..

'Kotlin' - 'tl' = 'Koin'

# Koin 이란?
Koin은 순수 Kotlin만으로 작성된 DI framework로 매우 경량화 되어 있고 실용적인 API이다. 자세한 사용법은 차차 적어 나가겠다.

# DSL 이란?
Koin 공식 사이트([Koin](https://insert-koin.io))를 보다 보면 몇 가지 생소한 용어가 나오는데 그중에 하나가 DSL이다.

  **DSL : Domain Specified Language**

영어를 풀어서 말하면 도메인(산업, 분야등 특정 영역)에 특화된 언어를 말한다. 한마디로 그 영역에서 좀 굴러먹은 전문가들만 쓰는 언어란 것이다. 쉽게 이해하기 위해서 예를 들면 새벽 노량진 시장 킹크랩 도매시장에서 들리는 도매상인들만 사용하는 암호같은 언어라던지, 건설현장에서 쓰이는 노가다 용어같은 것들이 DSL인 것이다.

# 결론
Koin 왜 쓰나요? 결국 쉽게 얘기하자면 내가 생각하는 Koin을 사용하는 이유는 Kotlin을 사용하고, Android 개발을 할 줄 아는 개발자가 DI 사용에 대한 필요성을 절실히 느껴야 한다는 것이다. 아니면 굳이 배울 필요가 없을 것 같다. 