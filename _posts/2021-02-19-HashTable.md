---
title: "해쉬 테이블, Hash Table C++ Sample Code, [STL] std::unordered_map" 
header:
  # image: /assets/images/koin.jpg
categories:
  - Coding Interview
tags:
  - Algorithm
  - C++
  - Hash Table
  - 해쉬 테이블
  - STL
  - std::unordered_map
toc: true
last_modified_at: 2021-02-19
use_math: true
---
# 1. std::unordered_map container 간략 설명
<br/>
<div>
<a href="https://en.cppreference.com/w/cpp/container/unordered_map" class="bookmark source"><div class="bookmark-info"><div class="bookmark-text"><div class="bookmark-title">std::unordered_map</div><div class="bookmark-description">Unordered map is an associative container that contains key-value pairs with unique keys. Search, insertion, and removal of elements have average constant-time complexity. Internally, the elements are not sorted in any particular order, but organized into buckets. Which bucket an element is placed into depends entirely on the hash of its key.</div></div><div class="bookmark-href"><img src="https://en.cppreference.com/favicon.ico" class="icon bookmark-icon"/>https://en.cppreference.com/w/cpp/container/unordered_map</div></div></a>
</div>
<br/>
std::unordered_map은 key-value 쌍을 포함하는 container이다. 
내부적으로 HashTable로 구현되어 있다.
<br/>
<div>
<a href="https://en.wikipedia.org/wiki/Hash_table" class="bookmark source"><div class="bookmark-info"><div class="bookmark-text"><div class="bookmark-title">Hash table</div><div class="bookmark-description">In computing, a hash table ( hash map) is a data structure that implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a hash function to compute an index, also called a hash code, into an array of buckets or slots, from which the desired value can be found.</div></div><div class="bookmark-href"><img src="https://en.wikipedia.org/static/favicon/wikipedia.ico" class="icon bookmark-icon"/>https://en.wikipedia.org/wiki/Hash_table</div></div><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg/1200px-Hash_table_3_1_1_0_1_0_0_SP.svg.png" class="bookmark-image"/></a>
</div>
<br/>

아래의 표와 같이 검색, 삽입, 제거 모두 평균 $O(1)$의 복잡도를 가지고 있어서 매우 빠르다. 내부적으로 모든 요소는 버킷에 저장되어 있으며 각 버킷은 고유의 hash 키 값을 가지고 있다. hash 키 값을 통하여 요소에 접근하기 때문에 모든 요소에 빠르게 접근할 수 있다.

| 알고리즘   | 평균복잡도 | 최악의경우 |
| ---------- | ---------- | ---------- |
| 공간복잡도 | $O(n)$     | $O(n)$     |
| 검색       | $O(1)$     | $O(n)$     |
| 삽입       | $O(1)$     | $O(n)$     |
| 삭제       | $O(1)$     | $O(n)$     |
   
자세한 내용은 아래 영상을 참고하면 된다.
<br/>
<div>
<a href="https://www.youtube.com/watch?v=Vi0hauJemxA"
		class="bookmark source">
		<div class="bookmark-info">
			<div class="bookmark-text">
				<div class="bookmark-title">[자료구조 알고리즘] 해쉬테이블(Hash Table)에 대해 알아보고 구현하기</div>
				<div class="bookmark-description">Collision</div>
			</div>
			<div class="bookmark-href"><img src="https://www.youtube.com/s/desktop/d2bf50f1/img/favicon.ico"
					class="icon bookmark-icon" />https://www.youtube.com/watch?v=Vi0hauJemxA</div>
		</div><img src="https://i.ytimg.com/vi/Vi0hauJemxA/hqdefault.jpg" class="bookmark-image" />
	</a>
</div>
<br/>

std::unordered_map이 지원하는 여러 함수 중에 우리가 구현 할 3개의 함수는 다음과 같다.

| Member Functions | Description                      |
| ---------------- | -------------------------------- |
| insert           | 값을 삽입합니다.                 |
| erase            | 값을 삭제합니다.                 |
| find             | 특정 key에 매칭된 값을 찾습니다. |

그럼 이제 위의 함수들의 실제 sample code를 사용해보자.

