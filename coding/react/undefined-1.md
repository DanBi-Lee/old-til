# 클래스형 컴포넌트

{% hint style="info" %}
과거에는 함수형 컴포넌트에서 state를 변경할 수 없는 등의 문제로 클래스형 컴포넌트를 사용했으나, hook을 사용하게 되면서, 함수형 컴포넌트를 사용하게 되었다.

클래스형 컴포넌트는 유지보수를 하거나, 몇몇의 특수 케이스에서 사용되니 간단히 사용 방법을 익혀두자.
{% endhint %}

{% tabs %}
{% tab title="함수형 컴포넌트" %}
{% code title="Hello.js" %}
```javascript
import React from 'react';

function Hello({ color, name, isSpecial }) {
  return (
    <div style={{ color }}>
      {isSpecial && <b>*</b>}
      안녕하세요 {name}
    </div>
  );
}

Hello.defaultProps = {
  name: '이름없음'
};

export default Hello;
```
{% endcode %}
{% endtab %}

{% tab title="클래스형 컴포넌트" %}
{% code title="Hello.js" %}
```javascript
import React, { Component } from 'react';

class Hello extends Component {
  // defaultProps를 선언하는 또다른 방법
	/* 
	static defaultProps = {
    name : '이름없음'
  }
  */

  render() {
    const { color, name, isSpecial } = this.props;
    return (
      <div style={{ color }}>
        {isSpecial && <b>*</b>}
        안녕하세요 {name}
      </div>
    );
  }
}

Hello.defaultProps = {
  name: '이름없음'
};

export default Hello;
```
{% endcode %}
{% endtab %}
{% endtabs %}

**차이점**

1. `import {Component} form 'react'`로 컴포넌트를 따로 임포트한다.
2. 클래스형 컴포넌트에서는 `render` 메서드에서 JSX를 반환
3. `props` 조회는 `this.props`로
4. `defaultProps`는 기존과 같이 할 수 있음
   * 혹은 `static`키워드를 사용하여 내부에서 선언할 수도 있음

### 클래스형 컴포넌트 커스텀 메서드만들기

```text
import React, { Component } from 'react';
​
class Counter extends Component {
  handleIncrease() {
    console.log('increase');
    console.log(this);
  }
​
  handleDecrease() {
    console.log('decrease');
  }
​
  render() {
    return (
      <div>
        <h1>0</h1>
        <button onClick={this.handleIncrease}>+1</button>
        <button onClick={this.handleDecrease}>-1</button>
      </div>
    );
  }
}
​
export default Counter;
```

커스텀 메서드로 표현한 함수를 render안에서 부르려고 하면 this가 조회되지 않는다.

this를 조회하는 방법

1. 생성자 메서드 constructor에서 bind작업
2. onClick 속성에서 메서드를 불러올 때 bind작업
   * 비권장한다
     * 렌더링 할 때마다 함수가 새로 만들어지기 때문에 컴포넌트 최적화 할 때 까다롭다.
3. 클래스 컴포넌트에서 화살표 함수를 사용 \([class-properties](https://babeljs.io/docs/en/babel-plugin-proposal-class-properties) 라는 문법\)

### 상태 선언

클래스형 컴포넌트에서 상태 관리는 constructor 내부세어 this.state를 설정해주면 된다.   
\(이 때 무조건 객체로\)

```javascript
import React, { Component } from 'react';
​
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0
    };
  }
  
  /* 화살표 함수 문법을 사용하여 메서드를 작성 할 수 있게 해줬던 class-properties 문법이 적용되어 있다면 굳이 constructor 를 작성하지 않고 state를 작성할 수 있다. */
  /*
  state = {
    counter : 0
  };
  */
  
  
  handleIncrease = () => {
    console.log('increase');
    console.log(this);
  };
​
  handleDecrease = () => {
    console.log('decrease');
  };
​
  render() {
    return (
      <div>
        <h1>{this.state.counter}</h1>
        <button onClick={this.handleIncrease}>+1</button>
        <button onClick={this.handleDecrease}>-1</button>
      </div>
    );
  }
}
​
export default Counter;
```

### 상태 업데이트

상태 업데이트는 `this.setState`함수를 사용한다.

함수형 업데이트도 가능하고,

상태가 업데이트 되고 나서 작업을 하고 싶다면 setState의 두 번째 파라미터에 콜백함수를 넣어줄 수 있다.

