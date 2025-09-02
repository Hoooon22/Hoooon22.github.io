---
layout: default
title: Integer와 int의 차이
parent: ★ Java
date: 2025-09-02 20:24:32
---

# Integer와 int의 차이

최근 면접에서 `Integer`와 `int`의 차이에 대해 명확하게 답변하지 못했던 경험이 있어, 복기하는 차원에서 내용을 정리해 올립니다.

---

## int (Primitive Type)

`int`는 Java의 **기본 자료형(Primitive Type)** 중 하나입니다.

- 변수를 선언하면 데이터 값 자체를 저장하는 공간이 스택(Stack) 메모리에 생성됩니다.
- 즉, `int`는 변수의 타입 그 자체이며, 데이터의 종류에 따라 값이 저장될 공간의 크기와 저장 형식을 정의합니다.
- 산술 연산이 가능하며, `null` 값을 가질 수 없습니다.

## Integer (Wrapper Class)

`Integer`는 `int` 기본 자료형을 객체로 다루기 위해 사용하는 **래퍼 클래스(Wrapper Class)**입니다.

- `Integer` 변수는 데이터 값이 아닌, 값이 저장된 힙(Heap) 메모리의 주소를 가리키는 참조 변수입니다.
- 객체이기 때문에 다양한 메서드(예: `parseInt()`, `compareTo()`)를 포함하고 있으며, 필드에 기본 데이터 유형(`int`)을 저장할 수 있습니다.
- `null` 값을 가질 수 있어, 데이터가 없는 상태를 표현해야 할 때 유용합니다.

---

## 주요 차이점 요약

| 구분 | `int` | `Integer` |
| :--- | :--- | :--- |
| **종류** | 기본 자료형 (Primitive Type) | 래퍼 클래스 (Wrapper Class) |
| **저장 위치** | 스택(Stack) 메모리에 값 직접 저장 | 스택에는 참조 주소, 힙(Heap)에 실제 값 저장 |
| **null 허용**| 불가 | 가능 |
| **기본값** | 0 | null |
| **연산** | 산술 연산 가능 | 객체이므로 메서드를 통해 연산 (Unboxing 후 가능) |
