---
title: "우선순위큐, Prioriry Queue C++ Sample Code, [STL] std::priority_queue, 이진힙, Binary heap C++ Sample Code" 
header:
  # image: /assets/images/koin.jpg
categories:
  - Coding Interview
tags:
  - Algorithm
  - C++
  - 우선순위큐
  - Priority Queue
  - 이진힘
  - Binary Heap
  - STL
  - std::priority_queue
toc: true
last_modified_at: 2021-03-08
use_math: true
---
# 1. std::priority_queue container 간략 설명
<br/>
<div>
<a href="https://en.cppreference.com/w/cpp/container/priority_queue" class="bookmark source">
	<div class="bookmark-info">
		<div class="bookmark-text">
			<div class="bookmark-title">std::priority_queue</div>
			<div class="bookmark-description">A priority queue is a container adaptor that provides
				constant time
				lookup of the largest (by default) element, at the expense of logarithmic insertion and
				extraction.
				A user-provided Compare can be supplied to change the ordering, e.g. using would cause
				the smallest
				element to appear as the .</div>
		</div>
		<div class="bookmark-href"><img src="https://en.cppreference.com/favicon.ico"
				class="icon bookmark-icon" />https://en.cppreference.com/w/cpp/container/priority_queue
		</div>
	</div>
</a>
</div>
<br/>
Priority Queue 는 키 노드 중에서 키값이 가장 큰 노드나 키 값이 가장 작은 노드를 찾기 위해서 만든 자료구조로 이진힙(Binary Heap)형태로 구현할 수 있다. 

 가장 큰 값을 바로 찾을 수 있는 Max Heap, 가장 작은 값을 바로 찾을 수 있는 Min Heap 두 가지 형태로 구현 가능하며 자세한 알고리즘은 다음을 참고 하면 된다.

<br/>
<div>
<a href="https://en.wikipedia.org/wiki/Binary_heap"
					class="bookmark source">
					<div class="bookmark-info">
						<div class="bookmark-text">
							<div class="bookmark-title">Binary heap</div>
							<div class="bookmark-description">A binary heap is a heap data structure that takes the form
								of a binary
								tree. Binary heaps are a common way of implementing priority queues. The binary heap was
								introduced
								by J. W. J. Williams in 1964, as a data structure for heapsort.</div>
						</div>
						<div class="bookmark-href"><img src="https://en.wikipedia.org/static/favicon/wikipedia.ico"
								class="icon bookmark-icon" />https://en.wikipedia.org/wiki/Binary_heap</div>
					</div><img
						src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Max-Heap.svg/1200px-Max-Heap.svg.png"
						class="bookmark-image" />
				</a>
</div>
<br/>
 역시 알고리즘을 가장 이해하기 쉬운 방법은 영상을 참고하는 방법!
<br/>
<div>
<a href="https://www.youtube.com/watch?v=jfwjyJvbbBI"	class="bookmark source">
	<div class="bookmark-info">
		<div class="bookmark-text">
			<div class="bookmark-title">[자료구조 알고리즘] Binary Heaps (Min-Heaps and Max-Heaps)</div>
			<div class="bookmark-description">선행학습자료]Tree의 종류 https://youtu.be/LnxEBW29DOwBinary Tree의
				3가지 순회방법 구현하기
				https://youtu.be/QN1rZYX6QaA</div>
		</div>
		<div class="bookmark-href"><img src="https://www.youtube.com/s/desktop/bda3c6ba/img/favicon.ico"
				class="icon bookmark-icon" />https://www.youtube.com/watch?v=jfwjyJvbbBI</div>
	</div><img src="https://i.ytimg.com/vi/jfwjyJvbbBI/hqdefault.jpg" class="bookmark-image" />
</a>
</div>
<br/>
Binary Heap의 알고리즘 복잡도는 다음과 같다.

| 알고리즘   | 평균복잡도 | 최악의경우 |
| ---------- | ---------- | ---------- |
| 공간복잡도 | $O(n)$     | $O(n)$     |
| 삽입       | $O(1)$     | $O(logn)$  |
| 검색       | $O(1)$     | $O(1)$     |
| 삭제       | $O(logn)$  | $O(logn)$  |

 std::priority_queue가 지원하는 여러 함수 중에 우리가 구현 할 4개의 함수는 다음과 같다.

| Member Functions | Description                 |
| ---------------- | --------------------------- |
| top              | 가장 상위 요소에 접근       |
| push             | 요소를 삽입하고 내부를 정렬 |
| pop              | 가장 상위 요소를 삭제       |
| empty            | 비어있는지 확인             |

그럼 이제 위의 함수들의 실제 sample code를 사용해보자.

```cpp
#include <iostream>
#include <queue>

using namespace std;

void main() {
    priority_queue<int> PQ;
    const auto data = { 5, 4, 6, 2, 3, 1 };
    for (int n : data) {
        PQ.push(n);
    }
    cout << "===== Priority Queue : Max Heap =====" << endl;
    while (!PQ.empty()) {
        cout << PQ.top() << " ";
        PQ.pop();
    }
}
```

결과 화면 :

