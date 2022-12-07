# 3 코드 품질
## 3 - 1 debugging-chrome
[링크참조](https://github.com/endmoseung/ko.javascript.info/blob/master/1-js/03-code-quality/01-debugging-chrome/article.md)
## 3 - 2 coding-style
<img width="792" alt="image" src="https://user-images.githubusercontent.com/103626175/206120870-a7ead049-6084-4ad1-aafc-ebd1d8c094f2.png">
### 함수의 위치
'헬퍼' 함수 여러 개를 만들어 사용하고 있다면 아래와 같은 방법을 사용해 코드 구조를 정돈할 수 있습니다.
```js run
// *!*함수 선언*/!*
function createElement() {
  ...
}

function setHandler(elem) {
  ...
}

function walkAround() {
  ...
}

// *!*헬퍼 함수를 사용하는 코드*/!*
let elem = createElement();
setHandler(elem);
walkAround();
```
## 3 - 3 comments
그러나 좋은 코드엔 '설명이 담긴(explanatory)' 주석이 많아선 안 됩니다. **주석 없이 코드 자체만으로 코드가 무슨 일을 하는지 쉽게 이해할 수 있어야 합니다.**<br>
### 좋은 주석
설명이 담긴 주석은 대개 좋지 않습니다. 그럼 좋은 주석이란 무엇일까요?<br>
아키텍처를 설명하는 주석 : 고차원 수준 컴포넌트 개요, 컴포넌트 간 상호작용에 대한 설명, 상황에 따른 제어 흐름 등은 주석에 넣는 게 좋습니다. 이런 주석은 조감도 역할을 해줍니다. 고차원 수준의 아키텍처 다이어그램을 그리는 데 쓰이는 언어인 UML도 시간을 내어 공부해 보는걸 추천해 드립니다.<br>
함수 용례와 매개변수 정보를 담고 있는 주석 : JSDoc이라는 특별한 문법을 사용하면 함수에 관한 문서를 쉽게 작성할 수 있습니다. 여기엔 함수 용례, 매개변수, 반환 값 정보가 들어갑니다.
* 고차원 수준 아키텍처
* 함수 용례
* 당장 봐선 명확해 보이지 않는 해결 방법에 대한 설명

## 3 - 4 ninja-code
아래 링크처럼 코딩해선 안된다.
[링크참조](https://github.com/endmoseung/ko.javascript.info/blob/master/1-js/03-code-quality/04-ninja-code/article.md)

## 3 - 5 testing-mocha
### 테스트의 필요성
테스트코드가 없다면 개발자들은 수동으로 에러를 테스트한다.하지만 테스트를 수동으로 하면 에러가 발생할 여지를 남깁니다. 그래서 테스트코드를 작성한다.
### Mocha
위에서 테스팅을 하기위해 제시하는 라이브러리가 Mocha다. 우테코에서 JEST를 사용했던것처럼.<br>
요약하면 JEST랑 상당히 비슷하다 describe()를 쓰는게 동일한것처럼.

## 3 = 6 polyfills
자바스크립트는 끊임없이 진화하는 언어입니다. 새로운 제안(proposal)이 정기적으로 등록, 분석되고, 가치가 있다고 판단되는 제안은 https://tc39.github.io/ecma262/에 추가됩니다. 그리고 궁극적으로 명세서(specification)에 등록됩니다.<br>
### 바벨
바벨(Babel)은 트랜스파일러(transpiler)로, 모던 자바스크립트 코드를 구 표준을 준수하는 코드로 바꿔줍니다.




