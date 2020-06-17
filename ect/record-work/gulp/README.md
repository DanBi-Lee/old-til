# Gulp 세팅

{% embed url="https://nomadcoders.co/gulp-for-beginners/lobby" caption="노마드 코더 gulp 90분 수업" %}

※ window기준으로 정리

1. gulp를 컴퓨터 전역 / 해당 폴더에 설치
   * 전역에 설치
     * ```text
       yarn add gulp-cli -g
       ```
     * ```text
       npm intall gulp-cli -g
       ```
   * 폴더에 설치
     * ```text
       yarn add gulp --dev
       ```
     * ```text
       npm install gulp --save -dev
       ```

       * `--dev` === `D` : 내 컴퓨터에 개발자모드로 설치하겠다는 의미
2. 환경설정 \(src 폴더 생성 및 git init 등\)
3. `yarn init`명령어 실행

   > error An unexpected error occurred: "Can't answer a question unless a user TTY". info If you think this is a bug, please open a bug report with the information provided in "E:\\\(중략\)studyGulp\yarn-error.log". info Visit [https://yarnpkg.com/en/docs/cli/init](https://yarnpkg.com/en/docs/cli/init) for documentation about this command.

   위와 같은 에러 발생 시 git bash 가 아닌 내장 CMD창을 통해 명령어 실행 \(shift+우클릭 하여 셸 실행\)

4. src 내부 파일 세팅
5. `gulpfile.js`생성
6. `package.json`에 추가
   1. ```text
      {
        "name": "supergulp",
        "version": "1.0.0",
        "description": "learn gulp",
        "repository": "https://github.com/DanBi-Lee/studyGulp.git",
        "author": "LeeDanBi <goldq0531@gmail.com>",
        "license": "MIT",
        "scripts": {
          "dev": "gulp dev",
          "build": "gulp build"
        },
        "dependencies": {
          "gulp": "^4.0.2"
        }
      }
      ```
7. `yarn add gulp`
8. `yarn add gulp -D`
9. 후에 gulpfile.js에 `const gulp = require("gulp");`구문 입력후 `yarn dev`실행하면 됨
   * import로 사용하는 방법
     1. gulpfile.js를 gulpfile.babel.js로 이름 수정
     2. .babelrc 파일 생성
        * ```text
          {
              "presets": ["@babel/preset-env"]
          }
          ```
     3. `gulp dev` : 오류 뜨는데 최신버전 앞에는 @가 붙음
        1. `yarn add @babel/{register,core,preset-env}`
10. gulp task만들기
    * task 설명
      * `export const dev = () => console.log("I will dev");`와 같은 식으로 하면 됨
      * task는
        * 모든 pug파일을 가지고 다른 폴더에 집어넣는 식의 작업
        * scss를 css로 변환하고 최소화시키는 등의 작업

    1. 플러그인 설치 \(pug\)
       1. `yarn add gulp-pug -D`
       2. 다음으로 다운받은 플러그를 import해준 뒤, 함수를 만들어 export해주면 된다. \(export는 package.json에서 쓸 command만 해주면 된다.\)
          * 함수의 return이 task로 실행되는 것.
          * pipe로 작업 연결
            * src가 작업파일은 모으는 것
            * dest가 작업파일을 풀어놓는 것
       3. `yarn add del` \(지우는 작업\)
       4. build를 위한 준비과정과 실제로 파일을 변형시키는 작업이 나눠져 있는데, 이것을 의미있는 작업 별로 다시 묶어주는 작업을 한다.
11. 웹서버 만들기
    1. `yarn add gulp-webserver`
       * 여기까지 해도 자동 리로드 되지는 않는다. 왜냐하면 watch하고 있지 않기 때문에.
    2. parallel에 watch를 추가

       > parrallel은 순서 상관없이 작업

    3. 지켜봐야 할 파일과 컴파일 해야 하는 파일이 있다는 점에 유의
12. 이미지 다루기
    1. `yarn add gulp-image`
    2. img가 시간을 잡아먹을 수 있기에 assets에 포함시키지는 않는 것을 권장하지만 어떻게 하고 싶은지는 자유
13. scss 다루기
    1. `yarn add node-sass gulp-sass`
    2. scss파일 앞 \_의 의미 : 앞에 \_가 붙은 파일은 compile하지는 말고 사용만 하라고 알려줌
    3. gulp-autoprefixer : 코드를 알아듣지 못하는 구형 브라우저도 호환 가능하도록 만들어줌
       1. `yarn add gulp-autoprefixer`
          * gulp-autoprefixer의 옵션으로 browser을 사용하면 작동은 되지만 경고문이 떴다.
          * browser옵션을 사용하는 대신 package.json에서 browserlist 키와 키값을 입력하는 것으로 해결했다.
    4. gulp-csso : css 최소화
       1. `yarn add gulp-csso`
14. JS 다루기
    * 해야할 일
      * 자바스크립트를 babel에서 실행시키는 것
      * browserify에서 실행시키는 것
        * browserify : 개발자들이 브라우저에서 Node.js 스타일의 모듈을 사용하기 위한 오픈 소스 JS툴
          * 브라우저는 import나 export같은 걸 이해하지 못함
          * browerify가 위와 같은 코드를 이해하게 도와준다.

        1. browserify import하기
        2. 그 browserify안에 babel 실행

    1. gulp-browserify유지보수를 안해서 -&gt; gulp-bro 사용
       1. `yarn add gulp-bro`
       2. `yarn add babelify`
       3. `yarn add uglifyify`
15. 배포하기
    1. gulp github pages
       1. `yarn add gulp-gh-pages`
          * gulp-gh-pages 사용할 경우 에러가 날 수 있다.
          * ```text
            cd node_modules/gulp-gh-pages/
            yarn add gift@0.10.2
            cd ../../
            gulp deploy
            ```

### 최종 세팅 파일

{% tabs %}
{% tab title="gulpfile.babel.js" %}
```javascript
import gulp from "gulp";
import gpug from "gulp-pug";
import del from "del";
import ws from "gulp-webserver";
import image from "gulp-image";
import sass from "gulp-sass";
import autoPrefixer from "gulp-autoprefixer";
import miniCSS from "gulp-csso";
import bro from "gulp-bro";
import babelify from "babelify";
import ghPages from "gulp-gh-pages";

sass.compiler = require("node-sass");

const routes = {
  pug: {
    watch: "src/**/*.pug",
    src: "src/*.pug",
    dest: "build"
  },
  img: {
    src: "src/img/*",
    dest: "build/img"
  },
  scss: {
    watch: "src/scss/**/*.scss",
    src: "src/scss/style.scss",
    dest: "build/css"
  },
  js: {
    watch: "src/js/**/*.js",
    src: "src/js/main.js",
    dest: "build/js"
  }
};

const pug = () =>
  gulp
    .src(routes.pug.src)
    .pipe(gpug())
    .pipe(gulp.dest(routes.pug.dest));


const clean = () => del(["build/", ".publish"]); //build를 위한 준비과정

const webserver = () => gulp.src("build").pipe(ws({ livereload: true }));

const img = () =>
  gulp
    .src(routes.img.src)
    .pipe(image())
    .pipe(gulp.dest(routes.img.dest));

const styles = () =>
  gulp
    .src(routes.scss.src)
    .pipe(sass().on("error", sass.logError))
    .pipe(autoPrefixer())
    .pipe(miniCSS())
    .pipe(gulp.dest(routes.scss.dest));

const js = () => 
  gulp.src(routes.js.src)
  .pipe(bro({
    transform: [
      babelify.configure({ presets: ['@babel/preset-env'] }),
      [ 'uglifyify', { global: true } ]
    ]
  }))
  .pipe(gulp.dest(routes.js.dest));

const gh = () => gulp.src("build/**/*").pipe(ghPages());

const watch = () => {
  gulp.watch(routes.pug.watch, pug);
  gulp.watch(routes.img.src, img);
  gulp.watch(routes.scss.watch, styles);
  gulp.watch(routes.js.watch, js);
};

const prepare = gulp.series([clean, img]);

const assets = gulp.series([pug, styles, js]);

const live = gulp.parallel([webserver, watch]);

export const build = gulp.series([prepare, assets]);
export const dev = gulp.series([build, live]);
export const deploy = gulp.series([build, gh, clean]);
```
{% endtab %}

{% tab title="package.json" %}
```javascript
{
  "name": "supergulp",
  "version": "1.0.0",
  "description": "learn gulp",
  "repository": "https://github.com/DanBi-Lee/studyGulp.git",
  "author": "LeeDanBi <goldq0531@gmail.com>",
  "license": "MIT",
  "scripts": {
    "dev": "gulp dev",
    "build": "gulp build",
    "deploy": "gulp deploy"
  },
  "devDependencies": {
    "@babel/core": "^7.4.5",
    "@babel/preset-env": "^7.4.5",
    "@babel/register": "^7.4.4",
    "del": "^5.1.0",
    "gulp": "^4.0.2",
    "gulp-image": "^6.2.0",
    "gulp-pug": "^4.0.1",
    "gulp-webserver": "^0.9.1"
  },
  "dependencies": {
    "babelify": "^10.0.0",
    "gift": "0.10.2",
    "gulp-autoprefixer": "^7.0.1",
    "gulp-bro": "^2.0.0",
    "gulp-csso": "^4.0.1",
    "gulp-gh-pages": "^0.5.4",
    "gulp-sass": "^4.1.0",
    "node-sass": "^4.14.1",
    "uglifyify": "^5.0.2"
  },
  "browserslist": [
    "defaults",
    "last 2 versions"
  ]
}

```
{% endtab %}

{% tab title=".babelrc" %}
```javascript
{
    "presets": ["@babel/preset-env"]
}
```
{% endtab %}

{% tab title=".gitignore" %}
```
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Runtime data
pids
*.pid
*.seed
*.pid.lock

# Directory for instrumented libs generated by jscoverage/JSCover
lib-cov

# Coverage directory used by tools like istanbul
coverage

# nyc test coverage
.nyc_output

# Grunt intermediate storage (http://gruntjs.com/creating-plugins#storing-task-files)
.grunt

# Bower dependency directory (https://bower.io/)
bower_components

# node-waf configuration
.lock-wscript

# Compiled binary addons (https://nodejs.org/api/addons.html)
build/Release

# Dependency directories
node_modules/
jspm_packages/

# TypeScript v1 declaration files
typings/

# Optional npm cache directory
.npm

# Optional eslint cache
.eslintcache

# Optional REPL history
.node_repl_history

# Output of 'npm pack'
*.tgz

# Yarn Integrity file
.yarn-integrity

# dotenv environment variables file
.env

# next.js build output
.next
build/
```
{% endtab %}
{% endtabs %}



gulp를 다양한 용도로 사용할 수 있다.

> * 파일 옮기는 용도
> * 이름 변경 용도
> * 파일을 지우는 용도

