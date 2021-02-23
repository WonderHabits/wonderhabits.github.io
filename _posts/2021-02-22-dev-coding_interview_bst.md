---
title: "이진 검색 트리, Binary Search Tree C++ Sample Code, [STL] std::set" 
header:
  # image: /assets/images/koin.jpg
categories:
  - Coding Interview
tags:
  - Algorithm
  - C++
  - Binary Search Tree
  - 이진 검색 트리
  - STL
  - std::set
toc: true
last_modified_at: 2021-02-22
use_math: true
---
# 1. std::set container 간략 설명
<br/>
<div>
<a href="https://en.cppreference.com/w/cpp/container/set"
		class="bookmark source">
		<div class="bookmark-info">
			<div class="bookmark-text">
				<div class="bookmark-title">std::set</div>
				<div class="bookmark-description">std::set is an associative container that contains a sorted set of
					unique objects of type Key. Sorting is done using the key comparison function . Search, removal, and
					insertion operations have logarithmic complexity. Sets are usually implemented as red-black trees.
					Everywhere the standard library uses the requirements, uniqueness is determined by using the
					equivalence relation.</div>
			</div>
			<div class="bookmark-href"><img src="https://en.cppreference.com/favicon.ico"
					class="icon bookmark-icon" />https://en.cppreference.com/w/cpp/container/set</div>
		</div>
	</a>
</div>
<br/>
std::set은 정렬된 고유한 key 값을 갖는 container이다. 

내부적으로 BST(Binary Search Tree, 이진트리)로 구현되어있다.
<br/>
<div>
<a href="https://en.wikipedia.org/wiki/Binary_search_tree"
					class="bookmark source">
					<div class="bookmark-info">
						<div class="bookmark-text">
							<div class="bookmark-title">Binary search tree</div>
							<div class="bookmark-description">In computer science, a binary search tree ( BST), also
								called an
								ordered or sorted binary tree, is a rooted binary tree whose internal nodes each store a
								key greater
								than all the keys in the node&#x27;s left subtree and less than those in its right
								subtree.</div>
						</div>
						<div class="bookmark-href"><img src="https://en.wikipedia.org/static/favicon/wikipedia.ico"
								class="icon bookmark-icon" />https://en.wikipedia.org/wiki/Binary_search_tree</div>
					</div><img
						src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Binary_search_tree.svg/1200px-Binary_search_tree.svg.png"
						class="bookmark-image" />
				</a>
</div>
<br/>
아래의 표와 같이 검색, 삽입, 제거 모두 평균 $O(nlogn)$의 복잡도를 가지고 있는 Data Structure 의 일종이다. 각각의 노드는 왼쪽의 자식 노드들 보다는 크고 오른쪽 자식 노드들 보다는 작은 키를 저장하는 이진 검색 트리이다.

| 알고리즘   | 평균복잡도 | 최악의경우 |
| ---------- | ---------- | ---------- |
| 공간복잡도 | $O(n)$     | $O(n)$     |
| 검색       | $O(nlogn)$ | $O(n)$     |
| 삽입       | $O(nlogn)$ | $O(n)$     |
| 삭제       | $O(nlogn)$ | $O(n)$     |

자세한 내용은 아래 영상들을 참고하면 된다.
<br/>
<div>
<a href="https://www.youtube.com/watch?v=LnxEBW29DOw"
					class="bookmark source">
					<div class="bookmark-info">
						<div class="bookmark-text">
							<div class="bookmark-title">[자료구조 알고리즘] Tree의 종류</div>
						</div>
						<div class="bookmark-href"><img src="https://www.youtube.com/s/desktop/a4d390aa/img/favicon.ico"
								class="icon bookmark-icon" />https://www.youtube.com/watch?v=LnxEBW29DOw</div>
					</div><img src="https://i.ytimg.com/vi/LnxEBW29DOw/hqdefault.jpg" class="bookmark-image" />
				</a>
</div>
<br/>
<div>
<a href="https://www.youtube.com/watch?v=QN1rZYX6QaA"
					class="bookmark source">
					<div class="bookmark-info">
						<div class="bookmark-text">
							<div class="bookmark-title">[자료구조 알고리즘] Binary Tree의 3가지 순회방법 구현하기</div>
							<div class="bookmark-description">선행학습자료]Tree의 종류 https://youtu.be/LnxEBW29DOw</div>
						</div>
						<div class="bookmark-href"><img src="https://www.youtube.com/s/desktop/a4d390aa/img/favicon.ico"
								class="icon bookmark-icon" />https://www.youtube.com/watch?v=QN1rZYX6QaA</div>
					</div><img src="https://i.ytimg.com/vi/QN1rZYX6QaA/hqdefault.jpg" class="bookmark-image" />
				</a>
</div>
<br/>
<div>
<a href="https://www.youtube.com/watch?v=9ZZbA2iPjtM"
					class="bookmark source">
					<div class="bookmark-info">
						<div class="bookmark-text">
							<div class="bookmark-title">[자료구조 알고리즘] 배열을 이진검색트리로 만들기 in Java</div>
							<div class="bookmark-description">선행학습자료]Tree의 종류 https://youtu.be/LnxEBW29DOwBinary Tree의
								3가지 순회방법 구현하기
								https://youtu.be/QN1rZYX6QaABinary Heaps (Min-Heaps and Max-Heaps) https://youtu.be/j...
							</div>
						</div>
						<div class="bookmark-href"><img src="https://www.youtube.com/s/desktop/a4d390aa/img/favicon.ico"
								class="icon bookmark-icon" />https://www.youtube.com/watch?v=9ZZbA2iPjtM</div>
					</div><img src="https://i.ytimg.com/vi/9ZZbA2iPjtM/hqdefault.jpg" class="bookmark-image" />
				</a>
