# Sass

## SASS 튜토리얼

Syntactically Awsome StyleSheets \(문법적으로 멋진 스타일시트\)

* 장점
  * 스타일코드 재사용성
  * 가독성 높여줌
* 확장자
  * `.sass`
    * 중괄호가 아닌 들여쓰기로 표현, 세미콜론 사용하지 않음
  * ☆`.scss`
    * 기존 css와 비슷한 문법

{% embed url="https://sass-guidelin.es/ko/" caption="Sass 가이드라인" %}

{% embed url="https://velopert.com/1712" caption="벨로퍼트 강좌" %}

1. 시작하기

   > ```text
   > $ npx create-react-app styling-with-sass
   > $ cd styling-with-sass
   > ```

2. node-sass라이브러리 설치

   > `yarn add node-sass`

3. `Button.js` 와 `Button.scss`파일 생성

{% tabs %}
{% tab title="Button.js" %}
```javascript
import React from 'react';
import './Button.scss';

function Button({ children }) {
  return <button className="Button">{children}</button>;
}

export default Button;
```
{% endtab %}

{% tab title="Button.scss" %}
```css
$blue: #228be6; // 변수 선언

.Button {
  display: inline-flex;
  color: white;
  font-weight: bold;
  outline: none;
  border-radius: 4px;
  border: none;
  cursor: pointer;

  height: 2.25rem;
  padding-left: 1rem;
  padding-right: 1rem;
  font-size: 1rem;

  background: $blue;
  &:hover { // &는 자기 자신
    background: lighten($blue, 10%); // 색상 10% 밝게
  }

  &:active {
    background: darken($blue, 10%); // 색상 10% 어둡게
  }
}
```
{% endtab %}
{% endtabs %}

### **1. size props 받아오기**

`classNames`이라는 라이브러리 사용

1. `$ yarn add classnames`로 라이브러리 설치
2. `Button.js`에서 불러오기

   > ```javascript
   > import React from 'react';
   > import classNames from 'classnames';
   > import './Button.scss';
   >
   > function Button({ children, size }) {
   >   return <button className={classNames('Button', size)}>{children}</button>;
   > }
   >
   > Button.defaultProps = {
   >   size: 'medium'
   > };
   >
   > export default Button;
   > ```

위와 같은 식으로하 props로 받은 값들을 `className`으로 사용할 수 있다.

### **2. color props 받아오기 \(@mixin 활용\)**

{% embed url="https://yeun.github.io/open-color/" caption="색 참고 사이트" %}

반복되는 scss 코드는 `@mixin`을 활용

```css
$blue: #228be6;
$gray: #495057;
$pink: #f06595;

// mixin 선언
@mixin button-color($color) {
  background: $color;
  &:hover {
    background: lighten($color, 10%);
  }
  &:active {
    background: darken($color, 10%);
  }
}

// mixin 사용
.Button {
  // 색상 관리
  &.blue {
    @include button-color($blue);
  }

  &.gray {
    @include button-color($gray);
  }

  &.pink {
    @include button-color($pink);
  }
}
```

### **3. outline, fullWidth \(불리언 형태의 값 받기\)**

```javascript
import React from 'react';
import classNames from 'classnames';
import './Button.scss';

function Button({ children, size, color, outline, fullWidth }) {
  return (
    <button
      className={classNames('Button', size, color, { outline, fullWidth })}
    >
      {children}
    </button>
  );
}

Button.defaultProps = {
  size: 'medium',
  color: 'blue'
};

export default Button;
```

위처럼 하면 outline과 fullWidth가 true일 때만 클래스명이 생긴다.

### **4. 버튼에 ...rest props 전달하기**

* 예시 상황
  * onClick이나 onMove 설정한다 생각하기

{% tabs %}
{% tab title="App.js" %}
```javascript
import React from 'react';
import './App.scss';
import Button from './components/Button';

function App() {
  return (
    <div className="App">
      <div className="buttons">
        <Button size="large" onClick={() => console.log('클릭됐다!')}>
          BUTTON
        </Button>
        <Button>BUTTON</Button>
        <Button size="small">BUTTON</Button>
      </div>
      <div className="buttons">
        <Button size="large" color="gray">
          BUTTON
        </Button>
        <Button color="gray">BUTTON</Button>
        <Button size="small" color="gray">
          BUTTON
        </Button>
      </div>
      <div className="buttons">
        <Button size="large" color="pink">
          BUTTON
        </Button>
        <Button color="pink">BUTTON</Button>
        <Button size="small" color="pink">
          BUTTON
        </Button>
      </div>
      <div className="buttons">
        <Button size="large" color="blue" outline>
          BUTTON
        </Button>
        <Button color="gray" outline>
          BUTTON
        </Button>
        <Button size="small" color="pink" outline>
          BUTTON
        </Button>
      </div>
      <div className="buttons">
        <Button size="large" fullWidth>
          BUTTON
        </Button>
        <Button size="large" color="gray" fullWidth>
          BUTTON
        </Button>
        <Button size="large" color="pink" fullWidth>
          BUTTON
        </Button>
      </div>
    </div>
  );
}

export default App;
```
{% endtab %}

{% tab title="Button.js" %}
```javascript
import React from 'react';
import classNames from 'classnames';
import './Button.scss';

function Button({ children, size, color, outline, fullWidth, ...rest }) {
  return (
    <button
      className={classNames('Button', size, color, { outline, fullWidth })}
      {...rest}
    >
      {children}
    </button>
  );
}

Button.defaultProps = {
  size: 'medium',
  color: 'blue'
};

export default Button;
```
{% endtab %}
{% endtabs %}

#### **className이 겹치지 않게 작성하는 팁**

1. 컴포넌트 이름을 고유하게 지정
2. 최상위 엘리먼트의 클래스이름을 컴포넌트 이름과 똑같게
3. 그 내부에서 셀렉터 사용

```css
.UserProfile{
    .user{
        img{
        }
    }
    .username {
    }
    .about{
    }
}
```



