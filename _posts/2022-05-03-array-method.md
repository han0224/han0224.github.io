---
layout: single
title: "[js] Array method 정리"
categories:
  - JavaScript
tag: [Array, method ]
toc: true
---

## at()
정수 값을 받아, 배열에서 해당 값에 해당하는 인덱스의 요소를 반환

음수 값의 경우 배열의 역순을 기준으로

대괄호 표기법으로 마지막 요소를 가져오고 싶을 경우 arr[arr.length - 1] 을 사용하지만, arr.at(-1) 을 대신 사용할 수 있음 

주어진 인덱스가 배열에 없으면 <U>undefind</U> 를 반환

```javascript
const arr = [1, 2, 3, 4, 5];
console.log(arr.at(2));     // 3
console.log(arr.at(-2));    // 4
```

## concat()
인자로 주어진 배열이나 값들을 기존 배열에 합쳐서 새 배열을 반환

- **기존 배열을 변경하지 않음**
- **추가된 새로운 배열을 반환**

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const arr3 = arr1.concat(arr2);
const arr4 = arr3.concat(7, 8);
console.log(arr3);          // [1, 2, 3, 4, 5, 6]
console.log(arr4);          // [1, 2, 3, 4, 5, 6, 7, 8]
```

## every()
배열 안의 **<U>모든 요소</U>**가 주어진 판별 함수를 통과하는지 테스트

Boolean 값을 반환

빈 배열에서 호출하면 모조건 true 반환

```javascript
arr.every((element, index, array) =>{...})
```
- element: 배열에서 처리되는 현재 요소
- index: 처리할 현재 요소의 인덱스
- array: every를 호출한 배열

```javascript
[1, 2, 3].every(e => e > 0)     // true
[1, 2, 3].every(e => e > 2)     // false
```

## some()
배열 안의 **<U>어떤 요소라도</U>** 주어진 판별 함수를 통과하는지 테스트

Boolean 값을 반환

빈 배열에서 호출하면 모조건 false 반환

```javascript
arr.some((element, index, array) =>{...})
```
- element: 배열에서 처리되는 현재 요소
- index: 처리할 현재 요소의 인덱스
- array: some 호출한 배열

```javascript
[1, 2, 3].every(e => e < 2)     // true
[1, 2, 3].every(e => e < 1)     // false
```

## filter()
주어진 함수의 테스트를 통과하는 요소를 모아 **<U>새로운 배열로 반환</U>**

어떤 요소도 테스트를 통과하지 못했으면 빈 배열을 반환
```javascript
arr.filter((element, index, array) =>{...})
```
- element: 배열에서 처리되는 현재 요소
- index: 처리할 현재 요소의 인덱스
- array: filter 호출한 배열

```javascript
const arr1 = [1, 2, 3].filter(e => e < 2)     // [1]
```

## find()
주어진 판별 함수를 만족하는 **첫 번째 요소의 값**을 반환

그런 요소가 없다면 undefined 반환

```javascript
arr.find((element, index, array) =>{...})
```
- element: 배열에서 처리되는 현재 요소
- index: 처리할 현재 요소의 인덱스
- array: find 호출한 배열

```javascript
[1, 2, 3].find(e => e < 2)     // 1
[1, 2, 3].find(e => e > 1)     // 2
```

## findIndex()
주어진 판별 함수를 만족하는 배열의 **첫 번째 요소에 대한 인덱스**를 반환

그런 요소가 없다면 -1 반환

```javascript
arr.findIndex((element, index, array) =>{...})
```
- element: 배열에서 처리되는 현재 요소
- index: 처리할 현재 요소의 인덱스
- array: findIndex 호출한 배열

```javascript
[1, 2, 3].findIndex(e => e < 2)     // 0
[1, 2, 3].findIndex(e => e > 2)     // 2
```

 작성 중
## flat()