```
===== Priority Queue : Max Heap =====
6 5 4 3 2 1
```

# 2. Priority Queue C++ Sample Code, Binary Heap C++ Sample Code

```cpp
#include <iostream>
#define SWAP(T, x, y){T t;t = x;x = y;y = t;}

using namespace std;

class _priority_queue {
private:
    int capacity;
    int* arr;
    int size;
public:
    _priority_queue(int capa);
    ~_priority_queue();
    bool empty();
    int top();
    void push(int val);
    void pop();
};

_priority_queue::_priority_queue(int capa)
{
    capacity = capa;
    size = 0;
    arr = new int[capacity];
}

_priority_queue::~_priority_queue()
{
    delete arr;
}

bool _priority_queue::empty()
{
    return size == 0 ? true : false;
}

int _priority_queue::top()
{
    return arr[0];
}

void _priority_queue::push(int val)
{
    if (size == capacity)
        return;
    // Heap은 완전 이진 트리 이므로 마지막 요소에 삽입
    int cur = size;
    arr[size++] = val;
    // root 까지 비교해서 부모보다 크면 swap
    while (cur > 0) {
        int parent = (cur - 1) / 2;
        if (arr[cur] > arr[parent]) {
            SWAP(int, arr[cur], arr[parent]);
        }
        else {
            break;
        }
        cur = parent;
    }
}

void _priority_queue::pop()
{
    if (empty()) {
        return;
    }
    // 맨 마지막 요소를 root로 가져오고 size를 1개 줄인다.
    SWAP(int, arr[size - 1], arr[0]);
    size--;
    // pop은 root부터 시작
    int cur = 0;
    // left child 가 size 보다 작을 때까지 - 즉 child node가 없는 tree 끝까지
    while ((cur * 2 + 1) < size) {
        int lc = cur * 2 + 1;   // left child
        int rc = cur * 2 + 2;   // right child
        int child;
        // tree의 마지막 child node가 left만 존재 할 경우
        if (rc == size) {
            child = lc;
        }
        // child가 모두 존재하면 둘중에 큰 노드 선택 - min heap일경우는 작은 노드 선택
        else {
            child = arr[lc] > arr[rc] ? lc : rc;
        }

        if (arr[cur] > arr[child]) {
            break;
        }
        SWAP(int, arr[cur], arr[child]);
        cur = child;
    }
}

void main() {
    _priority_queue* PQ = new _priority_queue(10);
    const auto data = { 5, 4, 6, 2, 3, 1 };
    for (int n : data) {
        PQ->push(n);
    }
    cout << "===== Priority Queue : Max Heap =====" << endl;
    while (!PQ->empty()) {
        cout << PQ->top() << " ";
        PQ->pop();
    }
}
```

결과 화면 : 

```cpp
===== Priority Queue : Max Heap =====
6 5 4 3 2 1
```
# 3. Search, Lazy Deletion 

Priority Queie에서 종종 특정 data의 값을 업데이트 한다거나 삭제할 경우가 발생한다.
하지만 그 데이터수가 많을 경우에 모든 데이터를 pop해서 값을 update 하거나 삭제한 뒤 다시 push하는 방식은
너무 바보 같은 짓이므로 다음과 같이 id 와 heap index 를 연결하여 $O(1)$의 복잡도로 값을 변경하거나 삭제 가능하다.
Lazy Deletion은 특정 node에 삭제 flag를 두어 나중에 top 검색 시 이미 삭제된 node는 pop하는 방식으로 동작하게 된다.

추가로 구현 할 2개의 함수는 다음과 같다.

| Member Functions | Description                 | 복잡도 |
| ---------------- | --------------------------- | ------ |
| replace          | 가장 상위 요소에 접근       | $O(1)$ |
| remove           | 요소를 삽입하고 내부를 정렬 | $O(1)$ |

