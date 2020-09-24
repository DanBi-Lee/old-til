# Redux

## 리덕스

상태관리 라이브러리

컴포넌트의 상태관리 로직을 다른 파일로 분리 관리

글로벌 상태관리도 손쉽게 할 수 있다.

Context API + useReducer

는 리덕스를 사용하는 것과 개발방식이 유사하다.

그런데 리덕스가 먼저 나왔다.

리액트를 사용하는 프로젝트 중 45%가 리덕스를 사용중이다. \(통계적으로\)

일반 자바스크립트나 앵귤러 같은 다른 프로젝트에서 리덕스를 사용할 수 있다.

* 리덕스 활용
  * 단순히 글로벌 상태를 관리하거나 별로 없다면 Context API를 활용하는 것 만으로 충분
* Context와 차이
  1. 미들웨어

     > 비동기 작업을 더욱 체계적으로 관리할 수 있다.

  2. 유용한 함수와, Hooks

     > 예\) connect, useSelector, useDispatch, useStore
     >
     > Context를 사용한다면 직접 만들어야 한다.

  3. 기본적인 최적화가 이미 되어있다.
  4. 하나의 커다란 상태
  5. DevTools

     > 현재 상태를 한눈에 볼 수 있고, 특정 시점으로 되돌릴 수 있다.

  6. 이미 사용중인 프로젝트가 많다.
* 리덕스 언제 써야 할까?
  * 프로젝트의 규모가 큰가?
    * Y - Redux , N - Context API
  * 비동기 작업을 자주 하게 되나요?
    * Y - Redux, N - Context API
  * 리덕스가 편하게 느껴지나요?
    * Y - Redux, N - Context API or MobX

### 리덕스에서 사용되는 키워드 숙지하기

* 액션 \(Action\)
  * 상태의 변화가 필요하게 될 때 발생시킨다.
  * 상태가 업데이트 될 때 어떻게 업데이트 할지 정보를 지니고 있는 객체
  * type값을 필수로 가지고 있다.
  * 형식

    ```text
    {
        type : "ADD_TODO",
        data : {
            id : 0,
            text : "리덕스 배우기"
        }
    }
    ```

    ```text
    {
        type : "CHANGE_INPUT",
        text : "안녕하세요"
    }
    ```
* 액션 생성함수 \(Action Creator\)
  * 액션을 만들어주는 함수 \(파라미터를 받아와서 액션 객체를 만들어주는 함수\)
  * 형식

    ```text
    export function addTodo(data){
        return {
            type: "ADD_TODO",
            data
        };
    }
    ​
    // 화살표 함수로도 만들 수 있다.
    export const changeInput = text => ({
        type: "CHANGE_INPUT",
        text
    });
    ```

  * 필수는 아니지만 액션 생성함수로 편하게 액션을 만들 수 있다.
* 리듀서 \(Reducer\)
  * 상태를 바꿔주는 함수

    > 액션 타입이 무엇이냐에 따라

  * 형식

    ```text
    function counter(state, action){
        switch (action.type){
            case 'INCREASE' :
                return state + 1;
            case 'DECARESE' :
                reutrn state - 1;
            default :
                return state;
        }
    }
    ```

  * reducer에서는 불변성을 유지해줘야 한다.
  * 리듀서의 default에서는 기존의 state를 그대로 반환해줘야 한다.
  * 루트 리듀서 / 서브 리듀서가 있음
* 스토어 \(Store\)
  * 한 애플리케이션 당 하나의 스토어를 만들게 된다.
  * Store에는 내장함수가 있다.
    * 디스페치 \(dispatch\)
      * 액션을 발생시킴 / 액션을 스토어에 전달

        ```text
        dispatch({ type : 'INCREASE' })
        ```
    * 구독 \(subscribe\)
      * 액션이 디스패치 될 때마다\(state가 업데이트 될때마다\) 특정 함수 호출
      * 컴포넌트가 리덕스의 상태 구독
        * 리덕스가 업데이트 되면 컴포넌트도 리랜더링

### 리덕스의 3가지 규칙

1. 하나의 애플리케이션엔 하나의 스토어가 있다.

   > 스토어를 하나 이상 만들면 안 된다. \(비권장\)

2. 상태는 읽기전용이다. \(불변성을 지켜야 한다\)

   > 스프레드 연산자를 사용하거나, concat, filter, map 같은 불변성을 유지하는 메서드만 사용할 수 있다.

3. 변화를 일으키는 함수, 리듀서는 순수한 함수여야 한다.

   > 순수한 함수란,
   >
   > 리듀서 함수는 이전 상태와 액션 객체를 파라미터로 받는다. 이전의 상태는 절대로 변경하지 않고, 변화를 일으킨 새로운 상태 객체를 만들어서 반환해야 한다. \(불변성 유지\) **똑같은 파라미터**로 호출된 리듀서 함수는 **언제나 똑같은 결과값**을 반환해야 한다.

   * 동일한 인풋 -&gt; 동일한 아웃풋

     > * `new Date()`
     > * `Math.random()`
     > * `axios.get()`
     >
     > 사용 불가.
     >
     > 리듀서 밖에 있는 변수에 의존하면 안 된다. \(상수라면 상관없음\) state와 action만 의존하여야 함.
     >
     > 사용하려면 미들웨어를 사용하여야 함.

