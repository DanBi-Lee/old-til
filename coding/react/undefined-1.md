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

