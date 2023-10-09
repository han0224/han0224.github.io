---
layout: single
title: "[프로그래머스] 삼각 달팽이"
categories:
  - Programmers
tag: [Coding Test, JS]
toc: true
---

## 📖 문제

[level2 삼각 달팽이](https://school.programmers.co.kr/learn/courses/30/lessons/68645)

## ✏️ 나의 풀이

문제를 풀면서 가장 먼저 고민한게 삼각형 모양이었다.

배열을 어떤 식으로 삼각형 모양으로 관리할 수 있는지 이에 대해 고만을 해봤다.

결론적으로 정삼각형 모양이 아닌 직각삼각형같은 모양으로 생각하니 이에 대한 고민이 해결되었다.

그리고 아래로 갈때랑, 위로 갈때, 오른쪽으로 갈때 이를 관리하고 있는 변수를 하나 생성해 이 변수에 따라 배열의 위치를 갖고 있는 변수의 값을 변경해주도록 하였다.

이제 마지막으로 어느 상황에서 이 상태를 바꾸어야할지 결정해야하는데 단순히 머릿속에서만 구상하니 쉽게 풀리지 않았다.

그래서 아래 그림처럼 직접 손으로 그려보며 고민해보았다.

![IMG_F062D8DF0CC3-1](https://github.com/han0224/my-earth/assets/70616579/b4a80c9b-1e6f-4d71-b35f-a6ab44856800){: width="70%" height="70%" }

최종적으로 코드는 아래와 같은 순서로 동작하게 된다.

### 변수 초기화
1. 배열의 위치를 갖고 있는 변수 i(열), j(행)를 0으로 초기화 시킨다.
1. 다음에 배열의 어느 위치를 채울지 관리하고 있는 status 변수를 `down` 으로 초기화 시킨다.
1. 배열의 채울 숫자를 관리하는 변수 `count`를 1로 초기화 시킨다.
1. 배열을 0으로 초기화하되 삼각형 모양의 배열으로 선언한다. `new Array(n).fill(0).map((v, i)=>new Array(i+1).fill(0));`
1. 최종적으로 배열에 채워질 마지막 숫자를 가지고 있을 `endNum` 상수를 초기화시킨다.

### 무한 반복문
1. 만일 count의 값이 endNum과 같거나 크다면 무한 반목문을 종료시킨다.
1. arr[i][j] 을 count의 값으로 변경시킴과 동시에 count 값을 1증가 시킨다. `arr[i][j] = count++;`
1. status === 'down'
    1. 열(i)를 1만큼 증가시킨다.
    1. 만일 증가시킨 i에 따라 arr[i][j]가 배열의 크기에서 벗어났거나, 이미 채워진 위치일 경우 
    1. 열은 그대로 유지하되, 행을 변경시켜주어야한다.
    1. 그렇기에 i를 1만큼 감소시키고, j를 1만큼 증가시킨 후, status를 right로 변경시킨다.
1. status === 'right'
    1. 행(j)을 1만큼 증가시킨다.
    1. 만일 증가시킨 행에 따라 arr[i][j]가 배열의 크기에서 벗어났거나, 이미 채워진 위치일 경우 
    1. 열(i)을 1만큼 감소시키고, 행(j)은 2만큼 감소시켜주어야한다.
    1. status를 up으로 변경시킨다.
1. status === 'up'
    1. 행(j)과 열(i)을 각각 1만큼 감소시킨다.
    1. 만일 arr[i][j]가 배열의 크기에서 벗어났거나, 이미 채워진 위치일 경우
    1. 열(i)을 2만큼 증가시키고, 행(j)을 1만큼 증가시켜주어야한다.
    1. status를 down으로 변경시킨다.

### 최종 반환
return 값으로는 1차원배열이기에 reduce 메소드를 사용해 모든 배열의 값들을 spread 연산자를 이용해 한 배열에 저장하도록 하였다.

```javascript
arr.reduce((acc, cur) => [...acc, ...cur], [])
```

## 👩‍💻 코드

```javascript
function solution(n) {
    const arr = new Array(n).fill(0).map((v, i)=>new Array(i+1).fill(0));
    let count = 1;
    let status = 'down'; // down, up, right
    let i = 0;
    let j = 0;
    const endNum = arr.reduce((acc, cur) => cur.length + acc, 0);
    while(count <= endNum){
        arr[i][j] = count++;
        if(status==='down'){
            i += 1;
            if(i === n || arr[i][j] > 0){
                i -= 1;
                j += 1;
                status = 'right'
            }
            continue;
        }
        if(status === 'right'){
            j += 1;
            if(arr[i][j] === undefined || arr[i][j] > 0){
                i -= 1;
                j -= 2;
                status = 'up'
            }
            continue;
        }   
        if(status === 'up'){
            i -= 1;
            j -= 1;
            if(i < 0 || j < 0 || !arr[i][j] === undefined || arr[i][j] > 0){
                i += 2;
                j += 1;
                status = 'down';
            }
            continue;
        }
    }
    return arr.reduce((acc, cur) => [...acc, ...cur], []);
}

```