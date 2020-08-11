# JS 크롬 앱 만들기

## 크롬 앱 만들기

{% embed url="https://nomadcoders.co/javascript-for-beginners" %}

{% hint style="info" %}
**목표** : 강의를 참고하여 크롬 앱 클론 제작

* 강의 외 추가 목표
  * gulp 활용하기
  * 이미지 사이트 API 활용하기
  * 기능 보완
{% endhint %}

* [x] 시계 만들기
* [ ] 유저 이름 입력창
* [ ] ToDoList 만들기
* [ ] 이미지 불러오기
* [ ] 날씨 불러오기

### 1. 시계만들기

#### part 1

1. `index.html`작성
2. `clock.js`작성

   > **js 작성 팁**
   >
   > * `init`함수를 생성하고, 함수를 각각 분할한다.

```javascript
const clockContainer = document.querySelector(".js-clock"),
  clockTitle = clockContainer.querySelector("h1");
​
function getTime() {
  const date = new Date();
  const minutes = date.getMinutes();
  const hours = date.getHours();
  const seconds = date.getSeconds();
  clockTitle.innerText = `${hours}:${minutes}:${seconds}`;
}
​
function init() {
  getTime();
}
​
init();
```



#### part 2

> **TIP**
>
> 삼항 연산자 활용  
> \(조건\) ? \(참일 경우\) : \(거짓일 경우\)

### 2. 유저 이름 입력

### 3. ToDoList 만들기

### 4. 이미지 불러오기

### 5. 날씨 불러오기



