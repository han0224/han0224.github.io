---
layout: single
title: "[알고리즘] 백트래킹"
categories:
  - Algorithm
tag: [backtraing]
toc: true
---

## 백트래킹

현재 상태에서 가능한 모든 후보군을 따라 해결책에 대한 후보를 구축하다가 가능성이 없는 후보는 즉시 포기하면서 정답을 찾아가는 범용적인 알고리즘

가지치기를 통해 효율 극대화

가지치기: 유망하지 않은 후보는 가지치기로 쳐내어 탐색하는 기법

## DFS 와 백트래킹

DFS 는 대표적인 완전 탐색 방법이다.

현재 지점에서 방문할 곳이 있으면 재귀 호출을 통해 계속 이동한다.

장점: 모든 곳을 탐색해야 하는 경우 효과적이다.

단점: 모든 곳을 방문하지 않아도 될 경우에는 비효율적이다.

DFS의 비효율적인 경로를 차단하고 목표지점에 갈 수 있는 가능성이 있는 루트를 검사하는 방법이 백트래킹이 알고리즘이다.

## N-Queen

> N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다. N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

만일, (1, 1) 자리에 퀸을 놓았다면 다음에 놓을 수 2행에 놓을 수 있는 곳은 (2, 3), (2, 4) 뿐이다. 그렇기에 (2, 1), (2, 2) 자리에 놓았을 경우는 배제하고 DFS 를 돌리면 된다.

![123](https://user-images.githubusercontent.com/70616579/168978386-0bffd6bc-2997-4b69-b213-8d803e01c22d.jpg){: width="90%" height="90%"}

1차원 배열로 했을 경우 인덱스는 행을 값은 열로 생각을 하며 문제를 풀어보자

### DFS 구현

DFS를 구현하기 위해 인자와 종료 조건을 생각해보자

우리는 가장 위에서부터 차례로 퀸을 놓을 것이기때문에 행을 인자로 받고, 행이 주어진 N과 같아지는 지점에서 종료하면된다.

```javascript
const dfs = (row) => {
  if (row === input) {
    return;
  }
};
```

그 뒤에 반복문을 돌려서 현재 행의 모든 열에 하나하나씩 퀸을 놓아보고, 퀸을 배치해도 문제가 없다면 다음 행으로 넘어가보자.

문제가 있는지 없는지 여부는 조금있다가 생각해보자.

반복이 끝나고 돌아왔으면 현재 행의 다른 열에도 퀸을 배치해봐야 하므로 0으로 다시 바꿔준다.

만일 마지막 열까지 도착을 했다면 문제의 조건에 맞게 퀸을 배치 했으므로 answer의 값을 1 증가 시켜준다.

```javascript
const dfs = (row) => {
  if (row === input) {
    answer++;
    return;
  }
  for (let col = 0; col < input; col++) {
    arr[row] = col;
    if (check(row)) dfs(row + 1);
    arr[row] = 0;
  }
};
```

### 배치 조건 확인

배치할 수 있는 조건은 다음과 같다.

1. 같은 열에 배치 할 수 없다.
2. 두 퀸사이의 행의 차와 열의 차가 같으면 안된다.

우리는 인덱스를 행으로, 해당 인덱스의 값을 열로 지정해주었기 때문에 아래 코드와 같이 작성을 하면 된다.

```javascript
const check = (row) => {
  for (let i = 0; i < row; i++) {
    if (arr[row] === arr[i] || row - i === Math.abs(arr[row] - arr[i])) {
      return false;
    }
  }
  return true;
};
```

<details>
  <summary>전체코드</summary>
  <div markdown='1'>
```javascript
const fs = require("fs");
const input = +fs.readFileSync("/dev/stdin").toString().trim();

const arr = new Array(input).fill(0);
let answer = 0;

const check = (row) => {
  for (let i = 0; i < row; i++) {
    if (arr[row] === arr[i] || row - i === Math.abs(arr[row] - arr[i])) {
      return false;
    }
  }
  return true;
};

const dfs = (row) => {
  if (row === input) {
    answer++;
    return;
  }
  for (let col = 0; col < input; col++) {
    arr[row] = col;
    if (check(row)) dfs(row + 1);
    arr[row] = 0;
  }
};

dfs(0);
console.log(answer);

```

</div>
</details>
