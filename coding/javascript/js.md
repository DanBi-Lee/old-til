# JS 크롬 앱 만들기

## 크롬 앱 만들기

{% embed url="https://nomadcoders.co/javascript-for-beginners" %}

{% hint style="info" %}
**목표** : 강의를 참고하여 크롬 앱 클론 제작

* 강의 외 추가 목표
  * gulp 활용하기
  * 이미지 사이트 API 활용하기
  * 기능 보완
    * 찾은 버그 
      * 투두 리스트의 목록 삭제 후, 다시 리스트 등록 시 id가 중복되는 현상
{% endhint %}

* [x] 시계 만들기
* [x] 유저 이름 입력창
* [x] ToDoList 만들기
* [x] 이미지 불러오기
* [x] 날씨 불러오기

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

#### part1 : 목록그리기

* 방법은 `greeting.js`와 비슷
* `document.createElement()`
* `appendChild()`함수를 활용

#### part2 : 목록 저장하기

1. 할 일 목록 저장 \(목록은 array\)
2. `JSON.stringify()`는 자바스크립트 object를 string으로 바꿔준다.
3. `JSON.parse()`는 불러온 JSON을 object로 변환해준다.
4. `forEach()`함수를 사용하여 array를 반복 처리한다.

#### part3 : 목록 지우기

1. local storage에서 to do 하나 지우기
   * `filter()`함수 사용
2. 그런 다음 저장하기
3. html에서도 지우기
   * `event.target.parentNode`
   * `removeChild()`함수 사용

```javascript
const toDoForm = document.querySelector(".js-toDoForm"),
    toDoInput = toDoForm.querySelector("input"),
    toDoList = document.querySelector(".js-toDoList");
​
const TODOS_LS = "toDos";
​
let toDos = [];
​
function deleteToDo(event){
    console.log(event.target.parentNode);
    const btn = event.target;
    const li = btn.parentNode;
    toDoList.removeChild(li);
    const cleanToDos = toDos.filter(function(toDo){
        return toDo.id !== parseInt(li.id);
    });
    console.log(cleanToDos);
    toDos = cleanToDos;
    saveToDos();
}
​
function saveToDos(){
    localStorage.setItem(TODOS_LS, JSON.stringify(toDos));
}
​
function paintToDo(text){
    const li = document.createElement("li");
    const delBtn = document.createElement("button");
    delBtn.innerText = "X";
    delBtn.addEventListener("click", deleteToDo);
    const span = document.createElement("span");
    const newId = toDos.length + 1;
    span.innerText = text;
    li.appendChild(delBtn);
    li.appendChild(span);
    li.id = newId;
    toDoList.append(li);
    const toDoObj = {
        text : text,
        id : toDos.length + 1
    };
    toDos.push(toDoObj);
    saveToDos();
}
​
function handleSubmit(event){
    event.preventDefault();
    const currentValue = toDoInput.value;
    paintToDo(currentValue);
    toDoInput.value = "";
}
​
function loadToDos(){
    const loadedToDos = localStorage.getItem(TODOS_LS);
    if(loadedToDos !== null){
        const parseToDos = JSON.parse(loadedToDos);
        parseToDos.forEach(function(toDo){
            paintToDo(toDo.text);
        })
    }
}
​
function init(){
    loadToDos();
    toDoForm.addEventListener("submit", handleSubmit);
}
​
init();
```

### 4. 이미지 불러오기

```javascript
Math.ceil() // 올림
Math.floor() // 버림
```

```javascript
const body = document.querySelector("body");

const IMG_NUMBER = 5;

function paintImage(imgNumber){
    const image = new Image();
    image.src = `../img/background_${imgNumber + 1}.jpg`;
    image.classList.add("bgImage");
    body.appendChild(image);
}

function genRandom(){
    const number = Math.floor(Math.random() * IMG_NUMBER);
    return number;
}

function init(){
    const randomNumber = genRandom();
    paintImage(randomNumber);
}

init();
```

### 5. 날씨 불러오기

1. 좌표 불러오기 \(로컬 스토리지에서\)
   * 값이 없으면
     * 좌표값을 물어봄

       ```text
        navigator.geolocation.getCurrentPosition(성공했을 때 실행, 실패했을 때 실행)
       ```
   * 값이 있으면
     * 그대로 사용
2. 날씨 불러오기

   1. https://openweathermap.org/ 가입
   2. [https://home.openweathermap.org/api\_keys](https://home.openweathermap.org/api_keys) 키 받기
   3. 날씨 정보를 받을 수 있는 url확인

      > 예시 : https://samples.openweathermap.org/data/2.5/weather?lat=35&lon=139&appid=439d4b804bc8187953eb36d2a8c26a02

   ```text
   function getWeather(lat, lng){
       fetch(
           `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lng}&appid=${API_KEY}&units=metric`
       ).then(function(response){
           console.log(response.json()); //데이터 불러오
       }).then(function(json){ //데이터 불러온 다음 실행
           console.log(json);
       });
   }
   ```

```javascript
const weather = document.querySelector(".js-weather");

const API_KEY = "875e80633fecba3610cdb9887449e624";
const COORDS = 'coords';

function getWeather(lat, lng){
    fetch(
        `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lng}&appid=${API_KEY}&units=metric`
    ).then(function(response){
        console.log(response);
        return response.json()
    }).then(function(json){
        console.log(json);
        const temperature = json.main.temp;
        const place = json.name;
        weather.innerText = `${temperature} @ ${place}`;
    });
}

function saveCoords(coordsObj){
    coordsObj = JSON.stringify(coordsObj);
    localStorage.setItem(COORDS, coordsObj);
}

function handleGeoSuccess(position){
    const latitude = position.coords.latitude;
    const longitude = position.coords.longitude;
    const coordsObj = {
        latitude,
        longitude
    };
    saveCoords(coordsObj);
    getWeather(latitude, longitude);
}

function handleGeoError(){
    console.log('Cant get Geo');
}

function askForCoords(){
    navigator.geolocation.getCurrentPosition(handleGeoSuccess, handleGeoError);
}

function loadCoords(){
    const loadedCords = localStorage.getItem(COORDS);
    console.log(loadedCords);
    if(loadedCords === null){
        askForCoords();
    }else{
        const parseCoords = JSON.parse(loadedCords);
        getWeather(parseCoords.latitude, parseCoords.longitude);
    }
}

function init(){
    loadCoords();
}

init();
```

