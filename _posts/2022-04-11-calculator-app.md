---
layout: single
title: "calculator - frontend 과제"
categories: 
- Frontend Mentor
tag: [JS, CSS, html]
toc: true
---
완성본😀 [Calculator](https://han0224.github.io/calculator-app-main/)

## 📕 이번 과제를 하면서 배운 것
<details>
<summary>prefers-color-scheme 미디어 퀴리</summary>
<div markdown="1">

> 운영체제에서 설정된 라이트/다크 모드를 실시간으로 감지하여 최적화된 스타일을 적용


```css
@media (prefers-color-scheme: ligth){
    /* light 모드에 적용할 스타일 */
}
```
```css
@media (prefers-color-scheme: dark){
    /* dark 모드에 적용할 스타일 */
}
```

[추가 정보](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme)

</div>
</details>


<details>
<summary>css variables</summary>
<div markdown="1">

> CSS 에서도 변수를 선언 할 수 있다. 일반적으로 아래 규칙을 따른다.

1. :root 의사 클래스에 선언
1. 두 개의 붙임표로 시작

[추가정보](https://developer.mozilla.org/ko/docs/Web/CSS/Using_CSS_custom_properties)

</div>
</details>
<details>
<summary>eval함수와 eval 함수의 위험성</summary>
<div markdown="1">

> eval 은 문자로 표현된 JavaScript 코드를 실행하는 함수이다.

이에 대한 자세한 것은 포스팅 할 예정!

[추가정보](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/eval)
</div>
</details>


## 🔮 완성 이미지
![화면 캡처 2022-04-21 135509](https://user-images.githubusercontent.com/70616579/164374961-eb80d976-14b8-47cb-8fd3-9f29de1a7e43.png){: width="50%" height="50%"}
![화면 캡처 2022-04-21 135604](https://user-images.githubusercontent.com/70616579/164375072-8819db07-a170-4285-a386-9cfc0398e13b.png){: width="50%" height="50%"}
![화면 캡처 2022-04-21 135619](https://user-images.githubusercontent.com/70616579/164375076-9c359445-3f22-43b4-ba94-3ae699a563bd.png){: width="50%" height="50%"}


## 💎 코드
CSS 변수 이용
```css
.theme1 {
  --main-background: hsl(222, 26%, 31%);
  --toggle-keypad-background: hsl(223, 31%, 20%);
  ...
}
.theme2 {
  --main-background: hsl(0, 0%, 90%);
  --toggle-keypad-background: hsl(0, 5%, 81%);
  ...
}
.theme3 {
  --main-background: hsl(268, 75%, 9%);
  --toggle-keypad-background: hsl(268, 71%, 12%);
  ...
}
body {
  background-color: var(--main-background);
  ...
}
header {
  color: var(--input-color);
  ...
}
```

body 의 클래스 이름을 변경하며 색상 변경
```javascript
const setTheme = (e) => {
  const target = e.target;
  const body = document.getElementsByTagName("body");
  if (target.id) {
    body[0].className = target.id;
  }
};
```

## 😊 느낀점

계산기를 구현하는 것을 너무 간단하게 생각을 했었다.

고려해야할 점이 너무 많아 생각보다 오래 걸렸다.

소수점은 최대 한번만 입력이 가능 한점, 숫자의 가장 앞에 0이 포함되면 안되는 점..

등등 고려해야 할 점을 미리 생각해놓지 않아 코드를 수정하고 계속 수정하게 되었다.

앞으로는 미리 한번 정의를 하는 습관을 들여놔야 겠다..

<br/>

최대한 eval 함수를 사용하지 않고 구해보려 했지만 결국 eval 함수를 사용하고 말았다..

나중에 코드를 수정할 일이 생기면 그때는 eval 함수를 사용하지 않고 다시 구현해볼 예정이다!
