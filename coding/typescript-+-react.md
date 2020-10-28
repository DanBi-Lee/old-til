# TypeScript + React

## 타입스크립트로 리액트 컴포넌트 만들기

create-react-app 에서 타입스크립트를 지원한다. \(타입스크립트를 쓴다는 옵션을 줄 경우\)

1. `yarn create react-app my-app --template typescript`
2. 확장자가 `.tsx`가 되어있다.

   > ```jsx
   > import React from 'react';
   > import logo from './logo.svg';
   > import './App.css';
   > ​
   > const App: React.FC = () => {
   > return (
   >  <div className="App">
   >    <header className="App-header">
   >      <img src={logo} className="App-logo" alt="logo" />
   >      <p>
   >        Edit <code>src/App.tsx</code> and save to reload.
   >      </p>
   >      <a
   >        className="App-link"
   >        href="https://reactjs.org"
   >        target="_blank"
   >        rel="noopener noreferrer"
   >      >
   >        Learn React
   >      </a>
   >    </header>
   >  </div>
   > );
   > }
   > ​
   > export default App;
   > ​
   > ```
   >
   > 위와 같이 화살표 함수로 되어있고 React.FC로 타입이 선언되어 있다.

   * React.FC로 선업할 때의 장단점
     * 장점
       * chilren이라는 props가 기본적으로 탑재되어 있음
         * 그러나 단점이 될 수 있다. 모든 컴포넌트에 children가 기본으로 들어가 있다면 명료하지 않다. \(React.FC가 있긴 하지만 선호하지 않는 개발자도 있다.\)
     * 단점
       * defaultProps가 정상작동하지 않음

         > ```jsx
         > const Greetings : React.FC<GreetingsProps> = ({name, mark= "!", array}) => {
         >  return <div>
         >      Hello, {name} {mark}
         >      {array}
         >  </div>
         > };
         > ```
         >
         > 위 처럼 해줘야함.
   * function 키워드로 함수 만들 때

     * 이경우엔 children이 기본으로 들어가지 않음

       > ```jsx
       > type GreetingsProps = {
       >  name: string;
       >  mark: string;
       >  optional? :string;
       >  onClick: (name:string)=>void;
       >  children? : React.ReactNode;
       > };
       > ```

     > ```jsx
     > import React from 'react';
     > ​
     > type GreetingsProps = {
     >  name: string;
     >  mark: string;
     >  optional? :string;
     >  onClick: (name:string)=>void;
     > };
     > ​
     > function Greetings({name, mark, onClick}:GreetingsProps){
     >  const handleClick = () => onClick(name);
     >  return <div>
     >      Hello, {name} {mark}
     >      <div><button onClick={handleClick}>
     >          Click me!
     >          </button></div>
     >  </div>
     > };
     > ​
     > Greetings.defaultProps = {
     >  mark : '?'
     > };
     > ​
     > ​
     > export default Greetings;
     > ```
     >
     > ```jsx
     > import React from 'react';
     > import './App.css';
     > import Greetings from './Greetings';
     > ​
     > const App: React.FC = () => {
     > const onClick = (name:string) => {
     >  console.log(name);
     > }
     > return (
     >  <Greetings name="리액트" onClick={onClick} />
     > );
     > }
     > ​
     > export default App;
     > ```

리액트 함수 만드는 다른 방법과 장단점

```jsx
const Greetings = React.FC<GreetingsProps> = () => null
```

다음 시간

타입스크립트를 사용하는 리액트 프로젝트에서

Context API를 어떻게 써야 편한지 알아보자