```cpp
#include <iostream>
#define ROOT 0
#define SWAP(T, x, y){T t;t=x;x=y;y=t;}

#define MAX 50000
using namespace std;

typedef struct _node {
    bool deleted;
    int id;
    int val;
}Node;

//cache db
Node db[MAX];
//node의 id가 heap tree에서 어디에 위치하는지 확인
int id2db[MAX];

class PQ {
private:
    int _size;
    int P(int i) { return (i - 1) / 2; }
    int LC(int i) { return (i * 2) + 1; }
    int RC(int i) { return (i * 2) + 2; }
public:
    PQ() { init(); }
    ~PQ() {}
    void init();
    bool empty();
    int size();
    Node top();
    void pop();
    void push(int id, int val);
    void update(int index);
    void downdate(int index);
    void replace(int id, int newVal);
    void remove(int id);
};

void PQ::init()
{
    _size = 0;
}

bool PQ::empty()
{
    return (_size == 0);
}

int PQ::size()
{
    return _size;
}

Node PQ::top()
{
    while (db[ROOT].deleted) {
        pop();
    }
    return db[ROOT];
}

void PQ::pop()
{
    // 1. range check
    if (empty()) {
        cout << "Error" << endl;
        return;
    }
    // 2. 노드의 처음과 마지막을 swap 하고 size를 하나 줄인다.
    SWAP(int, id2db[db[ROOT].id], id2db[db[_size - 1].id]);
    SWAP(Node, db[ROOT], db[_size - 1]);
    _size -= 1;
    int cur = ROOT;
    downdate(cur);
}

void PQ::push(int id, int val)
{
    // 1. range check
    if (_size + 1 > MAX) {
        cout << "Error" << endl;
        return;
    }
    // 2. 노드의 마지막에 값을 넣고 비교하면서 올린다.
    // max heap 구현
    int cur = _size;
    db[cur].val = val;
    db[cur].id = id;
    db[cur].deleted = false;
    id2db[id] = cur;
    _size++;
    update(cur);
}

void PQ::update(int index)
{
    int cur = index;
    while (cur > ROOT) {
        if (db[P(cur)].val > db[cur].val) {
            break;
        }
        else {
            SWAP(int, id2db[db[cur].id], id2db[db[P(cur)].id]);
            SWAP(Node, db[cur], db[P(cur)]);
        }
        cur = P(cur);
    }
}

void PQ::downdate(int index)
{
    int cur = index;
    // child node 가 있을때까지 == left child가 size보다 작을 때까지
    while (LC(cur) < _size) {
        int child;
        // left child 만 있으므로 child 는 left child
        if (RC(cur) == _size) {
            child = LC(cur);
        }
        // max heap 이므로 큰놈
        else {
            child = db[LC(cur)].val > db[RC(cur)].val ? LC(cur) : RC(cur);
        }
        // child 보다 크면 끝
        if (db[cur].val > db[child].val) {
            break;
        }
        else {
            SWAP(int, id2db[db[cur].id], id2db[db[child].id]);
            SWAP(Node, db[cur], db[child]);
        }
        cur = child;
    }
}

void PQ::replace(int id, int newVal)
{
    int cur = id2db[id];
    db[cur].val = newVal;
    update(cur);
    downdate(cur);
}

void PQ::remove(int id)
{
    int cur = id2db[id];
    db[cur].deleted = true;
}

void main() {
    PQ pq;
    pq.push(100, 10);
    pq.push(101, 5);
    pq.push(200, 6);
    pq.push(201, 7);
    pq.push(300, 8);
    pq.push(301, 9);
    pq.push(400, 4);
    pq.push(401, 1);
    pq.push(500, 2);
    pq.push(501, 3);

    for (register int i = 0; i < pq.size(); i++) {
        cout << "id : " << db[i].id << ", val : " << db[i].val << ", loc : " << id2db[db[i].id] << ", deleted : " << db[i].deleted << endl;
    }

    pq.replace(501, 100);
    cout << "501 replace new value to 100" << endl;
    for (register int i = 0; i < pq.size(); i++) {
        cout << "id : " << db[i].id << ", val : " << db[i].val << ", loc : " << id2db[db[i].id] << ", deleted : " << db[i].deleted << endl;
    }

    pq.replace(400, 200);
    cout << "501 replace new value to 100" << endl;
    for (register int i = 0; i < pq.size(); i++) {
        cout << "id : " << db[i].id << ", val : " << db[i].val << ", loc : " << id2db[db[i].id] << ", deleted : " << db[i].deleted << endl;
    }

    pq.replace(201, 200);
    cout << "501 replace new value to 100" << endl;
    for (register int i = 0; i < pq.size(); i++) {
        cout << "id : " << db[i].id << ", val : " << db[i].val << ", loc : " << id2db[db[i].id] << ", deleted : " << db[i].deleted << endl;
    }

    cout << "remove 300" << endl;
    pq.remove(300);
    for (register int i = 0; i < pq.size(); i++) {
        cout << "id : " << db[i].id << ", val : " << db[i].val << ", loc : " << id2db[db[i].id] << ", deleted : " << db[i].deleted << endl;
    }
    cout << "remove 201" << endl;
    pq.remove(201);
    for (register int i = 0; i < pq.size(); i++) {
        cout << "id : " << db[i].id << ", val : " << db[i].val << ", loc : " << id2db[db[i].id] << ", deleted : " << db[i].deleted << endl;
    }
    cout << "remove 200" << endl;
    pq.remove(200);
    for (register int i = 0; i < pq.size(); i++) {
        cout << "id : " << db[i].id << ", val : " << db[i].val << ", loc : " << id2db[db[i].id] << ", deleted : " << db[i].deleted << endl;
    }

    while (!pq.empty()) {
        cout << "Pop info - id : " << pq.top().id << ", val : " << pq.top().val << ", loc : " << id2db[pq.top().id] << ", deleted : " << pq.top().deleted << endl;
        pq.pop();
    }
}
```
# 4. Reference

1. [https://en.cppreference.com/w/cpp/container/priority_queue](https://en.cppreference.com/w/cpp/container/priority_queue)
2. [https://en.wikipedia.org/wiki/Binary_heap](https://en.wikipedia.org/wiki/Binary_heap)
3. [https://www.youtube.com/watch?v=jfwjyJvbbBI](https://www.youtube.com/watch?v=jfwjyJvbbBI)