```cpp
#include <iostream>
#include <string>
#include <unordered_map>

using namespace std;

void show(unordered_map<string, int> table, string str) {
    cout << "===== Hash Table Info : " << str.c_str() << " =====" << endl;
    for (const auto& item : table) {
        cout << "key : " << item.first << ", value : " << item.second << endl;
    }
    cout << endl;
}

void main() {
    unordered_map<string, int> hashTable;
    // 1. 삽입
    hashTable["tom"] = 100;
    hashTable["john"] = 90;
    hashTable["mary"] = 80;
    show(hashTable, "operator [] 를 이용한 삽입");
    
    hashTable.insert({ "jim", 70 });
    hashTable.insert(make_pair("jane", 60));
    hashTable.insert({ {"kim", 50}, {"jun", 40} });
    show(hashTable, "insert method를 이용한 삽입");

    // 2. 검색
    auto result = hashTable.find("john");
    cout << "===== Hash Table Info : find method를 이용한 검색 =====" << endl;
    cout << "john 검색 결과 : (" << result->first << ", " << result->second << ")" << endl << endl;

    // 3. 삭제
    string deletedItem = hashTable.begin()->first;
    hashTable.erase(hashTable.begin());
    show(hashTable, "iterator를 이용한 삭제 : " + deletedItem + " 삭제");

    hashTable.erase("tom");
    show(hashTable, "key값을 이용한 삭제 : tom 삭제");

    auto it = hashTable.begin();
    it++;
    hashTable.erase(it, hashTable.end());
    show(hashTable, "구간 삭제");
}
```

결과 :

```
===== Hash Table Info : operator [] 를 이용한 삽입 =====
key : tom, value : 100
key : john, value : 90
key : mary, value : 80

===== Hash Table Info : insert method를 이용한 삽입 =====
key : tom, value : 100
key : jim, value : 70
key : john, value : 90
key : kim, value : 50
key : mary, value : 80
key : jane, value : 60
key : jun, value : 40

===== Hash Table Info : find method를 이용한 검색 =====
john 검색 결과 : (john, 90)

===== Hash Table Info : iterator를 이용한 삭제 : jim 삭제 =====
key : tom, value : 100
key : john, value : 90
key : kim, value : 50
key : mary, value : 80
key : jane, value : 60
key : jun, value : 40

===== Hash Table Info : key값을 이용한 삭제 : tom 삭제 =====
key : john, value : 90
key : kim, value : 50
key : mary, value : 80
key : jane, value : 60
key : jun, value : 40

===== Hash Table Info : 구간 삭제 =====
key : kim, value : 50
```

# 2. Hash Table C++ Sample Code

HashTable 구현 방식으론 크게 linked list를 이용한 seperate chaining 방식과 open addressing 방식으로 나뉜다.
아래의 샘플코드는  seperate chaining 방식을 이용하여 구현되었다.
key는 string, value는 integer를 가지고 hash function은 널리 쓰이는 djb2 알고리즘을 사용할 것이다.
여담으로 "5381"이란 숫자는 709번째 prime number(소수)라고 한다.

```cpp
// hash function
unsigned long djb2(const char *str)
{
    unsigned long hash = 5381;
    int c;
    while (c = *str++)
        hash = ((hash << 5) + hash) + c; /* hash * 33 + c */
     return hash;
}
```

그럼 이제 Hash Table Sample Code를 살펴보자

