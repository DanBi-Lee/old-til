# 파라미터와 쿼리

## 파라미터와 쿼리

* URL Parameter
  * `/profiles/velopert`
  * 특정 데이터 조회할때 사용
* Query
  * `/filter?type=book&sort_by=date`
  * 옵션을 줘서 검색할 때 사용 ex. type, sort\_by

### URL 파라미터 사용하기

App.js

{% tabs %}
{% tab title="App.js" %}
```javascript
import React from "react";
import { Route, Link } from "react-router-dom";
// 특정 주소에 특정 컴포넌트를 보여주는 역할
import About from "./About";
import Home from "./Home";
import Profile from "./Profile";
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
      <Route path="/profiles/:username" component={Profile} />
    </div>
  );
}
​
export default App;
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

### Query 사용하기

`yarn add qs`

{% code title="About.js" %}
```javascript
import React from "react";
import qs from "qs";
​
function About({ location }) {
  const query = qs.parse(location.search, {
    ignoreQueryPrefix: true,
  });
​
  const detail = query.detail === "true";
​
  return (
    <div>
      <h1>소개</h1>
      <p>이 프로젝트는 리액트 라우터 기초를 실습해보는 예제 프로젝트 입니다.</p>
      {detail && <p>detail값이 true 입니다!</p>}
    </div>
  );
}
​
export default About;
```
{% endcode %}

{% embed url="https://codesandbox.io/s/router-tutorial-parameter-query-xf4p8?file=/src/Profile.js" %}



