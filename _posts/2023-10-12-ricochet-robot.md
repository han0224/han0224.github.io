---
layout: single
title: "[프로그래머스]리코쳇 로봇"
categories:
  - Programmers
tag: [Coding Test, JS]
toc: true
---

## 📖 문제

[level2 리코쳇 로봇](https://school.programmers.co.kr/learn/courses/30/lessons/169199)

## ✏️ 나의 풀이

그동안 풀었던 bfs와는 차별점이 있었던 문제였다.

기존 bfs 문제들은 한칸씩 이동하는 방식이었다면 이 문제는 맨 끝에 부딪힐 때까지 미끄러지는 새로운 규칙이 추가되어 있다.

이 규칙때문에 처음에 어떻게 접근해야할지 막막했지만, 기존 bfs 코드에 단순히 장애물 혹은 벽에 부딪힐때까지 계속 이동하는 코드만 추가하면 된다는 것을 알게 되었다.

### 상하좌우 이동하는 함수
게임에서 말은 상, 하, 좌, 우 4방향으로 이동하므로 이 4가지 방향으로 끝까지 이동하는 코드만 추가해주었다.

```javascript
    const up = (x, y) => {
      if (x === 0) return -1;
      for (let i = x; i >= 0; i--) {
        if (board[i][y] === "D") return i + 1 === x ? -1 : [i + 1, y];
      }
      return [0, y];
    };
    const down = (x, y) => {
      if (x === board.length - 1) return -1;
      for (let i = x; i < board.length; i++) {
        if (board[i][y] === "D") return i - 1 === x ? -1 : [i - 1, y];
      }
      return [board.length - 1, y];
    };
    const right = (x, y) => {
      if (y === board[x].length - 1) return -1;
      for (let i = y; i < board[x].length; i++) {
        if (board[x][i] === "D") return i - 1 === y ? -1 : [x, i - 1];
      }
      return [x, board[x].length - 1];
    };
    const left = (x, y) => {
      if (y === 0) return -1;
      for (let i = y; i >= 0; i--) {
        if (board[x][i] === "D") return i + 1 === y ? -1 : [x, i + 1];
      }
      return [x, 0];
    };
```
<br/>

위로 이동하는 경우를 예를 들어 설명하자면, 

```javascript
    const up = (x, y) => {
      if (x === 0) return -1;
      for (let i = x; i >= 0; i--) {
        if (board[i][y] === "D") return i + 1 === x ? -1 : [i + 1, y];
      }
      return [0, y];
    };
```

1. 매개변수로 현재 위치를 받는다.
    1. 첫번재 인자(x)는 열을, 두번째 인자(y)는 행을 가르킨다.
1. 만일 x가 0일 경우 더 이상 위로 이동할 수 없으므로 `-1`을 반환한다.
1. x가 0이 아닐 경우 x부터 0까지 1씩 감소하는 반복문을 실행시킨다.
1. 만일 이동한 위치에 D가 있을 경우 반복문을 종료한다.
    1. 만일 현재 위치가 x보다 한칸만 클 경우 더 이상 위로 이동할 수 없음을 의미한다. 즉, 바로 위 칸에 장애물이 있기에 `-1`을 반환한다.
    1. 그렇지 않다면 i에 1을 증가시킨다.
    1. 1을 증가시키는 이유는 1을 증가시키지 않으면 장애물이 있는 위치를 반환하기 때문이다.
1. 만일 반복문을 돌면서 장애물을 만나지 못했다면, 끝까지 이동할 수 있음을 의미하므로, 열을 0으로 해서 반환시킨다.


크게 3가지 경우의 수가 있다 이거를 좀 더 간단히 설명하자면 아래 그림과 같다.
![장애물을 만나지 못한 경우](https://github.com/han0224/my-earth/assets/70616579/c3d27fb1-1da3-4f50-89bb-d8143fe3d6ae){: width="70%" height="70%" }

![이동할 수 없는 경우](https://github.com/han0224/my-earth/assets/70616579/69a597f2-0e8c-4c97-8081-a452b149844a){: width="70%" height="70%" }

![장애물을 만난경우](https://github.com/han0224/my-earth/assets/70616579/894ad5cb-7d72-4bb7-8fba-6fcf4bcb32b5){: width="70%" height="70%" }

<br/>

이런 식으로 상, 하, 좌, 우를 각각 구현해 bfs 코드에 잘 녹여 주면 된다.

```javascript
const bfs = (x, y) => {
      const queue = [[x, y, 1]];
      const visited = new Array(board.length)
        .fill(0)
        .map((_) => new Array(board[0].length).fill(false));
      visited[x][y] = true;
      while (queue.length) {
        const v = queue.shift();
        for (let i = 0; i < 4; i++) {
          const res = direction[i](v[0], v[1]);
          if (res === -1) continue;
          const [xx, yy] = res;
          if (xx < 0 || yy < 0 || xx >= board.length || yy >= board[0].length)
            continue;
          if (visited[xx][yy]) continue;

          visited[xx][yy] = true;

          if (board[xx][yy] === "G") return v[2];

          queue.push([xx, yy, v[2] + 1]);
        }
      }
      return -1;
    };
```

대부분의 코드는 기본적인 bfs와 일치한다.

단, 최단거리를 구하는 것이기에 현재 이동 경로가 몇번 이동했는지를 가지고 있는 숫자도 같이 queue에 저장해두고 있다.

이러한 점을 제외하고선 기존 bfs 코드와 거의 유사하다.

bfs에 간단 설명은 포스팅해노았기에 bfs를 잘모른다면 읽어보길 추천한다.

[[알고리즘]BFS(너비 우선 탐색)](https://han0224.github.io/algorithm/bfs/)

## 👩‍💻 코드

```javascript
function solution(board) {
    var answer = 0;
    const start = [];

    for (let i = 0; i < board.length; i++) {
      const res = board[i].indexOf("R");
      if (res >= 0) {
        start.push(i, res);
        break;
      }
    }
    const up = (x, y) => {
      if (x === 0) return -1;
      for (let i = x; i >= 0; i--) {
        if (board[i][y] === "D") return i + 1 === x ? -1 : [i + 1, y];
      }
      return [0, y];
    };
    const down = (x, y) => {
      if (x === board.length - 1) return -1;
      for (let i = x; i < board.length; i++) {
        if (board[i][y] === "D") return i - 1 === x ? -1 : [i - 1, y];
      }
      return [board.length - 1, y];
    };
    const right = (x, y) => {
      if (y === board[x].length - 1) return -1;
      for (let i = y; i < board[x].length; i++) {
        if (board[x][i] === "D") return i - 1 === y ? -1 : [x, i - 1];
      }
      return [x, board[x].length - 1];
    };
    const left = (x, y) => {
      if (y === 0) return -1;
      for (let i = y; i >= 0; i--) {
        if (board[x][i] === "D") return i + 1 === y ? -1 : [x, i + 1];
      }
      return [x, 0];
    };

    const direction = [
      (x, y) => up(x, y),
      (x, y) => down(x, y),
      (x, y) => right(x, y),
      (x, y) => left(x, y),
    ];

    const bfs = (x, y) => {
      const queue = [[x, y, 1]];
      const visited = new Array(board.length)
        .fill(0)
        .map((_) => new Array(board[0].length).fill(false));
      visited[x][y] = true;
      while (queue.length) {
        const v = queue.shift();
        for (let i = 0; i < 4; i++) {
          const res = direction[i](v[0], v[1]);
          if (res === -1) continue;
          const [xx, yy] = res;
          if (xx < 0 || yy < 0 || xx >= board.length || yy >= board[0].length)
            continue;
          if (visited[xx][yy]) continue;

          visited[xx][yy] = true;

          if (board[xx][yy] === "G") return v[2];

          queue.push([xx, yy, v[2] + 1]);
        }
      }
      return -1;
    };
    return bfs(...start);
  }
```
