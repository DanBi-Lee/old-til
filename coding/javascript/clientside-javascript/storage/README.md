---
description: Storage객체
---

# 사용자 데이터 저장하기

{% embed url="https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=115186420" caption="" %}

## 사용자 데이터 저장하기 - Storage객체

자바스크립트 세계에서는 원칙적으로 스크립트로부터 컴퓨터에 마음대로 데이터를 쓰는 일은 허용하지 않았다. 왜냐하면 사용자가 컴퓨터 안의 파일을 다시 작성해버리면 일이기 때문이다.

하지만 그 예외가 되는 수단으로 부라우저에서는 초기부터 **쿠키**라는 메커니즘을 제공하고 있다. 웹 어플리케이션은 쿠키를 이용하여 클라이언트에 관한 소규모의 텍스트를 저장할 수 있다.

문제는 이 쿠키라는 것이 자바스크립트에서 조작하기 어렵고 크기도 제한되어있다는 것이다. 따라서 현재는 그 대안으로 **Web Storage**\(스토리지\)를 이용하는 것을 추천한다.

스토리지란, 브라우저에 내장된 데이터 스토어\(저장소\)다. 데이터를 특정하는 키와 값의 쌍으로 데이터를 저장하기 때문에 **Key-Value형 데이터 스토어**라고도 불린다.

```text
Key(키) : Value(값)
fuit1 : 사과
```

스토리지와 쿠키의 차이

| 항목 | 스토리지 | 쿠키 |
| :--- | :--- | :--- |
| 데이터 크기의 상한 | 크다\(5MB\) | 작다\(4KB\) |
| 데이터의 유효기간 | 없음 | 있음 |
| 데이터 통신 | 존재하지 않는다 | 요청마다 서버에도 송신 |

{% hint style="info" %}
> 데이터 크기의 상한은 어떤 기준은로 정해지는 걸까...?  
> 스토리지 전체? 아니면 key값 하나..?

쿠키는 쿠키 단위로 약 40KB, 로컬 스토리지는 도메인당 약 5MB

> ~~쿠키도 브라우저에 저장되는 걸로 알고 있는데 요청마다 서버에 송신하는 것은 무슨 의미인가...~~

**그렇지 않았다.**  
쿠키는 처음부터 서버와 클라이언트간의 지속적인 데이터 교환을 위해서 만들어졌다. \(참고: **제로초님 블로그**\)
{% endhint %}

{% page-ref page="cookie.md" %}

### 스토리지에 데이터 보관/취득하기

```javascript
let storage = localStorage;
storage.setItem('fruit1', '사과');
storage.fruit2 = '귤';
storage['fruit3'] = '포도';

console.log(storage.getItem('fruit1'));
console.log(storage.fruit2);
console.log(storage['fruit3']);
```

* 스토리지 종류
  * 로컬 스토리지\(localStorage\)
    * 오리진 단위로 데이터를 관리한다. 창/탭 전반에 걸쳐 데이터 공유가 가능하며 브라우저를 닫더라도 데이터는 유지된다.
  * 세션 스토리지\(sessionStorage\)
    * 현재 세션\(=브라우저가 열려있는 동안\)에서만 유지되는 데이터를 관리한다. 브라우저를 클로즈한 타이밍에 데이터는 삭제되고 창/탭 간에 데이터를 공유할 수 없다.

양자는 데이터 유효 기간/범위에서 차이가 있다. 용도에 따라 구분해야 하지만 일반적으로는 문제가 없다면 세션 스토리지를 우선적으로 사용할 것을 추천한다.

이유

* 명시적으로 데이터를 삭제하지 않는 한 데이터가 사라지지 않는다. \(=쓰레기가 쌓이기 쉽다.\)
* 동일한 오리진에서 여러 애플리케이션을 실행하는 경우 변수명이 충돌하기 쉽다.

> 오리진이란? 오리진\(origin\)은 '스키마://호스팅명:포트번호' 조합으로 나타내는 단위를 말한다. 스토리지에서는 오리진 단위로 데이터를 관리하기 때문에 현재의 호스트에서 저장된 데이터를 다른 호스트의 애플리케이션에서 읽을 수 없다.

* 개발자 도구로 스토리지 내용 확인 하는 방법
  * Application 탭의 Storage 항목 확인
  * 각 행에서 데이터를 삽입/수정/삭제할 수 있다.

### 기존 데이터 삭제하기

데이터 선택 삭제

