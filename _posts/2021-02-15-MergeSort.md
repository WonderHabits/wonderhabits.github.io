---
title: "합병 정렬, Merge Sort C++ Sample Code"
header:
  # image: /assets/images/koin.jpg
categories:
  - Coding Interview
tags:
  - Algorithm
  - C++
  - Merge Sort
  - 합병 정렬
toc: true
last_modified_at: 2021-02-15
use_math: true
---
<br/>
<div>
<a href="https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC" class="bookmark source"><div class="bookmark-info"><div class="bookmark-text"><div class="bookmark-title">합병 정렬</div><div class="bookmark-description">n-way 합병 정렬의 개념은 다음과 같다. 정렬되지 않은 리스트를 각각 하나의 원소만 포함하는 n개의 부분리스트로 분할한다. (한 원소만 든 리스트는 정렬된 것과 같으므로) 부분리스트가 하나만 남을 때까지 반복해서 병합하며 정렬된 부분리스트를 생성한다. 마지막 남은 부분리스트가 정렬된 리스트이다. 흔히 쓰이는 하향식 2-way 합병 정렬은 다음과 같이 작동한다. 리스트의 길이가 1 이하이면 이미 정렬된 것으로 본다.</div></div><div class="bookmark-href"><img src="https://ko.wikipedia.org/static/favicon/wikipedia.ico" class="icon bookmark-icon"/>https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC</div></div><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/cc/Merge-sort-example-300px.gif/220px-Merge-sort-example-300px.gif" class="bookmark-image"/></a>
</div>
<br/>
 Coding Interview에서 자주 사용되는 Sorting 알고리즘 중 하나이다.

 Divide & Conquer 알고리즘 중의 하나이고 개인적으론 Quick Sort보다 Merge Sort 가 훨씬 유용하게 쓰인다.

 그 이유는 평균시간복잡도가 Quick Sort와 같이 $O(nlogn)$으로 같고 DB문제에서 한가지 field 정렬 뿐만 아니라 2개 이상의 field에 대한 정렬을 동시에 수행할 수 있기 때문인다.

 코딩인터뷰를 처음 준비할 때 Quick Sort의 이름만 믿고 제일 빠른 줄 착각한 상태에서 Quick Sort만 달달 외워서 문제를 풀어 보았지만 2가지 이상의 field를 정렬할 때 전체 정렬을 2번 수행해야 하는 매우 난감한 상황을 겪은 이후로 Merge Sort를 사용하고 있다.

 예를 들어 DB 에 키와 성적이라는 2가지 field가 존재할 때 키는 오름차순으로, 성적은 내림차순으로 정렬할 경우 다음 코드와 같이 쉽게 정렬할 수 있고 그 코드가 매우 이해하기 편하다.
<br/>
<div>
<a href="https://www.youtube.com/watch?v=QAyl79dCO_k" class="bookmark source"><div class="bookmark-info"><div class="bookmark-text"><div class="bookmark-title">[자료구조 알고리즘] 병합정렬(Merge Sort) 구현하기</div></div><div class="bookmark-href"><img src="https://www.youtube.com/s/desktop/3748dff5/img/favicon.ico" class="icon bookmark-icon"/>https://www.youtube.com/watch?v=QAyl79dCO_k</div></div><img src="https://i.ytimg.com/vi/QAyl79dCO_k/hqdefault.jpg" class="bookmark-image"/></a>
</div>
<br/>
 Merge Sort를 이해하는 가장 쉬운 방법은 위 영상을 그냥 10번만 보면 된다. Merge Sort를 이렇게 쉽게 설명한 자료는 찾아보기 매우 힘들고 특히 선생님의 딕션이 뇌에 팍팍 꽂힌다.

# 1. Merge Sort C++ Code (Single Data)

```cpp
#include <iostream>
#define SIZE 10
using namespace std;
// DB에 Field 가 score 1개만 존재
typedef struct _db {
    int score;
}DB;

// Merge Sort는 DB크기와 동일 크기의 공간이 더 필요하다.
// Memory가 부족하면 Quick Sort를 대신 사용한다.
DB tmp[SIZE];

// Combine
void combine(int start, int mid, int end, DB arr[]) {
    int l = start; //   ㅁㅁㅁㅁ  merge할 첫 번째 arr의 index pointer
    int r = mid + 1; //     ㅁㅁㅁㅁ  merge할 두 번째 arr의 index pointer
    int k = start; //   ㅁㅁㅁㅁㅁㅁㅁㅁ merge결과를 저장할 tmp의 index pointer

    // merge할 두개의 arr 중 하나라도 끝날 때 까지
    while ((l <= mid) && (r <= end)) {
        // DB의 비교가능 field 가 height 1개만 존재
        if (arr[l].score <= arr[r].score)
            tmp[k++] = arr[l++];
        else
            tmp[k++] = arr[r++];
    }

    // 남은 db를 모두 다 순서대로 저장한다.
    if (l <= mid) {
        while (l <= mid) {
            tmp[k++] = arr[l++];
        }
    }
    else {
        while (r <= end) {
            tmp[k++] = arr[r++];
        }
    }

    // 정렬된 tmp 를 DB에 다시 복사한다.
    for (int i = start; i <= end; i++) {
        arr[i] = tmp[i];
    }
}

// MergeSort
void mergeSort(int start, int end, DB arr[]) {
    // 정렬할 DB가 2개 이상일 경우에 recursive하게 merge sort를 동작한다
    if (start < end) {
        // DB의 data를 반으로 나눈다 
        int mid = (start + end) / 2;
        mergeSort(start, mid, arr);
        mergeSort(mid + 1, end, arr);
        combine(start, mid, end, arr);
    }
}
// main
void main() {
    DB arr[SIZE] = { {89}, {100}, {45}, {70}, {91}, {98}, {64}, {36}, {100}, {90} };
    cout << "===== 정렬 전 DB =====" << endl;
    for (int i = 0; i < SIZE; i++) {
        cout << arr[i].score << " ";
    }
    cout << endl;
    mergeSort(0, 9, arr);
    cout << "===== 정렬 후 DB =====" << endl;
    for (int i = 0; i < SIZE; i++) {
        cout << arr[i].score << " ";
    }
    cout << endl;
}
```

