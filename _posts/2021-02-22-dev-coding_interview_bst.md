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

| Member Functions | Description                                       |
| ---------------- | ------------------------------------------------- |
| insert           | 값을 삽입합니다.                                  |
| erase            | 값을 삭제합니다.                                  |
| find             | 특정 key에 매칭된 값을 찾습니다.                  |
| lower_bound      | 주어진 key 보다 같거나 큰 첫번째 요소를 찾습니다. |
| upper_bound      | 주어진 key 보다 큰 첫번째 요소를 찾습니다.        |

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
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << *search << " 검색 성공" << endl;
    }
    else {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << " 검색 실패" << endl;
    }
    cout << endl;
    item = 20;
    search = bst.find(item);
    if (search != bst.end()) {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << *search << " 검색 성공" << endl;
    }
    else {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << " 검색 실패" << endl;
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
 검색 실패

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
#include <iostream>
#include <string>

using namespace std;

typedef struct _node {
    int key;
    _node* p;   // parent node
    _node* rc;  // right child node
    _node* lc;  // left child node
}Node;

class BST {
private:
    Node* root;
    void _clear(Node* node);
    void clear();
    Node* createNode(int key);
    void _show(Node* node);
    Node* _find(Node* node, int key);
    void _erase(Node** node, int key);
    Node* getMinNode(Node* node);
    Node* _lower_bound(Node* node, int key);
    Node* _upper_bound(Node* node, int key);
public:
    BST();
    ~BST();
    void insert(int key);
    void show(string str);
    Node* find(int key);
    void erase(int key);
    Node* lower_bound(int key);
    Node* upper_bound(int key);
};

void main() {
    BST* bst = new BST();
    bst->insert(100);
    bst->insert(90);
    bst->insert(80);
    bst->insert(70);
    //// bst는 유일한 key 값을 가지므로 70은 중복 insert 가 되지않는다.
    bst->insert(70);
    bst->insert(60);
    bst->insert(50);
    bst->insert(40);
    bst->show("insert method를 이용한 삽입");

    int item = 70;
    Node* search = bst->find(item);
    if (search != nullptr) {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " ====="  << endl;
        cout << search->key << " 검색 성공" << endl;
    }
    else {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << " 검색 실패" << endl;
    }
    cout << endl;
    item = 20;
    search = bst->find(item);
    if (search != nullptr) {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << search->key << " 검색 성공" << endl;
    }
    else {
        cout << "===== Set Info : find를 이용한 검색 : " << item << " =====" << endl;
        cout << " 검색 실패" << endl;
    }
    cout << endl;
    item = 30;
    bst->erase(item);
    bst->show("erase method를 이용한 삭제 : " + to_string(item) + " ");

    item = 50;
    search = bst->lower_bound(item);
    cout << "===== Set Info : lower_bound를 이용한 50보다 같거나 큰 값 검색 =====" << endl;
    cout << search->key << endl << endl;

    item = 45;
    search = bst->lower_bound(item);
    cout << "===== Set Info : lower_bound를 이용한 45보다 같거나 큰 값 검색 =====" << endl;
    cout << search->key << endl << endl;

    item = 50;
    search = bst->upper_bound(item);
    cout << "===== Set Info : upper_bound 를 이용한 50보다 큰 값 검색 =====" << endl;
    cout << search->key << endl << endl;

    item = 45;
    search = bst->upper_bound(item);
    cout << "===== Set Info : upper_bound 를 이용한 45보다 큰 값 검색 =====" << endl;
    cout << search->key << endl << endl;
}

// postorder traversal 로 모든 node를 삭제한다.
void BST::_clear(Node* node)
{
    if (node != nullptr) {
        _clear(node->lc);
        _clear(node->rc);
        delete node;
    }
}

void BST::clear()
{
    _clear(root);
    root = nullptr;
}

Node* BST::createNode(int key)
{
    Node* newNode = new Node;
    newNode->key = key;
    newNode->p = newNode->rc = newNode->lc = nullptr;
    return newNode;
}

void BST::insert(int key)
{
    Node* newNode = createNode(key);
    if (root == nullptr) {
        root = newNode;
        return;
    }
    // leaf node 가 null 인 순간까지 내려간다.
    Node* cur = root;
    while (cur != nullptr) {
        newNode->p = cur;
        if (key < cur->key)
            cur = cur->lc;
        else if (key > cur->key)
            cur = cur->rc;
        else
            return; // 유일한 key 값을 가지므로 같은 key 값이면 종료
    }
    // newNode의 parent를 저장해 두었으므로 값을 비교하여 작으면 왼쪽 크면 오른쪽에 node 생성
    if (key < newNode->p->key)
        newNode->p->lc = newNode;
    else
        newNode->p->rc = newNode;


}

// inorder traversal 로 모든 node를 오름차순으로 보여줌
void BST::_show(Node* node)
{
    if (node != nullptr) {
        _show(node->lc);
        cout << node->key << endl;
        _show(node->rc);
    }
}

Node* BST::_find(Node* node, int key)
{
    if (node != nullptr) {
        if (key < node->key)
            return _find(node->lc, key);
        else if (key > node->key)
            return _find(node->rc, key);
        else
            return node;
    }
    return nullptr;
}

void BST::_erase(Node** node, int key)
{
    Node* cur = *node;
    if (cur != nullptr) {
        if (key < cur->key)
            _erase(&(cur->lc), key);
        else if (key > cur->key)
            _erase(&(cur->rc), key);
        else {
            // 1. 자식 node 가 하나도 없는 경우
            if ((cur->lc == nullptr) && (cur->rc == nullptr)) {
                // 현재 node 가 root node일 경우
                if (cur->p == nullptr) {
                    root = nullptr;
                }
                else {
                    // 부모 node의 자식 node 정보를 갱신
                    if (cur->key < cur->p->key)
                        cur->p->lc = nullptr;
                    else
                        cur->p->rc = nullptr;
                }
                delete cur;
            }
            // 2. 왼쪽 자식 node만 있는 경우
            else if ((cur->lc != nullptr) && (cur->rc == nullptr)) {
                // 현재 node 가 root node일 경우
                // 왼쪽 자식 node가 root node가 된다.
                if (cur->p == nullptr) {
                    root = cur->lc;
                    root->p = nullptr;
                }
                else {
                    // 왼쪽 자식 node와 부모 node를 이어준다
                    if (cur->key < cur->p->key) {
                        cur->p->lc = cur->lc;
                        cur->lc->p = cur->p;
                    }
                    else {
                        cur->p->rc = cur->lc;
                        cur->lc->p = cur->p;
                    }
                        
                }
                delete cur;
            }
            // 3. 오른쪽 자식 node만 있는 경우
            else if ((cur->lc == nullptr) && (cur->rc != nullptr)) {
                // 현재 node 가 root node일 경우
                // 오른쪽 자식 node가 root node가 된다.
                if (cur->p == nullptr) {
                    root = cur->rc;
                    root->p = nullptr;
                }
                else {
                    // 오른쪽 자식 node와 부모 node를 이어준다
                    if (cur->key < cur->p->key) {
                        cur->p->lc = cur->rc;
                        cur->rc->p = cur->p;
                    }
                    else {
                        cur->p->rc = cur->rc;
                        cur->rc->p = cur->p;
                    }
                }
                delete cur;
            }
            // 4. 양쪽 자식 node가 모두 있는 경우
            else if ((cur->lc == nullptr) && (cur->rc == nullptr)) {
                // 오른쪽 자식 node 에서 가장 작은 node를 찾는다.
                Node* minNode = getMinNode(cur->rc);
                // 찾은 node를 삭제하고 현재 자리에 그 key값을 삽입한다.
                int key = minNode->key;
                _erase(&(cur->rc), key);
                cur->key = key;
            }
        }
    }
}

Node* BST::getMinNode(Node* node)
{
    Node* cur = node;
    while (cur->lc != nullptr)
        cur = cur->lc;
    return cur;
}

Node* BST::_lower_bound(Node* node, int key)
{
    Node* cur = root;
    Node* minNode = nullptr;
    while (cur != nullptr) {
        // key 값이 같으면 해당 node return
        if (key == cur->key)
            return cur;
        // key 값이 현재 node 보다 작으면
        else if (key < cur->key) {
            // 현재 node가 가장 왼쪽의 node, 즉 key 보다 큰 마지막 node이므로 return
            if (cur->lc == nullptr)
                return cur;
            // 현재까지 검사한 node 중 key보단 크지만 가장 작은 node 이므로 저장
            minNode = cur;
            cur = cur->lc;
        }
        else if (key > cur->key) {
            // 현재 node 가 마지막 node 이므로 지금 까지 저장한 node 중 가작 작은 node return
            if (cur->rc == nullptr) {
                return minNode;
            }
            cur = cur->rc;
        }
    }
    return minNode;
}

Node* BST::_upper_bound(Node* node, int key)
{
    Node* cur = root;
    Node* minNode = nullptr;
    while (cur != nullptr) {
        // key 값이 현재 node 보다 작으면
        if (key < cur->key) {
            // 현재 node가 가장 왼쪽의 node, 즉 key 보다 큰 마지막 node이므로 return
            if (cur->lc == nullptr)
                return cur;
            // 현재까지 검사한 node 중 key보단 크지만 가장 작은 node 이므로 저장
            minNode = cur;
            cur = cur->lc;
        }
        else if (key >= cur->key) {
            // 현재 node 가 마지막 node 이므로 지금 까지 저장한 node 중 가작 작은 node return
            if (cur->rc == nullptr) {
                return minNode;
            }
            cur = cur->rc;
        }
    }
    return minNode;
}

void BST::show(string str)
{
    cout << "===== Set Info : " << str.c_str() << " =====" << endl;
    _show(root);
    cout << endl << endl;
}

Node* BST::find(int key)
{
    return _find(root, key);
}

void BST::erase(int key)
{
    _erase(&root, key);
}

Node* BST::lower_bound(int key)
{
    return _lower_bound(root, key);
}

Node* BST::upper_bound(int key)
{
    return _upper_bound(root, key);
}

BST::BST()
{
    clear();
}

BST::~BST()
{
    clear();
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
 검색 실패

===== Set Info : erase method를 이용한 삭제 : 30  =====
40
50
60
70
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

---

# Reference

1. [https://en.cppreference.com/w/cpp/container/set](https://en.cppreference.com/w/cpp/container/set)
2. [https://en.wikipedia.org/wiki/Binary_search_tree](https://en.wikipedia.org/wiki/Binary_search_tree)
3. [https://www.youtube.com/watch?v=LnxEBW29DOw](https://www.youtube.com/watch?v=LnxEBW29DOw)
4. [https://www.youtube.com/watch?v=QN1rZYX6QaA](https://www.youtube.com/watch?v=QN1rZYX6QaA)
5. [https://www.youtube.com/watch?v=9ZZbA2iPjtM](https://www.youtube.com/watch?v=9ZZbA2iPjtM)
6. [https://www.youtube.com/watch?v=xxADG17SveY](https://www.youtube.com/watch?v=xxADG17SveY)