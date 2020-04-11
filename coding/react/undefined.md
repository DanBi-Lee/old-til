# 11. React.memo

성능 최적화

### React.memo

컴포넌트에서 리렌더링이 불필요할 떄는 이전에 리렌더링 한 내용 재사용 컴포넌트의 리렌더링 성능을 최적화 해줄 수 있다.

```javascript
export default React.memo(CreateUser);
// 내보내기 할 때, `React.memo`로 감싸주기만 하면 된다.
```

위처럼 하면 props가 바뀌었을 떄만 리렌더링 한다.

두번째 파라미터에 propsAreEqual 이라는 함수를 넣어줄 수 있음.   
전 프롭스와 이후 프롭스를 비교. 트루 -&gt; 방지 false -&gt; 리랜더링

#### 요약

연산된 값 재사용 : `useMemo()` 특정 함수를 재사용 : `useCallback()` 컴포넌트 재사용 : `React.memo()`

주의 : 최적화가 필요하다고 판단될 때만 사용

