# 리액트 Hook 메모



## Hook 메모

* useState
* useRef
* useEffect
  * 업데이트 된 뒤, 되기 전에 작업 가능
  * 사용 예시 : 유저네임과 UrlSlug를 가져와서... 그 다음에 뭔가 작업을 할 때에..
  * 마운트, 언마운트
    * 마운트 : 나타날 떄
    * 언마운트 : 사라질때

```javascript
    useEffect(()=>{
        console.log('컴포넌트가 화면에 나타남');
        // props -> state
        // REST API
        // D3 Video.js
        // setInterval, setTimeout
        return ()=> {
            // clearInterval, clearTImeout
            // 라이브러리 인스턴스 제거
            console.log('컴포넌트가 화면에서 사라짐');
        }
    }, []);// 조회하고 있는 상태가 있다면 []안에 넣어주어야 한다. 그래여 변경될 때도 호출됨
```

* useMemo
  * 이전에 연산된 값 재사용
  * 주로 성능을 최적화 해야할 떄 사용
  * 특정 값이 바꼈을 때만 연산한다.

```javascript
function countActiveUsers(users){
  console.log('활성 사용자 수를 세는중...');
  return users.filter(user=>user.active).length;
}
​
const count = useMemo(()=>countActiveUsers(users), [users]);
```

* useCallback
  * 이전에 만든 함수를 새로 만들지 않고 재사용 \(useMemo와 비슷\)
  * 문제점 : 기존에 함수를 선언했던 것은 리랜더링 할 때마다 새로 함수를 다시 선언하고 있었다. 선능이 많이 떨어지는 것은 아니지만, 재사용 할 수 있으면 하는 것이 좋다
    * 이유 : 나중에 컴포넌트들이 virtualDOM에 하는 리랜더링조차 하지 않게 만들 수도 있다. \(그 작업을 하기 위한 선행작업\)
* React.memo
  * 컴포넌트에서 리랜더링이 불필요할 때, 방지.
  * export할 때 React.memo로 감싸주면 최적화 끝. \(props가 바뀌었을 떄만 리랜더링 한다고함\)
  * export 없으면 함수 자체를 감싸주면 최적화가 어느정도 된다.

