---
layout: default
title: 코딩테스트 C++ 개인 요약
parent: C++
date: 2024-12-12 23:22:40
---
> 자바 문법과 많이 다른 부분 위주로 작성하였습니다.

## 자료형
### 1. 명시적 형변환

```C++
#include <iostream>

using namespace std;

int main() {
	int i = 65;
	double d = 5.2;

	// 명시적 형변환
	cout << static_cast<int>(d) << endl; // 5

	return 0;
}
```

## 문자열
### 1. 문자열 찾기

```C++
#include <iostream>
#include <string>

using namespace std;

int main() {
	// 문자열 초기화
	string str = "Hello, World!";

	// find
	int num = str.find("o"); 
	cout << num << endl; // 출력: 4

	return 0;
}
```

### 2. 문자열 수정

```C++
#include <iostream>
#include <string>

using namespace std;

int main() {
	string str = "Appl";
	str += "e"; // Apple

	// 문자열 수정
	str[0] = 'B'; // Bpple
	str.replace(2, 2, "lol"); // Blolle

	return 0;
}
```

## STL
### STL이란
> Standard Template Library

C++에서 제공하는 템플릿 기반의 표준 라이브러리
	-> 템플릿이란, C++에서 함수나 클래스를 구현할 때 **어떤 타입**에서도 동작할 수 있도록 하는 문법

STL은 크게 3가지로 이루어진다.
- 데이터를 담는 **컨테이너**
- 데이터를 처리하고 제어하는 **알고리즘**
- 컨테이너에 접근 및 순회할 수 있게 하는 **반복자**

### Call by reference
- void modify(int& value)
- 주소: &value


```C++
#include <iostream>
#include <vector>
#include <map>

using namespace std;

int main() {
	// vector
	vector<int> vec = {1, 2, 3, 4, 5};

	for (int num : vec) {
		cout << num << " ";
	}
	cout << endl; // 1, 2, 3, 4, 5

	// map
	map<string, int> fruitMap = {{"apple", 1}, {"banana", 2}, {"cherry", 3}};
	for (const audo& pair : fruitMap) {
		cout << pair.first << "=" << pair.second << " ";
	}
	cout << endl; // apple=1 banana=2 cherry=3

	return 0;
}
```

위와 같이 타입과 상관없이 유동적인 함수를 기용할 수 있다.

### 반복자
반복자는 C++에서 컨테이너(벡터, 맵, 셋 등) 종류와 관계없이 원소들을 순회하고 접근할 수 있게 해준다.

- 순방향 반복자 

```C++
#include <algorithm>
#include <iostream>
#include <vector>

using namespace std;

int main() {
	vector<int> vec = {10, 20, 30, 40, 50};

	// 순회 및 출력 (포인터 문법 사용)
	for (auto it = vec.begin(); it != vec.end(); ++it) {
		cout << *it << " ";
	}
	cout << endl; // 출력: 10 20 30 40 50

	
}
```