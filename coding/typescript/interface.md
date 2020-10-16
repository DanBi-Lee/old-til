# Interface

## interface

객체 안 속성의 타입을 정할 때 사용한다.

```typescript
interface Human {
    name :string,
    age:number,
    gender:string
}
​
const person = {
    name: "Dan",
    age : 29,
    gender: "female"
};
​
const sayHi = (person:Human):string => {
    return `Hello, ${person.name}. you are ${person.age}, you are a ${person.gender}!!!`;
};
​
console.log(sayHi(person));
​
export {};
```

