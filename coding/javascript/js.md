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
* [x] 유저 이름 입력창
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

#### part 1, 2

1. form, input 태그 생성
2. Local Storage 이용
   * 로컬 스토리지 저장

     ```text
     localStorage.setItem(/*key*/, /*value*/);
     ```

   * 로컬 스토리지 값 불러오기

     ```text
     localStorage.getItem(/*key*/);
     ```
3. local storage여부에 따라서
   1. 있으면 : 인사 그리기

      ```text
      const form = document.querySelector(".js-form"),
          input = form.querySelector("input"),
          greeting = document.querySelector(".js-greetings");
      ​
      const USER_LS = "currentUser",
          SHOWING_CN = "showing";
      ​
      function paintGreeting(text){
          form.classList.remove(SHOWING_CN);
          greeting.classList.add(SHOWING_CN);
          greeting.innerText = `Hello ${text}`;
      }
      ```

   2. 없으면 ? 이름 물어보기
      1. 이름 묻는 form태그 보이도록 처리
      2. input에 이름을 물어봤을 때 이벤트 제어
         1. 기본 submit이벤트를 제거한다.

            ```text
            function handleSubmit(event){
                event.preventDefault();
            }
            ```

         2.  입력 받은 이름을 그린다.

            ```text
            const value = input.value;
            paintGreeting(value);
            ```

         3. 로컬 스토리지에 저장한다.

            ```text
            function saveName(text){
                localStorage.setItem(USER_LS, text);
            }
            ```

```javascript
const form = document.querySelector(".js-form"),
    input = form.querySelector("input"),
    greeting = document.querySelector(".js-greetings");
​
const USER_LS = "currentUser",
    SHOWING_CN = "showing";
​
function saveName(text){
    localStorage.setItem(USER_LS, text);
}
​
function handleSubmit(event){
    event.preventDefault();
    const value = input.value;
    saveName(value);
    paintGreeting(value);
}
​
function askForName(){
    form.classList.add(SHOWING_CN);
    form.addEventListener("submit", handleSubmit);
}
​
function paintGreeting(text){
    form.classList.remove(SHOWING_CN);
    greeting.classList.add(SHOWING_CN);
    greeting.innerText = `Hello ${text}`;
}
​
function loadName(){
    const currentUser = localStorage.getItem(USER_LS);
    if(currentUser === null){
        askForName();
    } else {
        paintGreeting(currentUser);
    }
}
​
function init(){
    loadName();
}
​
init();
```

### 3. ToDoList 만들기

### 4. 이미지 불러오기

### 5. 날씨 불러오기