```cpp
#define MAX_KEY 128
#include <iostream>
#include <string>

using namespace std;
// Seperate Chaining을 위한 linked list node
typedef struct _node {
    char key[MAX_KEY];
    int val;
    _node* next;
}Node;
// string copy
void _strcpy(const char* src, char* dst) {
    while (*src != '\0') {
        *dst = *src;
        src++;
        dst++;
    }
    *dst = '\0';
}
// string compare
int _strcmp(const char* str1, const char* str2) {
    while (*str1 != '\0') {
        if (*str1 != *str2)
            break;
        str1++;
        str2++;
    }
    return (*str1 - *str2);
}

// hash function
unsigned long djb2(const char* str)
{
    unsigned long hash = 5381;
    int c;
    while (c = *str++)
        hash = ((hash << 5) + hash) + c; /* hash * 33 + c */
    return hash;
}

class HashTable {
private:
    Node** TB;
    int _capacity;
    void init(int capacity);
    void release();
    Node* createNode(const char* key, const int val);
public:
    HashTable(int capacity);
    ~HashTable();
    void insert(const char* key, const int val);
    bool find(const char* key, int& ret);
    void erase(const char* key);
    void show(string str);
};

void main() {
    HashTable* hashTable = new HashTable(50);
    //// 1. 삽입
    hashTable->insert("tom",100);
    hashTable->insert("john",90);
    hashTable->insert("mary", 80);
    hashTable->insert("jim", 70);
    hashTable->insert("jane", 60);
    hashTable->insert("kim", 50);
    hashTable->insert("jun", 40);
    hashTable->show("insert method를 이용한 삽입");

    //// 2. 검색
    int ret;
    if (hashTable->find("john", ret)) {
        cout << "===== Hash Table Info : find method를 이용한 검색 =====" << endl;
    cout << "john 검색 결과 : (john, " << ret << ")" << endl << endl;
    }
    

    //// 3. 삭제
    hashTable->erase("tom");
    hashTable->show("key값을 이용한 삭제 : tom 삭제");

}

void HashTable::init(int capacity)
{
    _capacity = capacity;
    TB = new Node * [_capacity];
    for (int i = 0; i < _capacity; i++) {
        TB[i] = nullptr;
    }
}

void HashTable::release()
{
    for (int i = 0; i < _capacity; i++) {
        Node* cur = TB[i];
        while (cur != nullptr) {
            Node* tmp = cur;
            cur = cur->next;
            delete tmp;
        }
    }
}

Node* HashTable::createNode(const char* key, const int val)
{
    Node* newNode = new Node;
    _strcpy(key, newNode->key);
    newNode->val = val;
    newNode->next = nullptr;
    return newNode;
}

HashTable::HashTable(int capacity)
{
    init(capacity);
}

HashTable::~HashTable()
{
    release();
}

void HashTable::insert(const char* key, const int val)
{
    // create node and hash
    Node* newNode = createNode(key, val);
    // _capacity로 modular 연산후 삽입한다.
    unsigned long hash = djb2(key) % _capacity;
    Node* cur = TB[hash];
    // 같은 키가 존재할 경우 error 처리
    while (cur != nullptr) {
        if (_strcmp(key, cur->key) == 0) {
            cout << "Error! the same key exists" << endl;
            return;
        }
        cur = cur->next;
    }
    // hash bucket에 해당하는 linked list의 맨앞에 추가한다.
    newNode->next = TB[hash];
    TB[hash] = newNode;
}

bool HashTable::find(const char* key, int& ret)
{
    unsigned long hash = djb2(key) % _capacity;
    Node* cur = TB[hash];
    while (cur != nullptr) {
        if (_strcmp(key, cur->key) == 0) {
            ret = cur->val;
            return true;
        }
        cur = cur->next;
    }
    return false;
}

void HashTable::erase(const char* key)
{
    unsigned long hash = djb2(key) % _capacity;
    Node* cur = TB[hash];
    Node* prev = nullptr;
    while (cur != nullptr) {
        if (_strcmp(key, cur->key) == 0) {
            if (prev == nullptr) {
                TB[hash] = cur->next;
            }
            else {
                prev->next = cur->next;
            }
            delete cur;
            return;
        }
        prev = cur;
        cur = cur->next;
    }
}

void HashTable::show(string str)
{
    cout << "===== HashTable Info : " << str.c_str() << " =====" << endl;
    for (int i = 0; i < _capacity; i++) {
        Node* cur = TB[i];
        while (cur != nullptr) {
        //key: tom, value : 100
            cout << "key: " << cur->key << ", value : " << cur->val << endl;
            cur = cur->next;
        }
    }
    cout << endl;
}
```

결과 :

```
===== HashTable Info : insert method를 이용한 삽입 =====
key: jun, value : 40
key: mary, value : 80
key: jim, value : 70
key: jane, value : 60
key: tom, value : 100
key: kim, value : 50
key: john, value : 90

===== Hash Table Info : find method를 이용한 검색 =====
john 검색 결과 : (john, 90)

===== HashTable Info : key값을 이용한 삭제 : tom 삭제 =====
key: jun, value : 40
key: mary, value : 80
key: jim, value : 70
key: jane, value : 60
key: kim, value : 50
key: john, value : 90
```

---

# Reference

1. [https://en.cppreference.com/w/cpp/container/unordered_map](https://en.cppreference.com/w/cpp/container/unordered_map)
2. [https://en.wikipedia.org/wiki/Hash_table](https://en.wikipedia.org/wiki/Hash_table)
3. [https://www.youtube.com/watch?v=Vi0hauJemxA](https://www.youtube.com/watch?v=Vi0hauJemxA)