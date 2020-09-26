# 리덕스 모듈

## 리덕스 모듈 만들기

* 리덕스 묘듈이란, 다음 항목이 포함된 JS파일
  * 액션 타입
  * 액션 생성 함수
  * 리듀서

    > 각 다른 파일에 저장할 수도 있지만, 한 파일에 몰아서 작성하는 걸 추천함
    >
    > * Ducks 패턴
    >   * 파일에 액션타입, 액션 선언함수, 리듀서 선언
    >   * 주의 : reducer는 export default로 내보내기, 액션 생성함수는 export로 내보내기
    >   * 불러올 때 `import * as 이름 from '경로';`로 불러올 수 있고, 각각 하나씩도 불러올 수 있다.

### 실습

1. 리덕스 모듈 제작 1 `counter.js`
2. 리덕스 모듈 제작2 `todos.js`
3. rootReducer제작
4. 리액트 프로젝트에 리덕스 적용하기 `yarn add react-redux`
5. index.js에 Provider불러오기 `import { Provider } from "react-redux";`
6. `import { creasteStore } from "redux";`
7. `import rootReducer from "./modules";`
8. `const store = createStore(rootReducer);`
9. App컴포넌트 Provider로 감싸고 props로 store를 넘겨줌

#### 카운터 구현하기

1. Counter라는 프레젠테이션 컴포넌트 제작

   > 프레젠테이션 컴포넌트란?

2. CounterContainer라는 컨테이너 컴포넌트 제작

   > `import { useSelector, useDispatch } from "react-redux";`
   >
   > `import { increase, decrease, setDiff } from "../modules/counter";`

3. Counter컴포넌트에 props 넘겨주기

