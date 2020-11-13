# Styled-components

## Styled-components

* Tagged Template Literal

  > ```javascript
  > const red = '빨간색';
  > const blue = '파란색';
  > ​
  > function favoriteColors(texts, ...values) {
  >     console.log(texts);
  >     console.log(values);
  > }
  > ​
  > favoriteColors`제가 좋아하는 색은 ${red}과 ${blue}입니다.`;
  > ​
  > //(3) ["제가 좋아하는 색은 ", "과 ", "입니다.", raw: Array(3)]
  > //(2) ["빨간색", "파란색"]
  > ```
  >
  > * 값들이 분리된 후, 괄호를 쓴 것처럼 된다.

* styled-components 쓸 때 자동완성쓰는 방법
  * 마켓플레이스에서 vscode-styled-components 다운받으면 됨

{% embed url="https://codesandbox.io/s/styling-with-styled-components-tk3fs?file=/src/App.js" %}



