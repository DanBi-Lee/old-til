# 리덕스 기본

## 리덕스 사용 할 준비

1. `npx create-react-app 파일이름`
2. `yarn add redux`
3. 스토어 불러오기
   1. `import { createStore } from 'redux';`
4. 리덕스에서 관리할 상태 정의 \(상태의 초기값 설정\)
5. 액션 타입 정의
6. 액션 생성함수 정의
7. 리듀서 만들기
8. 스토어 만들기
9. 스토어안에 들어있는 상태가 바꾸리때마다 호출되는 listener함수
10. 구독 해제하고 싶을때는 `unsubscribe()`를 호출
11. 액션 디스패치

    > ex. `store.dispatch(increase())`

