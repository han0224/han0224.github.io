---
layout: single
title: "[프로그래머스]이중우선순위큐"
categories:
  - Programmers
tag: [Coding Test, JS]
toc: true
---


## 📖 문제

[level3 리코쳇 로봇](https://school.programmers.co.kr/learn/courses/30/lessons/42628)

## ✏️ 나의 풀이

사실 이 문제는 정확성 테스트만 있었기에 단순히 정렬로만 풀 수 있는 문제다.

하지만, 힙을 연습하기 위해 푸는 문제이기에 최소 힙을 이용해 문제를 풀어보았다.

<br/>

우선 기본에 알고 있던 최소힙을 구현한다.

삽입, 삭제를 구현했으먄 삭제하는 메소드를 수정해주어야 한다.

단순 최소힙은 큐에서 최소값은 삭제할 수 있지만 최대값은 삭제 할 수 없다.

그래서 여기서 오랜 시간을 소요했다.

생각을 해보니 큐애 았는 최대값은 무조건 leafNode에 있다는 사실을 깨닫게 되었다.

그렇기에 최대값을 삭제해야하는 경우 leafNode들 중 가장 큰 값을 찾는 로직을 추가했다.


```javascript
  if (flag === "max") {
    const parentIndex = Math.floor(this.getSize() / 2);
    const leafNodes = this.queue.splice(parentIndex);
    const max = Math.max(...leafNodes);
    const maxIndex = leafNodes.indexOf(max);
    this.queue.push(
      ...leafNodes.slice(0, maxIndex),
      ...leafNodes.slice(maxIndex + 1)
    );
    return max;
  }
```

가장 마지막 노드의 부모의 인덱스보다 큰 노드들은 leafNode 이므로 leafNode들을 잘라서 새로운 배열에 선언해준다.

leafNode들 중에서 가장 큰 노드를 찾아 해당 노드를 삭제해 기존 배열에 업데이트된 leafNode들을 붙어 준다.

<br/>

마지막으로 결과를 추출하는 부분은 비교적 간단하다.

1. 만일 배열이 비어있다면 [0, 0]을 반환한다.
1. 만일 배열의 길이가 1이면 배열의 있는 유일한 요소를 담은 배열을 반환한다.
1. 위 두조건에 만족하지 않으면 기존에 만들어둔 pop메소드를 이용해 최소와 최대를 구해 각각을 배열에 담아 반환한다.

```javascript
  result() {
    if (this.isEmpty()) return [0, 0];
    if (this.getSize() === 1) return [this.queue[1], this.queue[1]];
    const max = this.pop("max");
    const min = this.pop("min");
    return [max, min];
  }
```

## 👩‍💻 코드

### 최소힙을 이용해
```javascript
class MinHeap {
    constructor() {
      this.queue = [null];
    }

    push(num) {
      this.queue.push(num);
      let curIndex = this.getSize();

      while (curIndex > 1) {
        const parentIndex = Math.floor(curIndex / 2);
        if (this.queue[parentIndex] > num) {
          this.swap(parentIndex, curIndex);
          curIndex = parentIndex;
        } else break;
      }
    }

    pop(flag) {
      if (this.isEmpty()) return null;
      if (this.getSize() === 1) return this.queue.pop();
      if (flag === "max") {
        const parentIndex = Math.floor(this.getSize() / 2);
        const leafNodes = this.queue.splice(parentIndex);
        const max = Math.max(...leafNodes);
        const maxIndex = leafNodes.indexOf(max);
        this.queue.push(
          ...leafNodes.slice(0, maxIndex),
          ...leafNodes.slice(maxIndex + 1)
        );
        return max;
      }
      const last = this.queue.pop();
      const res = this.queue[1];
      this.queue[1] = last;
      let curIndex = 1;
      let leftChildIndex = 2;
      let rightChildIndex = 3;
      while (curIndex < this.getSize()) {
        leftChildIndex = curIndex * 2;
        rightChildIndex = curIndex * 2 + 1;
        if (!this.queue[leftChildIndex]) break;
        if (!this.queue[rightChildIndex]) {
          this.swap(curIndex, leftChildIndex);
          break;
        }
        if (this.queue[leftChildIndex] > this.queue[rightChildIndex]) {
          this.swap(curIndex, rightChildIndex);
          curIndex = rightChildIndex;
        } else {
          this.swap(curIndex, leftChildIndex);
          curIndex = leftChildIndex;
        }
      }
      return res;
    }

    getSize() {
      return this.queue.length - 1;
    }

    isEmpty() {
      return this.queue.length === 1;
    }

    swap(index1, index2) {
      const tmp = this.queue[index1];
      this.queue[index1] = this.queue[index2];
      this.queue[index2] = tmp;
    }

    result() {
      if (this.isEmpty()) return [0, 0];
      if (this.getSize() === 1) return [this.queue[1], this.queue[1]];
      const max = this.pop("max");
      const min = this.pop("min");
      return [max, min];
    }
  }

  function solution(operations) {
    var answer = [];
    const queue = new MinHeap();

    for (let i of operations) {
      const [oper, num] = i.split(" ");
      if (oper === "I") {
        queue.push(Number(num));
      } else {
        queue.pop(Number(num) === 1 ? "max" : "min");
      }
    }
    return queue.result();
  }
```
<img width="431" alt="heap" src="https://github.com/woorifisa-projects/GoodFriends/assets/70616579/31da5781-f39d-4f80-b89d-587de2c6bf08">




### 단순 정렬을 이용해

이렇게 어렵게 풀었지만, 실제 이 문제는 단순히 정렬로만으로도 풀 수 있다.

```javascript
 function solution(operations) {
    var answer = [];

    for (let i of operations) {
      const [oper, num] = i.split(" ");
      if (oper === "I") {
        answer.push(Number(num));
        answer.sort((a, b) => b - a);
      } else {
        if (Number(num) === 1) {
          answer.shift();
        } else {
          answer.pop();
        }
      }
    }
    if (answer.length === 0) {
      return [0, 0];
    }
    return [Math.max(...answer), Math.min(...answer)];
  }
```



<img width="422" alt="sort" src="https://github.com/woorifisa-projects/GoodFriends/assets/70616579/cc23b9b0-c707-4cd5-8b57-8383b04a2aa3">


하지만, 실제 시간을 보면 확싫이 최소힙을 이용해서 푼게 더 적은 시간이 걸리는 것을 확인할 수 있다.