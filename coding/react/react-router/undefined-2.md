# 서브 라우트

## 서브라우트 만들기

* 서브라우트

  * 라우트 안에 있는 라우트
  * 라우트를 사용한 컴포넌트 내부에서 라우트를 한번 더 쓰면 된다.

  > 사용 예시: 페이지 안에 탭이 있는 경우. 서브라우트를 사용하면 편하다.

{% tabs %}
{% tab title="Plain App.js" %}
```javascript
import React from "react";
import { Route, Link } from "react-router-dom"; // 특정 주소에 특정 컴포넌트를 보여주는 역할
import About from "./About";
import Home from "./Home";
import Profile from "./Profile";
import Profiles from "./Profiles";
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
        <li>
          <Link to="/profiles">사용자 목록</Link>
        </li>
      </ul>
      <hr />
      <Route path="/" component={Home} exact />
      <Route path="/about" component={About} />
      <Route path="/profiles" component={Profiles} />
    </div>
  );
}
​
export default App;
​
```
{% endtab %}

{% tab title="Profiles.js" %}
```javascript
import React from "react";
import Profile from "./Profile";
import { Link, Route } from "react-router-dom";
​
function Profiles() {
  return (
    <div>
      <h3>사용자 목록</h3>
      <ul>
        <li>
          <Link to="/profiles/velopert">velopert</Link>
        </li>
        <li>
          <Link to="/profiles/homer">homer</Link>
        </li>
      </ul>
​
      <Route
        path="/profiles"
        exact
        render={() => <div>사용자를 선택해주세요.</div>}
      />
      <Route path="/profiles/:username" component={Profile} />
    </div>
  );
}
​
export default Profiles;
```
{% endtab %}

{% tab title="Profile.js" %}
```javascript
import React from "react";
​
const profileData = {
  velopert: {
    name: "김민준",
    description: "Frontend Engineer @ RIDI",
  },
  homer: {
    name: "호머 심슨",
    description: "심슨 가족에 나오는 아빠 역할 캐릭터",
  },
};
function Profile({ match }) {
  console.log(match);
  const { username } = match.params;
  const profile = profileData[username];
​
  if (!profile) {
    return <div>존재하지 않는 사용자입니다.</div>;
  }
  return (
    <div>
      <h3>
        {username}({profile.name})
      </h3>
      <p>{profile.description}</p>
    </div>
  );
}
​
export default Profile;
```
{% endtab %}
{% endtabs %}

{% embed url="https://codesandbox.io/s/router-tutorial-seobeu-rauteu-vp9r0?file=/src/Profiles.js" %}



