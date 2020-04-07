# 컴포넌트 만들기

{% code title="Hello.js" %}
```jsx
import React from 'react'; // 1. 리액트를 불러오겠다.

function Hello({color, name}){ // 2. 컴포넌트는 대문자로 시작한다.
return <div style={{color}}>안녕하세요, {name}</div>; //jsx
}

Hello.defaultProps = {
    name : '이름없음'
}

export default Hello; // 3. 헬로라는 컴포넌트를 내보낸다.
```
{% endcode %}

{% code title="App.js" %}
```jsx
import React from 'react';
import Hello from './Hello'; // 1. 불러온다.

function App() {
  return (
    <div>
      <Hello /> {/* 2. 이런식으로 붙인다*/}
    </div>
  );
}

export default App; // 3. 내보낸다.
```
{% endcode %}

{% code title="index.js" %}
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render( // 브라우저에 있는 실제 DOM 내부에 리액트 컴포넌트를 렌더링하겠다는 의
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root') // 아이디가 root인 DOM을 선택한다.
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```
{% endcode %}

{% code title="public/index.html" %}
```markup
<div id="root"></div>
```
{% endcode %}



