# 클라이언트 측 JavaScript의 사전 지식

* DOM개발 필수 지식
  * 요소 노드의 취득
  * 문서 트리 간의 왕래
  * 이벤트 구동 모델

### 요소 노드 취득하기

#### ID값을 키값으로 노드 취득하기

* `getElementById`메소드
* 지정된 ID값을 갖는 요소를 Element 객체로서 취득

```javascript
document.getElementById(id)
    id : 취득하고 싶은 요소의 id값
```

> **id값이 중복되는 경우**
>
> id값이 중복되는 요소가 존재하는 경우에도 getElementById 메소드는 처음에 일치하는 요소를 하나만 반환한다. 이 동작은 사용하는 브라우저 및 버전 등의 환경에 따라 변동될 수 있다. 원칙적으로 페이지에서 id값은 고유하게 설정해야 한다.

#### 태그명을 키값으로 노드 취득하기

* `getElementsByTagName` 메소드
* 태그명을 키로 하여 요소를 취득

```text
document.getElementsByTagName(name)
    name : 태그명
```

* getElementsByTagName\` 의 반환값은 **HTMLCollection객체** \(요소의 집합\)
* 인수 name에 '\*'를 지정하여 모든 요소 검색 가능

| 멤버 | 개요 |
| :--- | :--- |
| length | 리스트에 포함되는 요소의 수 |
| item\(i\) | i번째의 노드를 취득\(i는 0~length-1의 범위\) |
| namedItem\(name\) | id 또는 name 속성이 일치하는 요소를 취득 \(같은 여러개일 경우 처음에 일치하는 하나\) |

> **HTMLCollection 객체의 대괄호 구문**
>
> item/namedItem 메소드는 대괄호 구문으로 대체할 수도 있다.

{% hint style="info" %}
의문 : namedItem 은 어떻게 대괄호 구문으로 대체하는지...?
{% endhint %}

#### name 속성을 키로 요소 취득하기

* `getElementsByName` 메소드

일반적으로 폼 요소에서의 엑세스에 이용

* 하지만 하나의 요소를 취득하려고 한다면 오히려 getElementById 메소드가 코드가 간단함
* 라디오 버튼/체크박스 등 name 속성이 동일한 요소군들을 얻을 경우로 한정

```text
document.getElementsByName(name)
    name: name 속성의 값
```

* 반환값이 노드의 집합 \(NodeList객체\)

> **NodeList 객체**
>
> NodeList객체는 노드의 리스트를 나타내기 위함 객체다. HTMLCollection 객체와는 우선 거의 동일한 것으로 파악해도 상관 없다. 사용할 소 있는 멤버도 거의 같지만, NodeList 객체에서는 namedItem 메소드를 사용할 수 없다.

{% embed url="https://codepen.io/danbi-lee/pen/RwWpRdM?editors=1011" %}



