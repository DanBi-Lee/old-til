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

{% hint style="info" %}
**Q1** 안녕하세요. 클래스 강의를 듣고 몇가지 궁금점이 생겨서 질문 드립니다. ‌ ‌ ‌ 1. 멤버 함수 ‌ 멤버 함수를 공부 할 때, ‌

```javascript
class A{
    hello1(){
        console.log('hello1', this);
    }
    
    hello2 = () => {
        console.log('hello2', this);
    }
}

new A().hello1();
new A().hello2();
```

‌ 위처럼 arrow함수에서 작성한 this도 A클래스로 만듣 객체를 가르키는 결과가 나옵니다. ‌ 이전 생성자 함수 강의에서는 arrow함수 안에 this가 생기지 않아서 생성자 함수로 사용이 불가하다고 배운것으로 기억하는데, class안의 멤버함수로 arrow함수를 사용할 경우 this와 어떻게 차이가 생기는지 알 수 있을까요? ‌

‌ 2. 멤버 변수 ‌ 멤버 변수를 미리 작성할 수 있다는 것은 알았는데, 멤버 변수를 선언해놓고 constructor 함수를 다시 선언하면 기존 멤버에 의미가 있나요? ‌ 예를 들어서, ‌

```javascript
class A {
	name = 'Mark';
	
	constructor(name){
		this.name = name;
	}
}
```

‌ 위와 같이 class를 선언했을 때, ‌

```javascript
const a = new A('Anna');
const b = new A();
```

‌ `a.name` 은 'Anna', ‌ `b.name` 은 undefined로 멤버 변수 name으로 할당했던 'Mark'가 쓰이는 일은 없지 않나요? 24. 클래스 D 강의의 7분쯤에 constructor로 age와 name을 받는데 따로 age와 name을 멤버 함수로 선언해두는 것인지 궁금합니다.

**A1** 우선 2번은 제생각에는 강의하시는분이 타입스스크립트를 많이쓰셔서 습관이 아닐까합니다. 굳이 선언할 필요가없어보입니다 좀 더 생각해보고 추가 내용이있다면 대댓글로 추가해드리겠습니다. ‌ 

1번은 arrow함수의 특성때문입니다. 간단하게 arrow함수는 함수가 정의된 곳의 환경이 this가 되고 일반함수는 호출 방식에 따라서 this를 동적으로 정의합니다. 우선은 이정도만 기억하고 있으시면 무방할거같습니다. ‌ 

arrow함수는 prototype을 가지지 않아서 new키워드를 통해 생성하려고 한다면 constructor가 아니라서 생성할수 없다고 에러가 나올것입니다. this가 내부에 존재하지 않아서 사용못한다는건 객체에서 매서드를 arrow 함수로 정의하면 내부에서 this의 값은 window가 나오는것이랑 관련되어 보입니다. 위에서 말했듯이 arrow함수는 정의될때의 환경이 this로 정의됩니다. 이러한 환경을 정의할수있는것은 함수 또는 class\(따지자면 class도 함수이기 때문이다\) 이기 때문에 class 내부에서 정의한 arrow함수의 this는 class가 될수 있지만 객체내부에서 정의한 arrow함수의 this는 해당 객체의 환경 일반적으로 window가 됩니다. 이러한 이유 때문에 클래스에서 정의한 arrow함수의 this는 위와같은 결과를 보여줍니다. ‌ 

사실 이와같은 현상들을 완전히 이해하려면 prototype과 execution context를 완전히 이해해야 하는데 이것을 이해하기위해 this, lexical scope, scope chain등 너무 많은것을 공부해야해서 지금 모든것을 이해하고 해당 코스에서 요구하는 수준을 한참 뛰어넘는다고 생각합니다. 일반 함수와 arrow함수의 차이를 간단히 설명하고 추가적으로 좀 더 자세한 내용을 설명 드렸으나 현재 이해가 안될수도있고 전부 이해를 할필요는 없다고 생각됩니다. 해당코스를 한참벗어나는 수준이기 때문에 해당 코스를 마무리하시고 자바스크립트의 코어에 대해서 공부할 기회가 생길때 자세히 공부하시면 좋을거 같습니다.
{% endhint %}



