---
layout: single
title: "[프로그래머스] 오픈채팅방"
categories:
  - Programmers
tag: [Coding Test, JS]
toc: true
---

## 📖 문제

<https://programmers.co.kr/learn/courses/30/lessons/42888>

## ✏️ 나의 풀이

- 가장 먼저 든 고민은 <U>Change</U> 되는 닉네임이다.
- 그러기 위해 <U>uid 라는 Object</U>를 만들어 모든 유저들의 닉네임과 아이디를 저장한다.
- 모든 유저들은 <U>한번 이상은 Enter</U> 하기때문에 Leave 를 제외한 상황에서 유저 아이디와 닉네임을 저장한다.
- Object 의 키는 중복되지 않기에 Change 여도 닉네임이 최신닉네임으로 업데이트 된다.

## 👩‍💻 코드

```javascript
function solution(record) {
  var answer = [];
  const uid = {};
  record.forEach((v) => {
    v = v.split(" ");
    if (v[0] !== "Leave") {
      uid[v[1]] = v[2];
    }
  });
  record.forEach((v) => {
    v = v.split(" ");
    if (v[0] === "Enter") {
      answer.push(`${uid[v[1]]}님이 들어왔습니다.`);
    } else if (v[0] === "Leave") {
      answer.push(`${uid[v[1]]}님이 나갔습니다.`);
    }
  });
  return answer;
}
```
