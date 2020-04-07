# Ajax

{% embed url="https://opentutorials.org/course/3281" caption="생활코딩 강의 참고" %}

{% hint style="info" %}
책만으로 공부하기에 php가 함께 나와서, 생활코딩 -ajax 강의를 참고했다.
{% endhint %}



### fetch API

#### 1. 무작정 fetch 사용해보기

```markup
<!DOCTYPE html>
<html>
<body>
    <article>
    </article>
    <input type="button" value="fetch" onclick="
        fetch('css').then(function(response){//요청
            response.text().then(function(text){ // 데이터
                document.querySelector('article').innerHTML = text; // 실행
            })
        })
    ">
</body>
</html>
```

추가 준비물 : 웹서버, css라는 이름의 파일

> 사용법만 알아도 사용할 수 있다. 사용하는 자유도에 한계를 느낀 후에 원리를 파고들어도 괜찮다.

#### 2. fetch API 원리 알기

요청과 응답 

* `fetch('javascript')` : 서버에게 자바스크립트라는 파일을 응답해줘 
* `then()` : 시간이 오래 걸릴 수 있으니까... 뒤에 응답한다.

response

* response 객체 : 응답 결과를 담고 있는 객체 여러 속성을 통해 서버와 통신 상태를 알 수 있다

ex. `response.status` 

```markup
<!DOCTYPE html>
<html>
<body>
    <article>

    </article>
    <input type="button" value="fetch" onclick="
        fetch('html').then(function(response){
                console.log(response.status);
                if(response.status == '404'){
                    alert('Not found');
                }
            });
        console.log(1);
        console.log(2);
    ">
</body>
</html>
```

> 원리를 알면 자유도가 높아진다.

#### 3. 초기페이지 구현하기

* **사용 이유**
  * Ajax를 이용하여 페이지의 리로딩 없이 정보를 읽어들일 수 있었다. \(SPA\)
  * 대신 url이 변하지 않아서 그 페이지를 다시 찾거나, 공유하기 어려워졌다. 해시라는 것을 사용하여 url을 표시할 수 있다.
* **맹점**
  * 검색엔진 최적화가 잘 되지 않는다. 검색엔진에서 웹을 수집할 떄 웹 페이지를 다운받아서 작성되는데, 실제 내용이 없기 때문이다.
  * 그러므로 `#!`\(해시뱅\)을 이용해서 하는 방식은 현시점에서는 사용하지 않고, pjax\(pushState + ajax\)라는 기술을 사용한다.

```markup
<!doctype html>
<html>
<head>
  <title>WEB1 - Welcome</title>
  <meta charset="utf-8">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
  <script src="colors.js"></script>
</head>
<body>
  <h1><a href="#!welcome">WEB</a></h1>
  <input id="night_day" type="button" value="night" onclick="
    nightDayHandler(this);
  ">
  <ol id="nav">
    <li><a href="#!html" onclick="fetchPage('html')">html</a></li>
    <li><a href="#!css" onclick="fetchPage('css')">css</a></li>
    <li><a href="#!javascript" onclick="fetchPage('javascript')">javascript</a></li>
  </ol>
  <article>

  </article>
  <script>
  function fetchPage(name){
    fetch(name).then(function(response){
      response.text().then(function(text){
        document.querySelector('article').innerHTML = text;
      })
    });
  }
  if(location.hash){
    fetchPage(location.hash.substr(2));
  } else {
    fetchPage('welcome');
  }
  </script>
</body>
</html>
```

#### 4. 글목록 ajax로 구현하기

데이터 로직, 그리고 데이터와 애플리케이션 구분되어야 한다. 데이터와 애플리케이션이 혼재되어 있다면, 이것을 분리할 필요가 있다.

```markup
<!doctype html>
<html>
<head>
  <title>WEB1 - Welcome</title>
  <meta charset="utf-8">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
  <script src="colors.js"></script>
</head>
<body>
  <h1><a href="index.html">WEB</a></h1>
  <input id="night_day" type="button" value="night" onclick="
    nightDayHandler(this);
  ">
  <ol id="nav">

  </ol>
  <article></article>
  <script>
    function fetchpage(name){
      fetch(name).then(function(response){
        response.text().then(function(text){
          document.querySelector('article').innerHTML = text;
        });
      });
    }
    if(location.hash){
      fetchpage(location.hash.substr(2));
    }else{
      fetchpage('welcome');
    }
    fetch('list').then(function(response){
        response.text().then(function(text){
          var items = text.split(',')
          var i = 0;
          var tags = '';
          while(i < items.length){
            var item = items[i].trim();
            // <li><a href="#!html" onclick="fetchpage('html')">HTML</a></li>
            var tag = '<li><a href="#!' + item + '" onclick="fetchpage(\'' + item + '\')">' + item + '</a></li>'
            tags = tags + tag;
            i++;
          }
          document.querySelector('#nav').innerHTML = tags;
        });
      });
  </script>
</body>
</html>
```

#### 5.fetch API polyfill

XMLHttpRequest와 같은 API가 존재하지만 Fetch API는 좀 더 강력하고 유연한 조작이 가능하다. \(미래지향적\)

* 문제 : 브라우저 호환성
* 해결 방법 : 웹은 공공재. 브라우저, 브라우저 버전마다 차이가 있을 수 있다. 크로스 브라우징 하는 방법 알기
  1. caniuse.com에서 사용 가능 브라우저 점유율 확인
  2. 다른 방식으로쓸지 정하자.
  3. 다른 방식 : fetch api polyfill
     * polyfill : 브라우저에서 기능을 지원하지 않는 경우 대신 지원해주는 기능.
     * 다운로드 : [https://github.com/github/fetch](https://github.com/github/fetch)

{% code title="head태그 안" %}
```markup
<script src="https://polyfill.io/v3/polyfill.js?features=fetch"></script>
<script src="fetch/fetch.js"></script>
```
{% endcode %}



#### 6. 마무리

* 요약
  * ajax를 이용해서 서버로부터 동적으로 페이지 교체, 문서에서 확장되어서 애플리케이션 대열에 합류 했다.
  * 웹은 문서 -&gt; 문서 토대 위에 동적으로 얹어놓으 것. 웹은 검색이 되면서 어플리케이션 역할을 한다.
* **앞으로 공부할 주제**
  * 예제에선 다루지 않았지만 json으로 정보를 구조화하면 더 풍부하게 표현할 수 있다.
  * SPA 싱글 페이지 애플리케이션을 만드는 것에 여러 기법이 있다.
  * PJAX \(pushState+ajax\)
    * 검색엔진에서 찾게 해준다.
  * Progressive Web Apps?
    * SPA에 오프라인으로도 동작하는 특성이 추가되었다.
    * online + offline

