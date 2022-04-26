---
title: "Jetpack Compose 개발 시 이해해두면 좋은 Lambda Function"
header:
  # image: /assets/images/koin.jpg
categories:
  - Android
tags:
  - Android
  - Jetpack Compose
  - Kotlin
  - Lambda Function
  - setContent
toc: true
last_modified_at: 2022-04-26
use_math: true
---
# Jetpack Compose 개발 시 이해해두면 좋은 Lambda Function
Jetpack Compose를 이용해 개발하다보면 일반적으로 다음과 같이 Composable 요소를 연속적으로 나열하게 된다   
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Box {
                Row {
                    Text("Hello")
                    Text("World")
                }
            }
        }
    }
}
```
근데 일반적은 코드와는 달리 몬가 많이 생략되어있는 느낌이다. Composable Component옆에 중괄호들은 다 어디가고 바로 대괄호를 쓰고 있다.   
위의 코드에서 *setContent*와 Composable Component인 *Box*, *Row*의 reference 코드를 잘 살펴 보자.   
1. setContent   
![](https://user-images.githubusercontent.com/60498900/165269825-0e2cadfb-0998-4c79-bb24-90b44dc157ac.png)

2. Box   
![](https://user-images.githubusercontent.com/60498900/165269847-916b8e2d-8d84-42b3-a276-10e4ffe12cfa.png)

3. Row   
![](https://user-images.githubusercontent.com/60498900/165269873-25ee7a1c-cd2a-447d-9b47-bffee22a582f.png)   

모두 공통적으로 마지막 parameter인 content의 return 값은 @Composable인 '()->Unit'(Lambda Function) 이다. 결국 다음과 같은 a->b->c 단계를 통해 람다식을 이용하려 간단하게 표현할 수 있다.

```kotlin
// a. 마지막 parameter 인 content에  @Composable Lambda Function 사용
setContent(content = @Composable{})
// b. Kotlin에선 마지막 paramter에 Lambda Function 사용 시 중괄호 밖으로 꺼낼 수 있다.
setContent(){}
// c. Lambda Function에 아무런 parameter가 필요 하지 않으면 생략 가능
setContent{}
```

이해해 두면 Jetpack Compose을 사용할 때 매우 유용하다.