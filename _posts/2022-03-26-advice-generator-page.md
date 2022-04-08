---
layout: single
title: "Advice generator app - frontend 과제"
categories: 
- Frontend Mentor
tag: [JS, CSS, html, fetch]
toc: true
---
완성본😀 [Advice generator app](https://han0224.github.io/advice-generator-app/)
## 📕 이번 과제를 하면서 배운 것
- api 호출 - fetch
- 명언 호출 api: Advice Slip API

## 🔮 완성 이미지
![화면 캡처 2022-03-26 174526](https://user-images.githubusercontent.com/70616579/160231972-dd54dbac-9903-4c94-9d78-495ecb4c34ea.png){: width="40%" height="40%"}
![화면 캡처 2022-03-26 174544](https://user-images.githubusercontent.com/70616579/160231973-c6a35279-562c-45c8-b268-c43abb0642ca.png){: width="40%" height="40%"}  
- 버튼을 누를 시 랜덤으로 명언을 보여줌   
- 명언과 해당 명언의 id 번호를 화면에 출력

## 💎 코드
```javascript
// index.js
const id = document.querySelector('.adviceId')
const goes = document.querySelector('.adviceGoes')

const url = 'https://api.adviceslip.com/advice'

const btnClick = () =>{
    getAdvice();
}

const getAdvice = () =>{
    fetch(url)
    .then(res=>res.json())
    .then(data=>{
        goes.innerHTML = `"${data.slip.advice}"`
        id.innerHTML = `ADVICE #${data.slip.id}`
        console.log(data.slip.advice, data.slip.id)
    })
}

getAdvice();
```
- 첫 화면에서 랜덤 명언을 띄우기 위해 getAdvice() 함수를 한번 실행
- 버튼을 클릭 할때마다 btnClick() 실행
- fetch 함수를 이용해 Advice Slip API 호출

## 😊 느낀점
fetch 함수를 이용해 get 요청을 해보았다.   
api 호출을 너무 어렵게 생각했었다.   
그러나 간단한 호출을 해보니 그렇게 겁먹을 것은 아니였다!   
post 호출은 어떤 식으로 하는지 좀 더 공부해보고 포스팅 해봐야겠다!   