정렬 결과 :

```
===== 정렬 전 DB =====
89 100 45 70 91 98 64 36 100 90
===== 정렬 후 DB =====
36 45 64 70 89 90 91 98 100 100
```


# 2. Merge Sort C++ Code (Multiple Data)

```cpp
#include <iostream>
#define SIZE 10
using namespace std;
// DB에 Field 가 score 1개만 존재
typedef struct _db {
    int score;  // score는 오름차순 정렬
    int height; // score가 같을 경우 height는 내림차순 정렬
}DB;

// Merge Sort는 DB크기와 동일 크기의 공간이 더 필요하다.
// Memory가 부족하면 Quick Sort를 대신 사용한다.
DB tmp[SIZE];

// Combine
void combine(int start, int mid, int end, DB arr[]) {
    int l = start; //   ㅁㅁㅁㅁ  merge할 첫 번째 arr의 index pointer
    int r = mid + 1; //     ㅁㅁㅁㅁ  merge할 두 번째 arr의 index pointer
    int k = start; //   ㅁㅁㅁㅁㅁㅁㅁㅁ merge결과를 저장할 tmp의 index pointer

    // merge할 두개의 arr 중 하나라도 끝날 때 까지
    while ((l <= mid) && (r <= end)) {
        // DB의 비교가능 field 가 height 2개가 존재
        // score는 오름차순 정렬
        if (arr[l].score < arr[r].score)
            tmp[k++] = arr[l++];
        else if (arr[l].score > arr[r].score)
            tmp[k++] = arr[r++];
        else { // if(arr[l].score == arr[r].score)
            if (arr[l].height >= arr[r].height)
                tmp[k++] = arr[l++];
            else
                tmp[k++] = arr[r++];
        }
    }

    // 남은 db를 모두 다 순서대로 저장한다.
    if (l <= mid) {
        while (l <= mid) {
            tmp[k++] = arr[l++];
        }
    }
    else {
        while (r <= end) {
            tmp[k++] = arr[r++];
        }
    }

    // 정렬된 tmp 를 DB에 다시 복사한다.
    for (int i = start; i <= end; i++) {
        arr[i] = tmp[i];
    }
}

// MergeSort
void mergeSort(int start, int end, DB arr[]) {
    // 정렬할 DB가 2개 이상일 경우에 recursive하게 merge sort를 동작한다
    if (start < end) {
        // DB의 data를 반으로 나눈다 
        int mid = (start + end) / 2;
        mergeSort(start, mid, arr);
        mergeSort(mid + 1, end, arr);
        combine(start, mid, end, arr);
    }
}
// main
void main() {
    DB arr[SIZE] = { {80, 165}, {100, 182}, {90, 170}, {100, 193}, {100, 169}, {100, 183}, {64, 177}, {100, 179}, {100, 195}, {90, 173} };
    cout << "===== 정렬 전 DB =====" << endl;
    for (int i = 0; i < SIZE; i++) {
        cout << "(" << arr[i].score << "," << arr[i].height << ") ";
    }
    cout << endl;
    mergeSort(0, 9, arr);
    cout << "===== 정렬 후 DB =====" << endl;
    for (int i = 0; i < SIZE; i++) {
        cout << "(" << arr[i].score << "," << arr[i].height << ") ";
    }
    cout << endl;
}
```

정렬 결과 :

```bash
===== 정렬 전 DB =====
(80,165) (100,182) (90,170) (100,193) (100,169) (100,183) (64,177) (100,179) (100,195) (90,173)
===== 정렬 후 DB =====
(64,177) (80,165) (90,173) (90,170) (100,195) (100,193) (100,183) (100,182) (100,179) (100,169)
```
---
# Reference   
1. [https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91\_%EC%A0%95%EB%A0%AC)   
2. [https://www.youtube.com/watch?v=QAyl79dCO_k](https://www.youtube.com/watch?v=QAyl79dCO_k)   
