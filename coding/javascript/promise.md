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

* 생성자를 통해서 프로미 객체를 만드는 순간 pending\(대기\) 상태라고 한다.

```javascript
new Promise( (resolve, reject)=> {} ); // pending
```

* excutor함수 인자 중 하나인 resolve 함수를 실행하면, fulfilled\(이행\)상태가 된다.

```javascript
new Promise( (resolve, reject)=> {
    //
    // ...
    resolve(); // fulfilled
} );
```

* excutor함수 인자 중 하나인 reject 함수를 실행하면, reject\(거부\)상태가 된다.

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



```javascript
const p = new Promise((resolve, reject)=>{
    /* pending */
    setTimeout(()=>{
        resolve(); /* fulfilled */
    }, 1000);
});
​
p.then(()=>{
    console.log('1000ms 후에 fulfilled 된다.');
});
```

* 바로 Promise를 return하는 이유
  * then을 설정하는 시점을 정확히하고, 함수의 실행과 동시에 프로미스 객체를 만들면서 pending이 시작하도록 하귀 위해 프로미스 객체를 생성하면서 리턴하는 함수 p를 만들어 함수 p실행과 동시에 then을 설정한다.
  * 대규모 프로젝트에서 이와같이 사용한다.

```javascript
function p(){
    return new Promise((resolve, reject)=>{
        /* pending */
        setTimeout(()=>{
            resolve(); /* fulfilled */
        }, 1000);
    });
}
​
p().then(()=>{
    console.log('1000ms 후에 fulfilled 된다.');
});
```

* 프로미스 객체가 rejected 되는 시점에 p.catch안에 설정한 callback함수가 실행된다.

```javascript
function p(){
    return new Promise((resolve, reject)=>{
        /* pending */
        setTimeout(()=>{
            reject(); /* rejected */
        }, 1000);
    });
}
​
p().then(()=>{
    console.log('1000ms 후에 fulfilled 된다.');
}).catch(()=>{
    console.log('1000ms 후에 rejected된다.');
});
```

* executor의 resolve 함수를 실행할 때 인자를 넣어 실행하면, then의 callback 함수의 인자로 받을 수 있다.
  * 다음 동작에 필요한 메세지를 전달할 때 많이 이용한다.

```javascript
function p(){
    return new Promise((resolve, reject)=>{
        /* pending */
        setTimeout(()=>{
            resolve('hello'); /* fulfilled */
        }, 1000);
    });
}
​
p().then((message)=>{
    console.log('1000ms 후에 fulfilled 된다.', message);
}).catch(()=>{
    console.log('1000ms 후에 rejected된다.');
});
```

* 마찬가지로 executor의 reject함수를 실행할 때 인자를 넣어 실행하면, catch의 callback 함수의 인자로 받을 수 있다.

```javascript
function p(){
    return new Promise((resolve, reject)=>{
        /* pending */
        setTimeout(()=>{
            reject('error');
        }, 1000);
    });
}
​
p().then((message)=>{
    console.log('1000ms 후에 fulfilled 된다.', message);
}).catch((reason)=>{
    console.log('1000ms 후에 rejected된다.', reason);
});
​
/*
보통 reject 함수를 실행하며 rejected 되는 이유를 넘기는데, 
표준 내장 객체인 Error의 생성자를 이용하여 Error객체를 만든다.
*/
​
function p(){
    return new Promise((resolve, reject)=>{
        /* pending */
        setTimeout(()=>{
            reject(new Error('bad')); // Error객체 생성
        }, 1000);
    });
}
​
p().then((message)=>{
    console.log('1000ms 후에 fulfilled 된다.', message);
}).catch((reason)=>{
    console.log('1000ms 후에 rejected된다.', reason); // Error객체가 넘어옴
});
```

* fulfilled 되거나 rejected 된 후에 최종적으로 실행할 것이 있다면, `.finally()`를 설정하고, 함수를 인자로 넣는다.

```javascript
function p(){
    return new Promise((resolve, reject)=>{
        /* pending */
        setTimeout(()=>{
            reject(new Error('bad')); // Error객체 생성
        }, 1000);
    });
}
​
p().then((message)=>{
    console.log('1000ms 후에 fulfilled 된다.', message);
}).catch((reason)=>{
    console.log('1000ms 후에 rejected된다.', reason); // Error객체가 넘어옴
}).finally(()=>{
    console.log('end');
});
```

* 보통 비동기 작업을 할 때, callback 함수를 인자로 넣어 로직이 끝나면 callback 함수를 호출한다. 이런 경우 함수가 아래로 진행이 되지 않고, callback함수 안으로 진행된다.

