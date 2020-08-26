# async - await

## async function과 await

{% embed url="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/async\_function" %}

* Async 사용법

```javascript
async function 함수이름(){}
​
const 함수이름 = async()=>{}
```

* 어떻게 쓰는가

```javascript
// Promise 객체를 리턴하는 함수
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            resolve(ms);
        }, ms);
    });
}
​
// Promise 객체를 이용해서 비동기 로직을 수행할 때
p(1000).then((ms)=>{
    console.log(`${ms} ms 후에 실행된다.`);
});
​
// Promise 객체를 리턴하는 함수를 await로 호출하는 방법
​
const ms = await p(1000); // ms가 return 값으로 혼다.
console.log(`${ms} ms 후에 실행된다.`);
// 위 경우 문법 오류
```

* await를 사용하는 경우, 항상 async 함수 안에서 사용되어야 한다.
  * async, await의 장점 : 코드를 흐름에 따라서 아래로 내려 쓸 수 있다.

```javascript
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            resolve(ms);
        }, ms);
    });
}
​
(async function main(){
    const ms = await p(1000);
    console.log(`${ms} ms 후에 실행된다.`);
})();
```

* Promise 객체가 rejected 된 경우의 처리를 위해 `try cath`를 이용한다.

```javascript
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            //resolve(ms);
            reject(new Error('reason'));
        }, ms);
    });
}
​
(async function main(){
    try{
        const ms = await p(1000);
    } catch(error){
        console.log(error);
    }
})();
```

* async function 에서 return 되는 값은 `Promise.resolve` 함수로 감싸서 리턴된다.

```javascript
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            resolve(ms);
        }, ms);
    });
}
​
async function asyncP(){
    const ms = await p(1000); // 먼저 해결하려 한다.
    return 'Mark: ' + ms;
}
​
(async function main(){
    try{
        const name = await asyncP(1000);
        console.log(name);
    } catch(error){
        console.log(error);
    }
})();
​
// 결과 : 1초 후 name+ms 리턴
```

* error의 전파

```javascript
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            // resolve(ms);
            reject(new Error('reason'));
        }, ms);
    });
}
​
async function asyncP(){
    const ms = await p(1000); // 먼저 해결하려 한다. (에러나는게 다음으로 넘어감)
    return 'Mark: ' + ms;
}
​
(async function main(){
    try{
        const name = await asyncP(1000);
        console.log(name);
    } catch(error){
        console.log(error); // 여기 error로 보여짐
    }
})();
​
// 결과 : 1초 후 에러
```

* finally

```javascript
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            // resolve(ms);
            reject(new Error('reason'));
        }, ms);
    });
}
​
async function asyncP(){
    const ms = await p(1000); // 먼저 해결하려 한다. (에러나는게 다음으로 넘어감)
    return 'Mark: ' + ms;
}
​
(async function main(){
    try{
        const name = await asyncP(1000);
        console.log(name);
    } catch(error){
        console.log(error); // 여기 error로 보여짐
    } finally {
        console.log('end'); // 마지막에 호출
    }
})();
​
// 결과 : 1초후 에러가 출력된 후 finally 호출
```

* 연속된 Promise로 된 처리와 연속된 async await의 비교

```javascript
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            resolve(ms);
        }, ms);
    });
}
​
// Promise
p(1000).then(()=>p(1000)).then(()=>p(1000)).then(()=>{
    console.log('3000ms 후에 실행');
});
​
// async await
(async function main(){
    await p(1000);
    await p(1000);
    await p(1000);
    console.log('3000ms 후에 실행');
})();
```

* Promise.all 가 Promise.race를 async await로 표현하는 방법

```javascript
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            resolve(ms);
        }, ms);
    });
}
​
// Promise.all
(async function main(){
    const results = await Promise.all([p(1000), p(2000), p(3000)]);
    console.log(results);
})();
​
// Promise.race
(async function main(){
    const result = await Promise.race([p(1000), p(2000), p(3000)]);
    console.log(result);
})();
```

