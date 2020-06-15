# DOM의 기본



{% embed url="https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=115186420" %}



## DOM의 기본 파악하기

### 1. 마크업 언어를 사용하는 표준방식 DOM

* DOM
  * Document Object Model
  * 마크업 언어\(html, xml 등\)로 작성된 문서에 액세스하기 위한 표준적인 구조
  * Javascript에 한정하지 않고 현재 주로 사용되는 언어의 대부분에서 지원

### 2. 문서 트리와 노드

* DOM은 문서를 문서 트리로서 취급한다.
* DOM에서는 문서에 포함되는 요소나 속성, 텍스트를 각각 객체로 본다. 때문에 **객체의 집합\(계층관계\)이 문서**라고 생각한다.
* 문서를 구성하는 요소나 속성, 텍스트 등의 객체를 노드라고 부르며, 객체의 종류에 따라 **요소 노드, 속성 노드, 텍스트 노드** 등으로 부른다.
* DOM은 노드를 추출/추가/치환/삭제하기 위한 범용적인 수단을 제공한다.

#### 노드의 종류

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xB178;&#xB4DC;</th>
      <th style="text-align:left">&#xAC1C;&#xC694;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#xB8E8;&#xD2B8; &#xB178;&#xB4DC;</td>
      <td style="text-align:left">&#xD2B8;&#xB9AC;&#xC758; &#xCD5C;&#xC0C1;&#xC704;&#xC5D0; &#xC704;&#xCE58;&#xD558;&#xB294;
        &#xB178;&#xB4DC;, &#xCD5C;&#xC0C1;&#xC704; &#xB178;&#xB4DC; &#xBAA8;&#xB450;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xBD80;&#xBAA8; &#xB178;&#xB4DC; / &#xC790;&#xC2DD; &#xB178;&#xB4DC;</td>
      <td
      style="text-align:left">
        <p>&#xC0C1;&#xD558; &#xAD00;&#xACC4;&#xC5D0; &#xC788;&#xB294; &#xB178;&#xB4DC;,
          &#xC9C1;&#xC811; &#xC5F0;&#xACB0;&#xB418;&#xC5B4; &#xC788;&#xB294; &#xB178;&#xB4DC;&#xC5D0;&#xC11C;
          &#xB8E8;&#xD2B8; &#xB178;&#xB4DC;&#xC5D0; &#xAC00;&#xAE4C;&#xC6B4; &#xB178;&#xB4DC;&#xB97C;
          &#xBD80;&#xBAA8; &#xB178;&#xB4DC;, &#xBA3C; &#xB178;&#xB4DC;&#xB97C; &#xC790;&#xC2DD;
          &#xB178;&#xB4DC;&#xB77C;&#xACE0; &#xBD80;&#xB978;&#xB2E4;.</p>
        <p>(&#xC0C1;&#xD558;&#xAD00;&#xACC4;&#xC5D0; &#xC788;&#xC9C0;&#xB9CC; &#xC9C1;&#xC811;
          &#xBD80;&#xBAA8;-&#xC790;&#xC2DD; &#xAD00;&#xACC4;&#xC544; &#xC544;&#xB2CC;
          &#xAC83;&#xC744; &#xC870;&#xC0C1; &#xB178;&#xB4DC;&#xC640; &#xC190;&#xC790;&#xB178;&#xB4DC;&#xB77C;&#xACE0;
          &#xBD80;&#xB978;&#xB2E4;)</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">&#xD615;&#xC81C; &#xB178;&#xB4DC;</td>
      <td style="text-align:left">&#xB3D9;&#xC77C; &#xBD80;&#xBAA8; &#xB178;&#xB4DC;&#xB97C; &#xAC00;&#xC9C4;
        &#xB178;&#xB4DC;&#xB4E4;. &#xBA3C;&#xC800; &#xC791;&#xC131;&#xB41C; &#xAC83;&#xC744;
        &#xD615; &#xB178;&#xB4DC;, &#xB098;&#xC911;&#xC5D0; &#xC791;&#xC131;&#xB41C;
        &#xAC83;&#xC744; &#xB3D9;&#xC0DD; &#xB178;&#xB4DC;&#xB85C; &#xAD6C;&#xBD84;&#xD558;&#xB294;
        &#xACBD;&#xC6B0;&#xB3C4; &#xC788;&#xB2E4;.</td>
    </tr>
  </tbody>
</table>

{% hint style="info" %}
**DOM에 대한 포스**
{% endhint %}

{% embed url="https://velog.io/@godori/DOM%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80" %}



