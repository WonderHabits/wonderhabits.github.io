---
title: "벡터, STL Vector C++ Sample Code, [STL] std::vector" 
header:
  # image: /assets/images/koin.jpg
categories:
  - Coding Interview
tags:
  - Algorithm
  - C++
  - 벡터
  - STL Vector
  - std::vector
toc: true
last_modified_at: 2021-03-10
use_math: true
---
# 1. std::vector 간략 설명
<br/>
<div>
<a
					href="https://en.cppreference.com/w/cpp/container/vector" class="bookmark source">
					<div class="bookmark-info">
						<div class="bookmark-text">
							<div class="bookmark-title">std::vector</div>
							<div class="bookmark-description">1) std::vector is a sequence container that encapsulates
								dynamic size arrays. The storage of the vector is handled automatically, being expanded
								and contracted as needed. Vectors usually occupy more space than static arrays, because
								more memory is allocated to handle future growth.</div>
						</div>
						<div class="bookmark-href"><img src="https://en.cppreference.com/favicon.ico"
								class="icon bookmark-icon" />https://en.cppreference.com/w/cpp/container/vector</div>
					</div>
				</a>
</div>
<br/>
벡터(std::vector)는 일반 배열과는 다르게 동적 배열 구조로 되어있다. 즉, 벡터는 저장 공간보다 많은 양의 데이터를 추가할 경우 현재 보유하고 있는 메모리의 두 배만큼 할당하여 자동으로 배열의 크기를 조절한다.

그리고 new, delete 필요 없이 자동으로 메모리 관리도 해주기 때문에 많이 쓰인다.

 std::priority_queue가 지원하는 여러 함수 중에 우리가 구현 할 4개의 함수는 다음과 같다.

| Member Functions | Description              |
| ---------------- | ------------------------ |
| push_back        | 마지막에 요소 삽입       |
| empty            | 저장공간이 비었는지 확인 |
| at               | 특정 요소에 접근         |
| size             | 크기 확인                |
| clear            | 모두 삭제후 재 정렬      |


그럼 이제 위의 함수들의 실제 sample code를 사용해보자.

```cpp
#include <iostream>
#include <vector>

using namespace std;

void main() {
    vector<int> vec;
    const auto data = { 5, 4, 6, 2, 3, 1 };
    for (const int& n : data)
        vec.push_back(n);

    cout << "===== Vector =====" << endl;
    for (int i = 0; i < vec.size(); i++)
        cout << vec.at(i) << " ";

    vec.clear();
    if (vec.empty())
        cout << endl << "vector is cleared" << endl;

}
```

# 2. STL Vector C++ Sample Code

```cpp
#include <iostream>
#define MIN_SIZE 4
using namespace std;

template <typename T>
class Vector {
private:
    int _capacity;
    int _size;
    T* _arr;
public:
    Vector();
    ~Vector();
    int size();
    bool empty();
    void clear();
    T at(int idx);
    void push_back(T val);
};

template<typename T>
Vector<T>::Vector()
{
    _capacity = MIN_SIZE;
    _size = 0;
    _arr = new T[_capacity];
}

template<typename T>
Vector<T>::~Vector()
{
    delete[] _arr;
}

template<typename T>
int Vector<T>::size()
{
    return _size;
}

template<typename T>
bool Vector<T>::empty()
{
    return (_size == 0);
}

template<typename T>
void Vector<T>::clear()
{
    _capacity = MIN_SIZE;
    _size = 0;
    delete[] _arr;
    _arr = new T[_capacity];
}

template<typename T>
T Vector<T>::at(int idx)
{
    // 예외처리 가능
    if (idx >= _size) {
        cout << "Error : Out of range " << endl;
        return -1;  
    }
    return _arr[idx];
}

template<typename T>
void Vector<T>::push_back(T val)
{
    if (_size >= _capacity) {
        _capacity *= 2;
        T* tmp = new T[_capacity];
        for (int i = 0; i < _size; i++) {
            tmp[i] = _arr[i];
        }
        delete[] _arr;
        _arr = tmp;
    }
    _arr[_size++] = val;
}

void main() {
    Vector<int> vec;
    const auto data = { 5, 4, 6, 2, 3, 1 };
    for (const int& n : data)
        vec.push_back(n);
    
    cout << "===== Vector =====" << endl;
    for (int i = 0; i < vec.size(); i++)
        cout << vec.at(i) << " ";

    vec.clear();
    if (vec.empty())
        cout << endl << "vector is cleared" << endl;

}
```

결과 화면 :

```
===== Vector =====
5 4 6 2 3 1
vector is cleared
```

# 3. Reference

1. [https://en.cppreference.com/w/cpp/container/vector](https://en.cppreference.com/w/cpp/container/vector)