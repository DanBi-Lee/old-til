# class

## 클래스 CLASS

### 객체를 만들 수 있는 새로운 방법 \(ES6 class\)

prototype을 좀 더 명료하게 사용할 수 있도록 돕는다.

* 선언적 방식

```javascript
class A {}
​
console.log(new A());
```

* class 표현식을 변수에 할당

```javascript
const B = class {};
​
console.log(new B());
```

* 선언적 방식이지만 호이스팅은 일어나지 않는다.

```javascript
new C();
​
class C{}
```

#### constructor \(생성자\)

```javascript
// constructor
​
class A{}
​
console.log(new A());
​
class B{
    constructor(){ //이 부분은 B호출시 자동으로 실행
        console.log('constructor');
    }
}
​
console.log(new B());
​
class C{
    constructor(name, age){
        console.log('constructor', name, age);
    }
}
​
console.log(new C('Mark', 37)); // constructor Mark 37
console.log(new C()); // constructor undefined undefined
```

#### 멤버 변수 \(객체의 프로퍼티\)

```javascript
// 멤버 변수
​
class A {
    constructor(name, age){
        this.name = name;
        this.age = age;
    }
}
​
console.log(new A('Mark', 37));
​
// class field는 런타임 확인
​
class B{
    name;
    age;
}
​
console.log(new B());
​
class C{
    name = 'no name';
    age = 0;
​
    constructor(name, age){
        this.name = name;
        this.age = age;
    }
}
​
console.log(new C('Mark', 37));
​
// 멤버 함수
​
class A{
    hello1(){
        console.log('hello1', this);
    }
    
    hello2 = () => {
        console.log('hello2', this);
    }
}
​
new A().hello1(); // A클래스로 만든 객체
new A().hello2(); // A클래스로 만든 객체
​
class B{
    name = 'Mark';
​
    hello(){
        console.log('hello', this.name);
    }
}
​
new B().hello();
```

#### get, set \(게터, 세터\)

```javascript
// get, set
class A{
    _name = 'no name'; // 내부적으로 쓸 경우에 '_'앞에 언더바를 붙인다.
    
    get name(){
        return this._name + '@@@';
    }
    
    set name(value){
        this._name = value + '!!!';
    }
}
​
const a = new A();
console.log(a);
a.name = 'Mark'; // set함수 호출
console.log(a);
console.log(a.name); // get함수 호출
console.log(a._name); // 속성값 그대로 호출
​
// readonly (set함수를 선언하지 않음)
class B {
    _name = 'no name';
    
    get name(){
        return this._name + '@@@';
    }
}
​
const b = new B();
```

#### static 변수, 함수 \(객체가 아니고, 클래스의 변수와 함수\)

직접적으로 class를 통해 변수와 함수를 사용하는 방식

```javascript
// static 변수, 함수
class A {
    static age = 37;
    static hello(){
        console.log(A.age);
    }
}
​
console.log(A, A.age);
A.hello();
​
class B {
    age = 37;
    static hello(){
        console.log(this.age);
    }
}
​
console.log(B, B.age); // B.age는 undefined
console.log(B.hello()); // undefined undefined
// static으로 만든 것은 객체에 속해있지 않다.
​
class C {
    static name = '이 클래스의 이름은 C가 아니다.';
}
​
console.log(C); // 함수 이름이 static name으로 나타난다
```

#### extends \(클래스의 상속 기본\)

```javascript
// 상속 기본
class Parent {
    name = 'Lee';
​
    hello(){
        console.log('hello', this.name);
    }
}
​
class Child extends Parent { // 멤버 변수화 멤버 함수가 함께 가져가진다.
    
}
​
const p = new Parent();
const c = new Child();
console.log(p,c);
```

#### override \(클래스의 상속 멤버 변수 및 함수 오버라이딩, 추가\)

부모에서 구현중인 함수나 변수가 자식에게서 똑같이 같은 이름으로 구현을 시키면 그것을 오버라이드라고 한다.

자식이 만들어놓은 함수가 부모의 함수를 덮어씌운다. 부모에게 없는 경우엔 자식이 추가한다.

```javascript
class Parent {
    name = "Lee";
    
    hello(){
        console.log('hello', this.name);
    }
}
​
class Child extends Parent {
    age = 37;
    
    hello(){
        console.log('hello', this.name, this.age);
    }
}
​
const p = new Parent();
const c = new Child();
​
console.log(p,c);
```

#### super \(클래스의 상속 생성자 함수 변경\)

```javascript
// super
​
class Parent {
    name;
    
    constructor(name){
        this.name = name;
    }
​
    hello(){
        console.log('hello', this.name);
    }
}
​
class Child extends Parent {
    age;
    
    constructor(name, age){
        super(name); // 부모의 constructor호출
        this.age=age;
    }
    
    hello(){
        console.log('hello', this.name, this.age);
    }
}
​
const p = new Parent('Mark');
const c = new Child('Mark', 37);
```

#### static \(클래스의 static 상속\)

```javascript
// static 상속
​
class Parent{
    static age = 37;
}
​
class Child extends Parent{}
​
console.log(Parent.age, Child.age); // static도 상속 된다.
```

