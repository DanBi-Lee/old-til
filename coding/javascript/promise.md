# Promise

## Promise

{% embed url="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global\_Objects/Promise" %}

비동기적 상황에서 코드를 명확하게 사용할 수 있다.

ES6부터 JavaScript의 표준 내장 객체로 추가되었습니다. ES6를 지원하는 브라우저나 Node.js에서 전역에 있는 Promise를 확인할 수 있습니다.

```javascript
/*
생성자를 통해서 프로미스 객체를 만들 수 있다.
새성자의 인자로 executor라는 함수를 이용한다.
*/
​
new Promise(/* excutor (함수가 들어올 자리) */);
```

> executor : 집행자

excutor 함수는 resolve와 reject를 인자로 가진다. `(resolve, reject)=>{ ... }` resolve와 reject는 함수이다. `resolve()`, `reject()`

```javascript
new Promise( (resolve, reject)=> {} )
```

1. 생성자를 통해서 프로미슷 객체를 만드는 순간 pending\(대기\) 상태라고 한다.

```javascript
new Promise( (resolve, reject)=> {} ); // pending
```

1. excutor함수 인자 중 하나인 resolve 함수를 실행하면, fulfilled\(이행\)상태가 된다.

```javascript
new Promise( (resolve, reject)=> {
    //
    // ...
    resolve(); // fulfilled
} );
```

1. excutor함수 인자 중 하나인 reject 함수를 실행하면, reject\(거부\)상태가 된다.

```javascript
new Promise( (resolve, reject)=> {
    reject(); // rejected
} );
```

```javascript
/*
1. p라는 프로미스 객체는 1000ms 후에 fulfilled된다.
2. fulfilled되는 시점에 p.then 안에 설정한 callback함수가 실행된다.
*/
​
const p = new Promise( (resolve, reject)=> {
    /* pending */
    setTimeout(()=>{
        resolve(); /*fulfilled*/
    }, 1000);
});
​
p.then(/*callback*/); // resolve 함수가 실행 된 뒤에 이 callback이 실행된다.
```

