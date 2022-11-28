---
layout: single
title: "[js] 제너레이터"
categories:
  - JavaScript
tag: [제너레이터]
toc: true
---

> ES6에서 도입된 코드 블록의 실행을 제어할 수 있는 특수한 함수

## 제너레이터 함수 vs 일반 함수

1. 제너레이터 함수는 호출자에게 함수 실행의 제어권을 양도할 수 있다.
  - 일반 함수를 호출할 경우 제어권은 함수가 갖고 함수가 일괄적으로 실행된다. 즉, 함수를 호출한 후에는 제어가 불가능하다.
1. 제너레이터 함수는 함수 호출자와 함수 상태를 주고 받을 수 있다.
  - 일반 함수는 매개변수를 통해 외부에서 값을 받을 수 있고 결과값을 외부에 반환한다. 즉, 함수가 실행된 이후 내부 상태를 변경할 수 없다.
1. 제너레이터 함수를 호출하면 제너레이터 객체를 반환한다.
  - 일반 함수를 호출할 경우 코드를 일괄 실행한 후 결과값을 반환한다.

## 제너레이터 함수

제너레이터 함수는 `function*` 키워드로 선언한다. 그리고 하나 이상의 `yield` 표현식을 포함한다. 그 외는 일반 함수와 똑같다.

```javascript
// 함수 선언문
function* Func(){  yield 1;  }
// 함수 표현식
const Func = function*(){  yield 1;  }
// 메서드
const obj = {
  * Func(){  yield 1;  }
}
// 클래스 메서드
class myclass{
  * Func(){  yield 1;  }
}
```

- 화살표 함수로 정의 불가능
- `new` 연산자와 함께 생성자 함수로 호출 불가능

##  제너레이터 객체
> Symbol.iterator 메서드를 상속받는 이터러블이면서 value, doen 프로퍼티를 갖는 이터레이터 리절트 객체를 반환하는 next 메서드를 소유한 이터레이터

```
  이터러블: 이터러블 프로토콜을 준수한 객체로써, for ... of 문으로 순회할 수 있는 객체
  이터레이터: 이터러블의 Symbol.iterator 메서드를 호출하면 이터레이터 프로토콜을 준수하는 이터레이터를 반환
  이터레이터 리절트 객체: 이터레이터의 next 메서드를 통해 이터러블을 순차적으로 한 단계씩 순회하며 순회 결과를 나타내는 객체
```

제너레이터 함수를 호출하면 제너레이터 객체를 반환한다. 제너레이터 객체의 어떤 메서드를 호출하느냐에 따라 결과값이 달라진다.

1. next 메서드로 호출할 경우
  - `yield` 표현식까지 코드블록을 실행
  - 이터레이터 리절트 객체: `{value: yield된 값, done: false}`
1. return 메서드로 호출할 경우
  - 이터레이터 리절트 객체: `{value: 프로퍼티 값, done: true}`
1. throw 메서드로 호출할 경우
  - 이터레이터 리절트 객체: `{value: undefined, done: true}`
  
## yield 키워드, next 메서드

제너레이터는 yield 키워드와 next 메서드를 통해 함수 실행을 제어할 수 있다. next 메서드를 호출하면 yield 표현식까지만 실행하고 일시 중지한다. 한번 더 next 메서드를 호출하면 이전 실행이 중지된 부분부터 다시 yield 표현식까지 실행한다.

```javascript
function* func(){
  yield 1;
  yield 2;
}
const generator = func();
console.log(generator.next()); // {value: 1, done: false}
console.log(generator.next()); // {value: 2, done: false}
console.log(generator.next()); // {value: undefined, done: true}
```
위의 코드에서 3번째로 next 메서드를 호출할 경우 남은 yield 표현식이 없으므로 함수의 마지막까지 실행이되면서 함수가 끝까지 실행이 되었음을 나타내는 `done: true` 이 반환된다.

### next 메서드의 인자

이터레이터의 next 메서드는 인수를 전달할 수 없다. 하지만 제너레이터 객체의 next 메서드의 경우 인수를 전달할 수 있다.

전달된 인자는 제너레이터 함수의 yield 표현식을 할당받는 변수에 할당된다.

```javascript
function* func(){
  const x = yield 3;
  const y = yield (x + 2);
  return x + y;
}
const generator = func();
console.log(generator.next()); // {value: 3, done: false}
console.log(generator.next(10)); // {value: 12, done: false}
console.log(generator.next(20)); // {value: 30, done: true}
```
1. 처음 next 메서드를 호출했을 경우 x에 3이 할당되지 않은 상태에서 중지된다. 
  - x의 값은 다음 next 메서드가 호출될때 결정된다.
1. 두번째 next 메서드를 호출했을 경우 `const x = yield 3;`부터 실행된다. 
  - 이때, next의 인수로 10을 주었기에 yield 표현식을 할당받는 x에 할당된다. 즉, x의 값은 10이 된다.
1. 두번째 yield된 값 x + 2은 next 메서드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에 할당된다. 
  - 즉, value는 10+2인 12가 된다.
1. 세번째 next 메서드를 호출했을 경우 `const y = yield (x + 2);`부터 실행된다. 
  - 이때, next의 인수로 20을 주었기에 yield 표현식을 할당받는 y에 할당된다. 즉, y의 값은 20이 된다. 
1. 더이상의 yield가 없으므로 세번째 next 메서드는 함수의 끝까지 실행된다. 
  - 이때 value는 함수의 반환값인 `x+y`가 된다. 
  - 즉, 10+20인 30이 이터레이터 리절트객체의 value가 된다. 
  - 또한, 함수의 실행이 종료되었으므로 done은 true가 된다.

## 단점
제너레이터를 통해 비동기를 동기처러 동작하도록 구현할 수 있으나 코드가 장황해지면서 가독성역시 나빠졌다. 이러한 단저을 보안하기 위해 나온 것이 async/await이다. async/await은 제너레이터를 이용하는 것보다 간단하고 가독성이 좋다.

async/await은 ES8에서 도입되었으며, 프로미스 기반으로 동작한다. 기존 프로미스의 복잡한 후속처리를 간단하게 처리할 수 있다는 장점이 있다.