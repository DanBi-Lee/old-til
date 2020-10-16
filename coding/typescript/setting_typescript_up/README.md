# 타입스크립트 시작하기

## 타입스크립트 시작하기

1. 타입스크립트 설치
   * `yarn global add typescript`
2. 타입스크립트 옵션 설정하기

   1. `tsconfig.json`파일 생성
      * 이 파일에 TypeScript에게 어떻게 JavaScript로 변환하는지 알려주면서 옵션 설정한다.

   > ```javascript
   > {
   >  "compilerOptions" : {
   >      "module" : "commonjs", // node.js를 평범하게 사용하고 다양한걸 import하거나 export할 수 있게 만듦
   >      "target" : "ES2015", // 어떤 버전의 JavaScript로 컴파일 되고 싶은지 작성
   >      "sourceMap" : true, // sourcemap 처리를 하고싶은지
   >  },
   >  // 어떤 파일들이 컴파일 과정에 포함되는지 설정
   >  "include": [
   >      "index.ts"
   >  ],
   >  // 포함되지 않을 파일 설정
   >  "exclude" : [
   >      "node_modules"
   >  ]
   > }
   > ```

3. 컴파일 해보기
   1. > 1. `index.ts` 작성
      >
      > ```typescript
      > alert("hello");
      > ```
      >
      > 1. 컴파일
      >
      >    > ```bash
      >    > tsc
      >    > ```
      >
      >    * `package.json`설정
      >
      >      > ```javascript
      >      > {
      >      >   "name": "typechain",
      >      >   "version": "1.0.0",
      >      >   "main": "index.js",
      >      >   "repository": "https://github.com/DanBi-Lee/typechain.git",
      >      >   "author": "DanBi-Lee <danbi.s.rain@gmail.com>",
      >      >   "license": "MIT",
      >      >   "scripts" : {
      >      >     "start" : "node index.js",
      >      >     "prestart": "tsc"
      >      >   }
      >      > }
      >      > ​
      >      > ```