</div>
<br/>
<div>
<a href="https://www.youtube.com/watch?v=xxADG17SveY"
					class="bookmark source">
					<div class="bookmark-info">
						<div class="bookmark-text">
							<div class="bookmark-title">[자료구조 알고리즘] BST insertion/deletion</div>
						</div>
						<div class="bookmark-href"><img src="https://www.youtube.com/s/desktop/a4d390aa/img/favicon.ico"
								class="icon bookmark-icon" />https://www.youtube.com/watch?v=xxADG17SveY</div>
					</div><img src="https://i.ytimg.com/vi/xxADG17SveY/hqdefault.jpg" class="bookmark-image" />
				</a>
</div>
 std::unordered_map이 지원하는 여러 함수 중에 우리가 구현 할 2개의 함수는 다음과 같다.

|Member Functions|Description|
|insert|값을 삽입합니다.|
|erase|값을 삭제합니다.|
|find|특정 key에 매칭된 값을 찾습니다.|
|lower_bound|주어진 key 보다 같거나 큰 첫번째 요소를 찾습니다.|
|upper_bound|주어진 key 보다 큰 첫번째 요소를 찾습니다.|

그럼 이제 위의 함수들의 실제 sample code를 사용해보자.

```cpp
#include <iostream>
#include <set>
#include <string>

using namespace std;

void show(set<int> bst, string str) {
    cout << "===== Set Info : " << str.c_str() << " =====" << endl;
    for (auto item : bst) {
        cout << item << " " << endl;
    }
    cout << endl;
}

void main() {
    set<int> bst;
    bst.insert(100);
    bst.insert(90);
    bst.insert(80);
    bst.insert(70);
    // bst는 유일한 key 값을 가지므로 70은 중복 insert 가 되지않는다.
    bst.insert(70);
    bst.insert(60);
    bst.insert(50);
    bst.insert(40);
    show(bst, "insert method를 이용한 삽입");

    int item = 70;
    auto search = bst.find(item);
    if (search != bst.end()) {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " ====="  << endl;
        cout << item << " 검색 성공" << endl;
    }
    else {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << item << " 검색 실패" << endl;
    }
    cout << endl;
    item = 20;
    search = bst.find(item);
    if (search != bst.end()) {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << item << " 검색 성공" << endl;
    }
    else {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << item << " 검색 실패" << endl;
    }
    cout << endl;
    item = 70;
    bst.erase(item);
    show(bst, "erase method를 이용한 삭제 : " + to_string(item) + " ");

    item = 50;
    search = bst.lower_bound(item);
    cout << "===== Set Info : lower_bound를 이용한 50보다 같거나 큰 값 검색 =====" << endl;
    cout << *search << endl << endl;

    item = 45;
    search = bst.lower_bound(item);
    cout << "===== Set Info : lower_bound를 이용한 45보다 같거나 큰 값 검색 =====" << endl;
    cout << *search << endl << endl;

    item = 50;
    search = bst.upper_bound(item);
    cout << "===== Set Info : upper_bound 를 이용한 50보다 큰 값 검색 =====" << endl;
    cout << *search << endl << endl;

    item = 45;
    search = bst.upper_bound(item);
    cout << "===== Set Info : upper_bound 를 이용한 45보다 큰 값 검색 =====" << endl;
    cout << *search << endl << endl;
}
```

결과 :

```
===== Set Info : insert method를 이용한 삽입 =====
40
50
60
70
80
90
100

===== Set Info : find를 이용한 검색 : 70 =====
70 검색 성공

===== Set Info : find를 이용한 검색 : 20 =====
20 검색 실패

===== Set Info : erase method를 이용한 삭제 : 70  =====
40
50
60
80
90
100

===== Set Info : lower_bound를 이용한 50보다 같거나 큰 값 검색 =====
50

===== Set Info : lower_bound를 이용한 45보다 같거나 큰 값 검색 =====
50

===== Set Info : upper_bound 를 이용한 50보다 큰 값 검색 =====
60

===== Set Info : upper_bound 를 이용한 45보다 큰 값 검색 =====
50
```

# 2. Binary Search Tree C++ Sample Code

그럼 이제 Binary Search Tree Sample Code를 살펴보자

```cpp

```

결과 :

```

```

---

# Reference

1. [https://en.cppreference.com/w/cpp/container/set](https://en.cppreference.com/w/cpp/container/set)
2. [https://en.wikipedia.org/wiki/Binary_search_tree](https://en.wikipedia.org/wiki/Binary_search_tree)
3. [https://www.youtube.com/watch?v=LnxEBW29DOw](https://www.youtube.com/watch?v=LnxEBW29DOw)
4. [https://www.youtube.com/watch?v=QN1rZYX6QaA](https://www.youtube.com/watch?v=QN1rZYX6QaA)
5. [https://www.youtube.com/watch?v=9ZZbA2iPjtM](https://www.youtube.com/watch?v=9ZZbA2iPjtM)
6. [https://www.youtube.com/watch?v=xxADG17SveY](https://www.youtube.com/watch?v=xxADG17SveY)