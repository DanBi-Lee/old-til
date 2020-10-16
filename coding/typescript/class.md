# Class

interface는 자바스크립트로 컴파일되지 않는다.   
interface를 컴파일 하고 싶을 때, 대신 class를 사용한다.

```typescript
class Human {
    public name:string;
    public age: number;
    public gender:string;
    constructor(name:string, age:number, gender:string){
        this.name= name;
        this.age = age;
        this.gender = gender;
    }
}
​
const plyrn = new Human("Syn", 18, "female");
​
const sayHi = (person:Human):string => {
    return `Hello, ${person.name}. you are ${person.age}, you are a ${person.gender}!!!`;
};
​
console.log(sayHi(plyrn));
​
export {};
```

