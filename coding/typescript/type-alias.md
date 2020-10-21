# 타입별칭

## 타입 별칭

* 타입 별칭\(Type-alias\) : interface와 비슷하지만 직접 작성한 타입에 이름을 붙일 수 있다.
  * intersection타입을 타입으로 부여하기

    > ```typescript
    > interface User {
    >     name : string;
    > }
    > interface Action {
    >     do() : void;
    > }
    > ​
    > type UserAction = User & Action;
    > ​
    > function createUserAction():UserAction {
    >     return {
    >         name: 'test',
    >         do(){
    >             console.log('test');
    >         }
    >     }
    > }
    > ```

  * 원시형과 제네릭에서도 사용 가능

    > ```typescript
    > // 원시형도 사용 가능
    > type StringOrNumber = string | number;
    > ​
    > // 제네릭
    > type Arr<T> = T[];
    > type P<T> = Promise<T>;
    > ```

  * 단순히 이름만 부여하는 것이 아니라 특정 타입을 정의할 수도 있다.

    > ```typescript
    > type User2 = {
    >     name: string;
    >     login(): boolean;
    > }
    > ​
    > class UserImpl implements User2 {
    >     login(): boolean {
    >         throw new Error("Method not implemented.");
    >     }
    >     name : string;
    > }
    > ```

  * 문자와 함께 활용할 수도 있다.

    > ```typescript
    > type UserState = "PENDING" | "APPROVED" | "REJECTED";
    > ​
    > type User2 = {
    >     name: string;
    >     login(): boolean;
    > }
    > ​
    > function checkuser(user:User2):UserState {
    >     if(user.login()){
    >         return "APPROVED"
    >     } else {
    >         return "REJECTED"
    >     }
    > }
    > ```