```javascript
function c(callback){
    setTimeout(()=>{
        callback();
    }, 1000);
}
​
c(()=>{
    console.log('1000ms 후에 callback 함수가 실행됩니다.');
});
​
// 콜백지옥
c(()=>{
    c(()=>{
        c(()=>{
            console.log('3000ms 후에 callback 함수가 실행됩니다.');
        });
    });
});
​
/*
then 함수에서 다시 프로미스 객체를 리턴하는 방법을 통해 체이닝하면, 
비동기 작업을 순차적으로 아래로 표현할 수 있다.
*/
​
function p(){
    return new Promise((resolve, reject)=>{
       setTimeout(()=>{
           resolve();
       },1000); 
    });
}
​
p().then(()=>{
    return p();
})
.then(()=>p())
.then(p)
.then(()=>{
    console.log('4000ms 후에 fulfilled 됩니다.');
});
```

* `new Promise()`가 아닌 방식으로 `resolve()`메서드를 통해 promise를 사용할 수 있다.
  * value가 프로미스 객체인지 아닌지 알 수 없는 경우, 사용하면 연결된 then 메서드를 실행한다.
  * value가 프로미스 객체면, resolve된 then 메서드를 실행한다.
  * value가 프로미스 객체가 아니면, value를 인자로 보내면서 then 메서드를 실행한다.

```javascript
/* 
value안에 프로미스 객체를 넣을 수도 있고, 일반 객체를 넣을 수도 있다. 
*/
​
Promise.resolve(/* value */);
​
​
// value가 프로미스 객체
Promise.resolve(new Promise((resolve, reject)=>{
    setTimeout(()=>{
        resolve('foo');
    }, 1000);
})).then((data)=>{
    console.log('프로미스 객체인 경우, resolve된 결과를 받아서 then이 실행 된다.', data);
}); //resovle된 후에 then실행
​
// 객체가 아닌 경우
Promise.resolve('bar').then((data)=>{
    console.log('then 메서드가 없는 경우, fulfilled 된다.', data);
});
​
// 객체가 프로미스인지 아닌지 모를 경우, then메서드를 실행한다..
```

* `Promise.reject`를 사용하면, catch로 연결된 rejected 상태로 변경된다.

```javascript
Promise.reject(/* value */);
​
// 이런 문법도 가능하다.
Promise.reject(new Error('reason'))
    .then(error => {})
    .catch(error => {
    console.log(error);
});
```

* 프로미스 객체 여러개를 생성하여 배열로 만들어 인자로 넣고 `Promise.all`을 실행하면,
  * 배열의 모든 프로미스 객체들이 fulfilled 되었을 때, then의 함수가 실행된다.
  * then의 함수의 인자로 프로미스 객체들의 resolve 인자값을 배열로 돌려준다.

```javascript
// Promise.all([프로미스 객체들]);
​
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            console.log(ms);
            resolve(ms);
        }, ms);
    });
}
​
Promise.all([p(1000), p(2000), p(3000)]).then(messages=>{
    console.log('모두 fullfiled 됭 이후에 실행됩니다.', messages);
}); // 모두 fullfiled 됭 이후에 실행됩니다. (3) [1000, 2000, 3000]
```

* `Promise.race([프로미스 객체들])`

```javascript
// Promise.race([프로미스 객체들]);
​
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            console.log(ms);
            resolve(ms);
        }, ms);
    });
}
​
Promise.race([p(1000), p(2000), p(3000)]).then(messages=>{
    console.log('가장 빠른 하나가 fullfiled 된 이후에 실행됩니다.', messages);
}); // 가장 빠른 하나가 fullfiled 된 이후에 실행됩니다. 1000 (가장 fulfilled된 결과값 반영)
​
// 뒤에것도 실행되긴 한다.
```

{% hint style="info" %}
**Q1** 안녕하세요. '29. async function과 await -1'를 듣다가 질문 남깁니다. ‌

```javascript
// Promise 객체를 리턴하는 함수
function p(ms){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            resolve(ms);
        }, ms);
    });
}
// Promise 객체를 리턴하는 함수를 await로 호출하는 방법
const ms = await p(1000);
console.log(`${ms}ms 후에 실행된다.`);
```

‌ 위 코드를 node환경에서 실행시키려고 하면 오류가 나고, await를 사용하는 경우에는 항상 async 함수 안에서 사용되어야 한다고 가르쳐 주셨는데요. ‌ 강사님의 설명처럼 node환경에서 동작시킬때는 문법오류가 뜨는데, 크롬 브라우저 콘솔창에 위 구문을 치면 오류가 나지 않고 실행이 됩니다. 브라우저에서 쓸때는 문법이 다르게 적용되는건가요? 왜 두 환경에서 결과가 서로 다른지 알고싶습니다.

**A1** 크롬코드를 보면 콘솔을 구현한 함수가 async함수라서 콘솔창에서는 가능한것같습니다. ‌ 129번줄에 보시면 async evaluateCommandInConsole라는 함수를 볼수있습니다 이때문에 가능합니다.   
  
[https://chromium.googlesource.com/chromium/src.git/+/e8111c396fef38da6654093433b4be93bed01dce/third\_party/WebKit/Source/devtools/front\_end/console\_model/ConsoleModel.js](https://chromium.googlesource.com/chromium/src.git/+/e8111c396fef38da6654093433b4be93bed01dce/third_party/WebKit/Source/devtools/front_end/console_model/ConsoleModel.js)
{% endhint %}



