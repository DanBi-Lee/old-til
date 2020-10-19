# Class

## Class

등장시기 : ES6

```javascript
class Cart {
    constructor(user) {
        this.user = user;
        this.store = {};
    }
    put(id, product) {
        this.store[id] = product;
    }
    get(id) {
        return this.store[id];
    }
}
​
const cartJohn = new Cart({name:'john'});
const cartJay = new Cart({name:'jay'});
```

타입스크립트

```typescript
interface User {
    name :string;
}
​
interface Product {
    id:string;
    price:number;
}
​
class Cart {
    user : User;
    store : object;
    constructor(user:User) {
        this.user = user;
        this.store = {};
    }
    put(id:string, product: Product) {
        this.store[id] = product;
    }
    get(id:string) {
        return this.store[id];
    }
}
​
const cartJohn = new Cart({name:'john'});
const cartJay = new Cart({name:'jay'});
```

타입스크립트는 속성과 메서드에 접근제한자를 가질 수 있다. \(ES6에는 없음, 타입스크립트에서 추가된 기능\)

store를 접근제한 하고 싶다면. \(private, public, protected\)

접근 제한자를 주지 않으면 public

private 를 사용할 경우엔 클래스 내부에서만 접근할 수 있게 된다. 인스턴스에서는 접근할 수 없다.

```typescript
interface User {
    name :string;
}
​
interface Product {
    id:string;
    price:number;
}
​
class Cart {
    user : User;
    private store : object;
    constructor(user:User) {
        this.user = user;
        this.store = {};
    }
    put(id:string, product: Product) {
        this.get(id); // 메서드에 접근제한을 걸 경우, 다른 메서드를 통해서는 접근할 수 있다.
        this.store[id] = product;
    }
    private get(id:string) {
        return this.store[id];
    }
}
​
const cartJohn = new Cart({name:'john'});
console.log(cartJohn.store); // 접근 불가
const cartJay = new Cart({name:'jay'});
```

* protected와 private차이점
  * Cart라는 클래스를 상속할 경우
    * private : 접근 불가
    * protected : 접근 가능

파라미터에 접근제한자 사용하면 속성이 정의 + 할당되면서, 선언 단축 가능

```typescript
class Cart {
    // protected user : User;
    // private store : object;
​
    constructor(public user:User, private store : object ={}) {
    }
​
​
    put(id:string, product: Product) {
        this.get(id); // 메서드에 접근제한을 걸 경우, 다른 메서드를 통해서는 접근할 수 있다.
        this.store[id] = product;
    }
    get(id:string) {
        return this.store[id];
    }
}
```

상속, 인터페이스와의 관계

인터페이스를 이용하여 클래스 만들기

```typescript
interface Person {
    name : string;
    say(message: string) : void;
}
​
interface Programmer {
    writeCode(requirment:string):string;
}
​
class KoreanProgrammer implements Person, Programmer {
    constructor (public name:string){
    }
    writeCode(requirment: string): string {
        console.log(requirment);
        return requirment + '....';
    }
    say(message: string): void {
        console.log(message);
    }
}
```

abstract 클래스 \(추상 객체\)

미완성 클래스지만, 상속은 할 수 있다.

```typescript
abstract class Korean implements Person {
    public abstract jumin: number;
    
    constructor (public name: string){
​
    }
    say(message: string): void {
        throw new Error("Method not implemented.");
    }
​
    abstract lobeKimchi():void;
}
​
class KoreanProgrammer extends Korean implements Programmer {
    constructor (public name:string, public jumin:number){
        super(name);
    }
    writeCode(requirment: string): string {
        console.log(requirment);
        return requirment + '....';
    }
    say(message: string): void {
        console.log(message);
    }
    lobeKimchi():void{
​
    }
}
​
const jay = new KoreanProgrammer('jay', 1234);
```



interface는 자바스크립트로 컴파일되지 않는다.   
interface를 컴파일 하고 싶을 때, 대신 class를 사용한다.

```typescript
class Human {
    public name:string;
    public age: number;
    public gender:string;
    constructor(name:string, age:number, gender:string){
        this.name= name;
        this.age = age;
        this.gender = gender;
    }
}
​
const plyrn = new Human("Syn", 18, "female");
​
const sayHi = (person:Human):string => {
    return `Hello, ${person.name}. you are ${person.age}, you are a ${person.gender}!!!`;
};
​
console.log(sayHi(plyrn));
​
export {};
```





