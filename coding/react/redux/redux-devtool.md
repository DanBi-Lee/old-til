# redux-devtool

### 리덕스 개발자 도구 적용

* 리덕스 개발자 도구
  * 현재 스토어의 상태 개발자 도구에서 조회 가능
  * 지금까지 어떤 액션이 dispatch되었는지
  * 액션에 따라 상태가 어떻게 변했는지
  * 액션의 상태 되돌리기
  * 액션을 개발자도구에서 바로 디스패치

1. [Redux Devtools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=ko) 크롬 확장앱 설치
2. 패키지 설치 `yarn add redux-devtools-extention`
3. index 파일

   > ```javascript
   > import { composeWithDevTools } from "redux-devtools-extension";
   > ​
   > const store = createStore(rootReducer, composeWithDevTools());
   > ```