```javascript
storage.removeItem('fruit1');
delete storage.fruit1;
delete storage['fruit1'];
```

모든 데이터 삭제

```javascript
storage.clear();
```

로컬 스토리지는 명시적으로 데이터를 삭제하지 않는 한 영원히 데이터를 계속 유지한다. 우선은 세션 스토리지를 이용해야 하지만 로컬 스토리지를 이용할 경우에는 어디에서 데이터를 삭제할지 미리 규칙화하고 있어야 한다.

### 스토리지로부터 모든 데이터 추출하기

```javascript
let storage = localStorage;
for(let i =0, len = storage.length; i < len; i++){
    let k = storage.key(i);
    let v = storage[k];
    console.log(`${k} : ${v}`);
}
```

### 스토리지에 객체 보관/취득하기

스토리지에 저장할 수 있는 형식은 문자열을 전제로 한다. \(객체를 저장해도 toString 메소드로 문자열화 된다.\) 그러므로 객체를 스토리지에 저장하는 경우, 복원 가능한 문자열로 변환해야 한다.

```javascript
let storage = localStorage;
let apple = {name: '사과', price: 150, mode : '아오모리'};
storage.setItem('apple', JSON.stringify(apple));
let data = JSON.parse(storage.getItem('apple'));
console.log(data.name);
```

{% hint style="info" %}
JSON.stringify 메소드가 가물가물하다...
{% endhint %}

**스토리지에서 이름 충돌 방지**

로컬 스토리지는 오리진 단위로 데이터를 관리한다. 특히 하나의 오리지니에서 복수의 애플리케이션이 실행되는 경우에는 이름 충돌의 위험을 방지하기 위해 하나의 애플리케이션에서 사용할 데이터는 최대한 **하나의 객체**에 넣어둘 것을 추천한다.

단, 값이 들어가고 나가는 것 때문에 객체의 변환을 의식하는 것은 귀찮으므로 다음과 같은 MyStorage 클래스를 준비하는 것이 편리하다.

```javascript
let MyStorage = function(app){
    // 애플리케이션 명
    this.app = app
    // 이용할 스토리지의 종류 (여기서는 로컬 스토리지)
    this.storage = localStorage;
    // 스토리지로부터 읽어들인 객체
    // 해당하는 객체가 없을 경우 빈 객체를 생성
    this.data = JSON.parse(this.storage[this.app] || '{}');
};

MyStorage.prototype = {
    // 지정된 키로 값을 취득
    getItem : function(key){
        return this.data[key]
    },
    // 지정된 키/값으로 객체를 고쳐쓰기
    setItem : function(key, value){
        this.data[key] = value;
    },
    // MyStorage 객체의 내용을 스토리지에 보관
    save : function(){
        this.storage[this.app] = JSON.stringify(this.data);
    }
};
```

MyStorage객체를 이용하려면 다음과 같이 하면 된다.

```javascript
let storage2 = new MyStorage('JSSample');
storage2.setItem('hoge', '호게');
console.log(storage2.getItem('hoge'));
storage2.save(); // save메소드까지 사용해야 storage에 반영
```

### 스토리지의 변경 감시하기

다른 창/탭에서 발생한 스토리지의 변화를 감지하여 현재 페이지에 반영시키고 싶은 상황이 생길 수 있다. 니러한 격우에는 storage 이벤트를 이용한다.

ex. 스토리지에 대한 변경을 감시하여 변경 내용을 로그로 출력하는 예.

```javascript
window.addEventListener('storage', (e)=>{
    console.log(`변경된 키 : ${e.key}`);
    console.log(`변경 전의 값 : ${e.oldValue}`);
    console.log(`변경 후의 값 : ${e.newValue}`);
    console.log(`발생원 페이지 : ${e.url}`)
}, false);
```

storage 이벤트 리스너에서는 이벤트 객체 e를 통해 다음과 같은 정보에 액세스 할 수 있다.

* key : 변경된 키
* oldValue : 변경전 값
* newValue : 변경후 값
* url : 변경 발생원의 페이지
* storageArea : 영향을 받은 스토리지\(localStorage/sessionStorage 객체\)

{% hint style="info" %}
localStorage는 오리진 단위로 데이터를 관리하지만, sessionStorage는 창/탭 간에 데이터를 공유할 수 없다고 한다. 그렇다면 stoageArea는 무슨 의미가 있는걸까..?
{% endhint %}

