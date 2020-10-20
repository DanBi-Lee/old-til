# Generic

## 제네릭

### 1. 제네릭은 타입을 파라미터화 하는 것이다.

```typescript
function createPromise<T>(x:T, timeout:number){
    return new Promise((resolve: (v:T)=> void, reject)=>{
        setTimeout(()=>{
            resolve(x);
        }, timeout);
    })
}
​
createPromise<string>("ok",100)
    .then(v => console.log(v));
​
// 위와 동일
​
function createPromise<T>(x:T, timeout:number){
    return new Promise<T>((resolve, reject)=>{
        setTimeout(()=>{
            resolve(x);
        }, timeout);
    })
}
​
createPromise<string>("ok",100)
    .then(v => console.log(v));
```

여러개의 타입의 파라미터화

```typescript
function createTuple2<T, U>(v: T, v2: U): [T, U]{
    return [v, v2];
}
const t1 = createTuple2("user1", 1000);
```

타입 파라미터도 원하는 단어를 사용할 수 있지만 대문자로 하는 것이 관례

### 2. 제네릭은 클래스를 정리할 때도 사용 가능하다.

```typescript
class LocalDB<T> {
    constructor(private localStorageKey: string) {}
    add(v : T){
        localStorage.setItem(this.localStorageKey, JSON.stringify(v));
    }
    get(): T{
        const v = localStorage.getItem(this.localStorageKey);
        return (v) ? JSON.parse(v) : null;
    }
}
​
interface User {name:string}
​
const userDB = new LocalDB<User>('user');
userDB.add({name: 'jay'});
const userA = userDB.get();
userA.name;
```

### 3. 인터페이스를 만들때도 제네릭 사용 가능

```typescript
interface DB<T>{
    add(v:T) : void;
    get():T;
}
​
class D<T> implements DB<T> {
    add(v:T): void {
        throw new Error("Method not implemented.");
    }
    get():T {
        throw new Error("Method not implemented.");
    }
}
​
// 제네릭 확장
​
interface JSONerialier {
    serialize() : string
}
​
class LocalDB<T extends JSONerialier> implements DB<T> {
    constructor(private localStorageKey: string) {}
    add(v : T){
        localStorage.setItem(this.localStorageKey, v.serialize());
    }
    get(): T{
        const v = localStorage.getItem(this.localStorageKey);
        return (v) ? JSON.parse(v) : null;
    }
}
```

### 4. 조건부 타입

```typescript
interface Vegitable {
    v: string;
}
interface Meat {
    m : string;
}
interface Cart2<T> {
    getItem() : T extends Vegitable? Vegitable : Meat
}
​
const cart1 : Cart2<Vegitable> = {
    getItem() {
        return {
            v : ''
        }
    }
}
​
cart1.getItem().v
```

