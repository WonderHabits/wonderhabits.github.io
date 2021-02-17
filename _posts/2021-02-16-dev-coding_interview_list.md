---
title: "[STL] List container구현 (C++)"
header:
  # image: /assets/images/koin.jpg
categories:
  - Coding Interview
tags:
  - Dev
  - Algorithm
  - C++
toc: true
last_modified_at: 2021-02-16
---
# 1. std::list container 간략 설명

 std::list는 어느 위치에서든 요소를 일정한 시간 삽입 및 제거할 수 있도록 지원하는 STL container종류 중 하나이다

 일반적으로 doubly linked list로 구현이 된다.

 linked list의 자세한 내용은 아래 영상을 참고하면 된다.

[[자료구조 알고리즘] Linked List 개념](https://www.youtube.com/watch?v=DzGnME1jIwY&amp;list=PLjSkJdbr_gFZQp0KEoo0Y4KkCI5YqxtjZ&amp;index=1)   
[<img src="https://i.ytimg.com/vi/DzGnME1jIwY/hqdefault.jpg"/>](https://www.youtube.com/watch?v=DzGnME1jIwY&amp;list=PLjSkJdbr_gFZQp0KEoo0Y4KkCI5YqxtjZ&amp;index=1)   

 std::list가 지원하는 여러 함수 중에 우리가 구현 할 7개의 함수는 다음과 같다.
[[STL] List](https://en.cppreference.com/w/cpp/container/list)   

| Member Function | Description                                         |
| --------------- | --------------------------------------------------- |
| push_back       | 지정된 요소 값을 컨테이너 끝에 추가합니다.          |
| push_front      | 지정된 요소 값을 컨테이너의 시작 부분에 추가합니다. |
| pop_back        | 컨테이너의 마지막 요소를 제거합니다.                |
| pop_front       | 컨테이너의 첫번째 요소를 제거합니다.                |
| insert          | 컨테이너의 지정된 위치에 요소를 삽입합니다.         |
| erase           | 지정된 위치의 값을 컨테이너에서 지웁니다.           |
| remove          | 특정값과 같은 요소를 모두 제거합니다.               |

그럼 이제 위의 함수들의 실제 sample code를 사용해보자.

```cpp
#include <iostream>
#include <list>
#include <string>

using namespace std;

void show(list<int> lst, string str) {
    cout << "===== List Info : " << str.c_str() << " =====" <<endl;
    for (auto itr = lst.begin(); itr != lst.end(); itr++) {
        cout << *itr << " ";
    }
    cout << endl;
}

void main() {
    list<int> lst;
    lst.push_back(1);
    lst.push_back(2);
    lst.push_back(3);
    show(lst, "push_back 1, 2, 3");
    lst.push_front(4);
    lst.push_front(5);
    lst.push_front(6);
    show(lst, "push_front 4, 5, 6");
    lst.pop_back();
    show(lst, "pop_back");
    lst.pop_front();
    show(lst, "pop_front");
    auto it = lst.begin();
    for (int i = 0; i < 1; i++)
        it++;
    lst.insert(it, 10);
    show(lst, "insert 10 at second");
    it = lst.begin();
    for (int i = 0; i < 2; i++)
        it++;
    lst.erase(it);
    show(lst, "erase element at third");
    lst.remove(1);
    show(lst, "erase 1");
}
```

결과 :

```
===== List Info : push_back 1, 2, 3 =====
1 2 3
===== List Info : push_front 4, 5, 6 =====
6 5 4 1 2 3
===== List Info : pop_back =====
6 5 4 1 2
===== List Info : pop_front =====
5 4 1 2
===== List Info : insert 10 at second =====
5 10 4 1 2
===== List Info : erase element at third =====
5 10 1 2
===== List Info : erase 1 =====
5 10 2
```

# 2. Doubly linked list 로 구현

```cpp
#include <iostream>
#include <string>

using namespace std;

typedef struct _node {
    _node* prev;
    _node* next;
    int val;
}Node;

class List {
private:
    int size;
    Node* front;
    Node* back;
    void init();
    void release();
    Node* createNode(const int val);
    void deleteNode(Node** node);
    bool isEmpty();

public:
    List();
    ~List();
    void show(string str);
    void push_back(int val);
    void push_front(int val);
    void pop_back();
    void pop_front();
    void insert(int pos, int val);
    void erase(int pos);
    void remove(int val);
};

void main() {
    List lst;
    lst.push_back(1);
    lst.push_back(2);
    lst.push_back(3);
    lst.show("push_back 1, 2, 3");
    lst.push_front(4);
    lst.push_front(5);
    lst.push_front(6);
    lst.show("push_front 4, 5, 6");
    lst.pop_back();
    lst.show("pop_back");
    lst.pop_front();
    lst.show("pop_front");
    lst.insert(0, 10);
    lst.show("insert 10 at second");
    lst.erase(2);
    lst.show("erase element at third");
    lst.remove(1);
    lst.show("erase 1");
}

void List::init()
{
    size = 0;
    front = back = nullptr;
}

void List::release()
{
    size = 0;
    Node* cur = front;
    while (cur != nullptr) {
        Node* tmp = cur;
        cur = cur->next;
        delete tmp;
    }
    front = back = nullptr;
}

Node* List::createNode(const int val)
{
    Node* newNode = new Node;
    newNode->val = val;
    newNode->prev = newNode->next = nullptr;
    return newNode;
}

void List::deleteNode(Node** node)
{
    Node* cur = *node;
    if (cur != nullptr)
        delete cur;
    *node = nullptr;
}

bool List::isEmpty()
{
    // front, end pointer 가 null 일 경우 empty
    // 여기선 간략히 front만 체크
    if (front == nullptr)
        return true;
    return false;
}

List::List()
{
    init();
}

List::~List()
{
    release();
}

void List::show(string str)
{
    cout << "===== List Info : " << str.c_str() << " =====" << endl;
    Node* cur = front;
    while (cur != nullptr) {
        cout << cur->val << " ";
        cur = cur->next;
    }
    cout << endl;
    cur = back;
    while (cur != nullptr) {
        cout << cur->val << " ";
        cur = cur->prev;
    }
    cout << endl;
}

void List::push_back(int val)
{
    Node* newNode = createNode(val);
    // list 가 비어있을 경우 front, back node pointer 에 newNode를 삽입
    if (isEmpty()) {
        front = back = newNode;
    }
    else {
        // back 뒤에 이어주고 back을 newNode로 대체한다.
        back->next = newNode;
        newNode->prev = back;
        back = newNode;
    }
}

void List::push_front(int val)
{
    Node* newNode = createNode(val);
    // list 가 비어있을 경우 front, back node pointer 에 newNode를 삽입
    if (isEmpty()) {
        front = back = newNode;
    }
    else {
        // front 앞에 이어주고 front를 newNode로 대체한다.
        front->prev = newNode;
        newNode->next = front;
        front = newNode;
    }
}

void List::pop_back()
{
    if (!isEmpty()) {
        if (front == back) {
            deleteNode(&front);
            front = back = nullptr;
        }
        else {
            // back node를 back의 prev node로 옮기고 마지막에 남은 node는 지워준다.
            Node* cur = back;
            back = back->prev;
            back->next = nullptr;
            deleteNode(&cur);
        }
    }
}

void List::pop_front()
{
    if (!isEmpty()) {
        if (front == back) {
            deleteNode(&front);
            front = back = nullptr;
        }
        else {
            // front node를 front의 next node로 옮기고 마지막에 남은 node는 지워준다.
            Node* cur = front;
            front = front->next;
            front->prev = nullptr;
            deleteNode(&cur);
        }
    }
}

void List::insert(int pos, int val)
{
    if (!isEmpty()) {
        // cursor Node 를 이동
        Node* cur = front;
        for (int i = 0; i < pos; i++) {
            if (cur == back)
                return;
            cur = cur->next;
        }
        // pos의 바로 뒤에 새로운 노드 삽입
        if (cur == back) {
            push_back(val);
        }
        else {
            Node* newNode = createNode(val);
            Node* prev = cur;
            Node* next = cur->next;
            if(prev != nullptr)
                prev->next = newNode;
            if(next != nullptr)
                next->prev = newNode;
            newNode->prev = prev;
            newNode->next = next;
        }
    }
}

void List::erase(int pos)
{
    if (!isEmpty()) {
        // cursor Node 를 이동
        Node* cur = front;
        for (int i = 0; i < pos; i++) {
            if (cur == back)
                return;
            cur = cur->next;
        }
        if (front == back) {
            delete cur;
            front = back = nullptr;
        }
        else if (cur == front) {
            pop_front();
        }
        else if (cur == back) {
            pop_back();
        }
        else {
            cur->prev->next = cur->next;
            cur->next->prev = cur->prev;
            deleteNode(&cur);
        }
    }
}

void List::remove(int val)
{
    if (!isEmpty()) {
        Node* cur = front;
        while (cur != nullptr) {
            if (val == cur->val) {
                if (front == back) {
                    delete cur;
                    front = back = nullptr;
                    break;
                }
                else if (cur == front) {
                    cur = cur->next;
                    deleteNode(&front);
                    front = cur;
                    front->prev = nullptr;
                }
                else if (cur == back) {
                    back = cur->prev;
                    back->next = nullptr;
                    deleteNode(&cur);
                }
                else {
                    Node* tmp = cur;
                    cur->prev->next = cur->next;
                    cur->next->prev = cur->prev;
                    cur = cur->next;
                    deleteNode(&tmp);
                }
            }
            else {
                cur = cur->next;
            }
        }
    }
}
```

결과 :

```
===== List Info : push_back 1, 2, 3 =====
1 2 3
===== List Info : push_front 4, 5, 6 =====
6 5 4 1 2 3
===== List Info : pop_back =====
6 5 4 1 2
===== List Info : pop_front =====
5 4 1 2
===== List Info : insert 10 at second =====
5 10 4 1 2
===== List Info : erase element at third =====
5 10 1 2
===== List Info : erase 1 =====
5 10 2
```