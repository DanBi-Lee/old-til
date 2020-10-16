# tsc-watch

## 타입스크립트 자동으로 컴파일하기

1. tsc-watch설치

   > `yarn add tsc-watch --dev`

2. `package.json`설정 변경

   > ```javascript
   > {
   >   "name": "typechain",
   >   "version": "1.0.0",
   >   "main": "index.js",
   >   "repository": "https://github.com/DanBi-Lee/typechain.git",
   >   "author": "DanBi-Lee <danbi.s.rain@gmail.com>",
   >   "license": "MIT",
   >   "scripts": {
   >     "start": "tsc-watch --onSuccess \" node dist/index.js\" "
   >   },
   >   "devDependencies": {
   >     "tsc-watch": "^4.2.9"
   >   },
   >   "dependencies": {
   >     "typescript": "^4.0.3"
   >   }
   > }
   > ```

3. `tsconfig.json`설정 변경

   > ```javascript
   > {
   >     "compilerOptions" : {
   >         "module" : "commonjs", // node.js를 평범하게 사용하고 다양한걸 import하거나 export할 수 있게 만듦
   >         "target" : "ES2015", // 어떤 버전의 JavaScript로 컴파일 되고 싶은지 작성
   >         "sourceMap" : true, // sourcemap 처리를 하고싶은지
   >         "outDir": "dist" //컴파일 된 js파일이 생기는 위치
   >     },
   >     // 어떤 파일들이 컴파일 과정에 포함되는지 설정
   >     "include": [
   >         "src/**/*"
   >     ],
   >     // 포함되지 않을 파일 설정
   >     "exclude" : [
   >         "node_modules"
   >     ]
   >    }
   > ```

### tsc-watch 사용시, 예상 이슈

{% embed url="https://github.com/TypeStrong/ts-node/issues/707\#issuecomment-457448149" %}

