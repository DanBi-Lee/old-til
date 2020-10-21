# Intersection & Union

## Intersection & Union타입

* intersection타입 : 여러 타입이 하나로 합쳐진 타입
  * 예제 : User 인터페이스와 Action 인터페이스 intersection타입으로 만들어 보기

    > ```typescript
    > interface User {
    >     name : string;
    > }
    > interface Action {
    >     do() : void;
    > }
    > ​
    > function createUserAction (u: User, a:Action): User & Action {
    >     return { ...u, ...a };
    > }
    > const u = createUserAction({ name: 'jay'} , {do(){}});
    > ```

  * 활용성 : 클래스를 상속하지 않고 인터페이스를 활용할 수 있음
* union타입 : or 기호를 사용해서 타입을 표시하는 것
  * 예제

    > ```typescript
    > function compare(x:string, y:string);
    > function compare(x:number, y:number);
    > function compare(x : string | number  ,y : string | number) {
    >     // or 기호를 사용해서 타입을 표시하는 것이 union타입
    >     // 이럴경우 매개변수를 사용하려고 할 경우 공통되는 메서드가 나타남
    >     // x.toLocaleString 등..
    >     if (typeof x === 'number' && typeof y === 'number'){
    >         return x === y ? 0 : x > y ? 1 : -1 ;
    >     }
    >     if (typeof x === 'string' && typeof y === 'string'){
    >         return x.localeCompare(y);
    >     }
    >     throw Error('not supported type');
    > }
    > const v = compare(1, 2);
    > const v2 = compare("a", "b");
    > const v3 = compare("a", 1); // 선언된 오버로딩이 없어서 오류
    > console.log([3,2,1].sort(compare));
    > ```

  * 예제 : interface를 union타입으로 설정하기

    > ```typescript
    > interface User {
    >     name : string;
    > }
    > interface Action {
    >     do() : void;
    > }
    > ​
    > function isAction(v: User | Action): v is Action { // 사용자정의 타입가드
    >     return (<Action>v).do !== undefined;
    > }
    > ​
    > function process(v: User | Action){
    >     if(isAction(v)){ // 타입가드
    >         v.do()
    >     }else{
    >         v.name
    >     }
    > }
    > ```

  * union타입을 사용할 때는 타입가드를 사용하여 타입을 보장한다.

