# Ajax

{% embed url="https://opentutorials.org/course/3281" %}

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

> 리를 알면 자유도가 높아지는 것이다.

