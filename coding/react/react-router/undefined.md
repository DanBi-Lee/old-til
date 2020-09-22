# 라우터의 기본적인 사용법

## 프로젝트 준비 및 기본적인 사용법

목표 : 리액트 라우터를 사용하기 위해 프로젝트를 준비하고 리액트의 기본적인 사용법 배우기

1. npx create-react-app touter-tutorial
2. cd router-tutorial
3. yarn add react-router-dom

```javascript
import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import * as serviceWorker from "./serviceWorker";
import { BrowserRouter } from "react-router-dom"; // 1. 브라우저 라우터 불러오기
​
ReactDOM.render(
  <BrowserRouter> {/* 2. 브라우저 라우터로 감싸주기 */}
    <App />
  </BrowserRouter>,
  document.getElementById("root")
);
​
// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

### Route 사용법

```javascript
import React from "react";
import { Route } from "react-router-dom"; // 특정 주소에 특정 컴포넌트를 보여주는 역할
import About from "./About";
import Home from "./Home";
​
function App() {
  return (
    <div>
      <Route path="/" component={Home} exact />
      <Route path="/about" component={About} />
    </div>
  );
}
​
export default App;
```

### Link 사용법

* 경로이동시 a태그를 사용하면 안 된다.
  * a태그를 사용하면 아예 페이지가 새로 로딩되기 때문에.

```javascript
import React from "react";
import { Route, Link } from "react-router-dom"; // 특정 주소에 특정 컴포넌트를 보여주는 역할
import About from "./About";
import Home from "./Home";
​
function App() {
  return (
    <div>
      <ul>
        <li>
          <Link to="/">홈</Link>
        </li>
        <li>
          <Link to="/about">소개</Link>
        </li>
      </ul>
      <hr />
      <Route path="/" component={Home} exact />
      <Route path="/about" component={About} />
    </div>
  );
}
​
export default App;
​
```

### 다른 방식의 라우터 사용

* HashRouter
  * 주소 뒤에 `#`가 붙는다.
* MemoryRouter
  * 주소가 변하지 않는다.

