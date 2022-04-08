---
layout: single
title: "[프로그래머스] 괄호 변환"
categories:
  - Programmers
tag: [Coding Test, JS]
toc: true
---

## 📖 문제

<https://programmers.co.kr/learn/courses/30/lessons/60058>

- 문제에서 알려준 알고리즘

```
1. 입력이 빈 문자열인 경우, 빈 문자열을 반환합니다.
2. 문자열 w를 두 "균형잡힌 괄호 문자열" u, v로 분리합니다. 단, u는 "균형잡힌 괄호 문자열"로 더 이상 분리할 수 없어야 하며, v는 빈 문자열이 될 수 있습니다.
3. 문자열 u가 "올바른 괄호 문자열" 이라면 문자열 v에 대해 1단계부터 다시 수행합니다.
  3-1. 수행한 결과 문자열을 u에 이어 붙인 후 반환합니다.
4. 문자열 u가 "올바른 괄호 문자열"이 아니라면 아래 과정을 수행합니다.
  4-1. 빈 문자열에 첫 번째 문자로 '('를 붙입니다.
  4-2. 문자열 v에 대해 1단계부터 재귀적으로 수행한 결과 문자열을 이어 붙입니다.
  4-3. ')'를 다시 붙입니다.
  4-4. u의 첫 번째와 마지막 문자를 제거하고, 나머지 문자열의 괄호 방향을 뒤집어서 뒤에 붙입니다.
  4-5. 생성된 문자열을 반환합니다.
```

## ✏️ 나의 풀이

해당 문제에서 알고리즘을 알려주지 않았으면 못풀었을 것 같다.

문제에서 주어진 알고리즘대로 코드를 작성하다 한 고민이 들었다.

균형잡힌 괄호가 올바른 괄호 문자열인지 확인 하는 것이였다.

반복문을 사용하여 균형잡힌 괄호가 올바른 괄호인지 확인하는 방법 말고 다른 방법을 고민하던 중 균형잡힌 괄호에 대해 다시 생각해보았다.

<U>애시당초 균형잡힌 괄호였기에 균형잡힌 괄호에서 0번째 인덱스가 (이면 균형잡힌 괄호이면서 올바른 괄호이다.</U>

재귀함수를 작성하는 것이 아직 너무 서툴러 생각보다 오래걸렸지만 재귀함수를 작성할 때 중요한 점만 기억하면 된다는 것을 잊지말자!

## 👩‍💻 코드

```javascript
const string = (p) => {
  if (p === "") return "";
  let answer = "";
  const uStack = [];
  const vStack = [...p];
  while (true) {
    uStack.push(vStack.shift());
    if ( uStack.length % 2 === 0 && uStack.filter((e) => e === ")").length === uStack.length / 2 ) break;
  }
  if (uStack[0] === ")") {
    answer += "(";
    answer += string(vStack.join(""));
    answer += ")";
    uStack.pop();
    uStack.shift();
    uStack.forEach((v) => {
      if (v === ")") answer += "(";
      else answer += ")";
    });
  } else {
    answer += uStack.join("");
    answer += string(vStack.join(""));
  }
  return answer;
};
function solution(p) {
  return string(p);
}
```
