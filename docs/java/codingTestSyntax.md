---
layout: default
title: 코딩테스트 - Java 문법 정리
layout: default
parent: ★ Java
date: 2024-10-25 22:15:38
---

## 자료형
- 우선순위 큐

```java
PriorityQueue<Integer> pQ = new PriorityQueue<>();

// 삽입 (큐랑 동일)
pQ.add(1);

// front 확인 및 제거
pQ.remove();
```

- 해시맵

```java
HashMap<String, Integer> map = new HashMap<>();

map.put("apple", 1);
map.put("banana", 2);

// 키값 변경
map.put("banana", 4);

// 키가 있는지 확인, 키값 가져오기 (get)
String key = "apple";
if (map.containsKey(key)) { 
	int value = map.get(key); 
	System.out.println(key + ": " + value); // apple: 1 
	}

// 키값 삭제
map.remove("banana");
```

- 스택

```java
Stack<Integer> stack = new Stack<>();
```

- 큐

```java
Queue<Integer> queue = new LinkedList<>();
```

- 연결리스트

```java
LinkedList<Integer> list = new LinkedList<>();

// add
list.addFirst(1); // 앞에 추가
list.addLast(2); // 뒤에 추가
list.add(3);
list.add(1, 10); // index 1에 값 "10"추가

// remove
list.removeFirst();
list.removeLast();
list.remove(); // 생략시 index 0 제거
list.remove(2); // index 2 제거
list.clear();

// 기타
list.get(1);
list.size();
list.contain(1); // 1 검색, boolean
list.indexOf(1); // index 1에 있는 값 불러오기, 없으면 -1
```

- 해시셋

```java
HashSet<Integer> set1 = new HashSet<>();

// 용량이 10인 HashSet 생성 (해시셋은 저장공간을 늘릴 때, 2배로 늘리기 때문에 크기를 알고 있다면 정해주는 것이 Best)
HashSet<Integer> set2 = new HashSet<>(10);

set.add(1);
set.add(1);
set.add(2);

set.remove(1); // 값 1 제거
set.clear();

if (set.contains(1)) {
	System.out.println("It has 1.");
}
```

## 문자열
1. 정렬

```java
// 기본 정렬 (오름차순)
Arrays.sort(arr);

// 내림차순 정렬
Arrays.sort(arr, Collections.reverseOrder());
```

- StringBuffer


```java
String str = "abc";
StringBuffer sb = new StringBuffer(str); // "abc"로 초기화

// reverse (거꾸로, toString)
String reversedStr = sb.reverse().toString;
```

- String to Int

```java
String str = "123";
int a = Integer.parseInt(str);
```

1. int to String
```java
int a = 123;
String str1 = Integer.toString(a);
String str2 = a + "";
```