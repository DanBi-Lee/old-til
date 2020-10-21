# 인덱스 타입

## 인덱스 타입

* 인덱스 타입 : 속성 이름이 정해져있지 않고 동적으로 처리해야 할 때 사용
  * 예시

    > ```typescript
    > interface Props {
    >     name : string;
    >     [key :  string] : string; 
    >     // index 시그니쳐 매개변수 형식은 string혹은 number여야 한다.
    > }
    > ​
    > const p: Props = {
    >     a : 'd',
    >     b : 'e',
    >     c : '3',
    >     0 : 'd',
    >     1 : 'b',
    >     name : 'hello'
    > }
    > ​
    > p[0] // key가 string이면 숫자도 넣을 수 있지만 number면 문자를 넣을 수 없다.
    > p.name // name은 보장 받는다.
    > ```

  * 인덱스 타입과 관련된 오퍼레이터

    > ```typescript
    > interface Props {
    >     name : string;
    >     [key :  string] : string; 
    >     // index 시그니쳐 매개변수 형식은 string혹은 number여야 한다.
    > }
    > ​
    > let keys: keyof Props;
    > ​
    > interface User {
    >     name: string;
    >     age: number;
    >     hello(msg:string): void;
    > }
    > ​
    > let keysOfUser: keyof User;
    > keysOfUser = "age";
    > ​
    > // 유저의 특정한 타입들을 키 이름으로 가져올 수 있다.
    > ​
    > let helloMethod: User["hello"];
    > helloMethod = function(){
    > ​
    > };
    > ```

