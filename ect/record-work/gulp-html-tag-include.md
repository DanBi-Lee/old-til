---
description: gulp로 html 편하게 쓰기
---

# gulp-html-tag-include

{% embed url="https://www.npmjs.com/package/gulp-html-tag-include" %}

gulp강의에는 pug를 사용하는 방법을 소개해줬지만, pug의 필요성을 아직 느끼지 못하여 배울 단계가 아닌 것 같다.

그래서 스터디 강사님이 소개해주셨던 gulp-html-tag-include를 사용하려고 한다.

홈페이지에 소개된 사용 예시

```markup
<include src="filename.html" label="Lorem ipsum dolor sit amet"><input type="text" /></include>
```

{% code title="filename.html" %}
```markup
<label>@@label: @@content</label>
```
{% endcode %}

{% code title="result" %}
```markup
<label>Lorem ipsum dolor sit amet: <input type="text" /></label>
```
{% endcode %}

`@@`가 앞에 붙어있으면 변수처럼 사용할 수 있다. \(react가 생각나는 방식인 것 같다\)

`@@content`를 사용하면 include태그 안에 다른 태그를 사용할 수 있다.

다른 예시로는 헤더, 본문, 푸터 처럼 쪼개는데 이부분은 php include가 떠올랐다. 신기하고 좋은 기능! 그런데 예시처럼 너무 많이 쪼개면 복잡해지니 적당히 사용하는 방법을 고민해야다.

