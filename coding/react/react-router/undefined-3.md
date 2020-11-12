# 리액트 라우터의 부가기능

## 리액트 라우터의 부가기능

### history 객체

* `<Route>`로 사용되는 객체에게 props로 전달된다.
* history객체를 사용해서 컴포넌트에서 라우터에 직접적인 접근을 할 수 있다.
  * 특정 함수를 이용했을 때, 특정 경로로 가거나 뒤로갈 수 있다. \(페이지 이탈 방지\)
* history객체 소개

  > ```text
  > length: 5
  > action: "POP"
  > location: Object
  > createHref: ƒ createHref() {}
  > push: ƒ push() {}
  > replace: ƒ replace() {}
  > go: ƒ go() {}
  > goBack: ƒ goBack() {}
  > goForward: ƒ goForward() {}
  > block: ƒ block() {}
  > listen: ƒ listen() {}
  > ```

  * action : 라우터에서 가장 마지막에 발생한 액션이 무엇인지
    * `"PUSH"` : 링크를 통한 이동
    * `"POP"` : 브라우저의 뒤로가기나 앞으로가기를 눌렀을 때
  * block : 사용자가 페이지에서 이탈할 때 방지
  * ~~createHref : 주소 만들 때 쓰임 \(거의 안 쓰임\)~~
  * go : 앞으로가기 혹은 뒤로가기
    * `go(1)` : 앞으로 1번
    * `go(-2)` : 뒤로 2번
  * goBack : 뒤로가기
  * goForward : 앞으로 가기
  * length : 방문 길이
  * listen : 경로이동 시 특정 함수를 호출하고 싶을 때
  * location : 현재 경로에 대한 정보
  * push : 특정 경로로 보내는 것 \(방문 기록 남김\)
  * replace : 특정 주소로 이동 \(방문 기록을 남기지 않음\)

### withRouter

* 라우터 컴포넌트가 아닌 곳에서 match, location, history 사용
* location, match의 차이점
  * location : 어디서 불러오든 같은 정보
  * match : 현재 자신이 렌더링된 위치를 기준으로 값을 받아옴
* Route가 설정되지 않은 컴포넌트에서 조건부로 이동해야할 때 사용
  * 로그인 성공시 특정 경로 가는 경우 등

{% embed url="https://codesandbox.io/s/router-tutorial-riaegteu-rauteoyi-bugagineung-c7phf?file=/src/Profile.js" %}



