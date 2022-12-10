<br />
<h1 align="center">1-03 코드 품질</h1>
<br />

> 코딩 관례(coding practice)

## 1. Chrome으로 디버깅하기

> 디버깅(debugging) : 스크립트 내 에러를 검출해 제거하는 일련의 과정

- Sources 패널 → 토글 버튼 눌러 navigator
  - 파일 탐색 영역 : 페이지를 구성하는 데 쓰인 모든 리소스(HTML, JavaScript, CSS, 이미지 파일 등)를 트리 형태로 보여준다 (Chrome 익스텐션이 표시될 때도 있다)
  - 코드 에디터 영역 : 리소스 영역에서 선택한 파일의 소스 코드 (소스 코드 편집 가능)
  - 자바스크립트 디버깅 영역 : 디버깅에 관련된 기능을 제공
- 콘솔 : 명령어 입력해서 실행
- 중단점(breakpoint) : 실행이 중지된 시점에 변수가 어떤 값을 담고 있는지 알 수 있고, 실행이 중지된 시점을 기준으로 명령어를 실행할 수 있다
  - 조건부 중단점(conditional breakpoint) : 변수에 특정 값이 할당될 때나 함수의 매개 변수에 특정 값이 들어올 때만 실행을 중단시킬 수 있어 유용
    - 줄 번호에서 마우스 오른쪽 버튼을 클릭해 `Add conditional breakpoint`를 눌러 뜨는 작은 창에 표현식을 입력하면, 표현식이 참인 경우에만 실행을 중지
- debugger 명령어
  ```js
  function hello(name) {
    let phrase = `Hello, ${name}!`;
    debugger;  // 여기서 실행이 멈추고 중단점 설정과 동일한 효과
    say(phrase);
  }
  ```
- 멈추면 보이는 것들
  - 디버깅 패널
    - Watch : 표현식을 평가하고 결과를 보여준다
      - Add Expression 버튼 +를 클릭해 원하는 표현식을 입력한 후 Enter를 누르면 중단 시점의 값을 보여준다. 입력한 표현식은 실행 과정 중에 계속해서 재평가된다
    - Call Stack : 코드를 해당 중단점으로 안내한 실행 경로를 역순으로 표시
      - 실행은 index.html 안에서 hello()를 호출하는 과정 중에 멈춘다. 함수 hello 내에 중단점을 설정했기 때문에, 콜 스택(Call Stack) 최상단엔 hello가 위치한다. index.html에서 함수 hello를 정의하지 않았기 때문에 콜 스택 하단엔 'anonymous’가 출력된다
      - 콜 스택 내의 항목을 클릭하면 디버거가 해당 코드로 휙 움직이고, 변수 역시 재평가된다
    - Scope : 현재 정의된 모든 변수 출력
      - Local : 함수의 지역변수
      - Global : 전역 변수
- 실행 추적하기
  - Resume : 스크립트 실행을 다시 시작(F8)
  - Step : 다음 명령어를 실행(F9)
    - 비동기 동작은 무시
  - Step over : 다음 명령어를 실행하되, 함수 안으로 들어가진 않음(F10)
  - Step into : 비동기 동작을 담당하는 코드로 진입하고, 필요하다면 비동기 동작이 완료될 때까지 대기(F11)
  - Step out: 실행 중인 함수의 실행이 끝날 때 까지 실행을 계속(Shift+F11)
    - 실수로 Step을 눌러 내부 동작이 궁금하지 않은 중첩함수로 진입했거나 빨리 함수 실행 끝내고 싶을 때
  - 모든 중단점을 활성화/비활성화
  - 예외 발생 시 코드를 자동 중지시켜주는 기능을 활성화/비활성화
  - Continue to here 옵션 : 중단점을 설정하기는 귀찮은데 해당 줄에서 실행을 재개하고 싶을 때 사용(줄에서 마우스 오른쪽 버튼 클릭)
- console.log과 디버거를 적절히 활용할 것
- 스크립트 실행이 중단되는 경우
  - 중단점을 만났을 때
  - debugger문 만났을 때
  - 에러가 발생했을 때(개발자 도구가 열려있고 예외 발생 시 코드를 자동 중지시켜주는 기능 버튼이 활성화되어있는 경우)

<br />

## 2. 코딩 스타일

> 코드는 가능한 간결하고 읽기 쉽게 짜야 한다

### 코딩 스타일

- 중첩 레벨은 최소화
- 함수의 위치
  - 함수 선언 후 해당 함수 사용하는 코드
  - 함수 사용하는 코드 후 해당 함수 선언 → 보통 선호
```js
function pow(x, n) { // 여는 중괄호 앞엔 공백 하나
  let result = 1; // 들여쓰기는 탭 대신 스페이스로 해야 유연하게 가능

  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result; // 모든 구문의 끝에는 세미콜론
}
// 논리 블록 사이에 넣어 코드를 분리하여 코드 가독성 높이기
let x = prompt("x?", "");
let n = prompt("n?", "");

if (n <= 0) {
  alert(`Power ${n} is not supported,
    please enter an integer number greater than zero`); // 가로가 갈면 여러 줄에 나눠서 작성
} else {
  alert( pow(x, n) );
}
```

### 스타일 가이드

- 코드를 어떻게 작성할지 전반적인 규칙 담은 문서
- [Google의 자바스크립트 스타일 가이드](https://google.github.io/styleguide/jsguide.html)
- [Airbnb의 자바스크립트 스타일 가이드](https://github.com/airbnb/javascript)
- [Idiomatic.JS](https://github.com/rwaldron/idiomatic.js)
- [StandardJS](https://standardjs.com/)

### Linter

- 작성한 코드가 스타일 가이드를 준수하고 있는지를 자동으로 확인 가능 및 스타일 개선과 관련된 제안
- [JSLint](https://www.jslint.com/) : 역사가 오래된 linter
- [JSHint](https://jshint.com/) : JSLint보다 유연한 linter
- [ESLint](https://eslint.org/) : 가장 최근에 나온 linter

<br />

## 3. 주석

> 주석(comment) : 어떻게 코드가 동작하는지, 왜 코드가 동작하는지 설명

- 설명이 담긴(explanatory) 주석이 많아서는 안 된다. 주석 없이 코드 자체만으로 설명할 수 있어야 한다
- 리팩터링 팁 : 함수 분리하기/만들기
- 좋은 주석
  - 고차원 수준 아키텍처(아키텍처를 설명하는 주석)
    - 고차원 수준 컴포넌트 개요, 컴포넌트 간 상호작용에 대한 설명, 상황에 따른 제어 흐름 등
    - UML
  - 함수 용례와 매개변수 정보를 담고 있는 주석 : JSDoc
  - 당장 봐선 명확해 보이지 않는 해결 방법에 대한 설명
    - 왜 이런 방법으로 문제를 해결했는지를 설명하는 주석
      - 문제 해결 방법이 여러가지인데 왜 하필 이 해결책을 택했는지 적어놓으면 이후 불필요하게 코드를 수정하는 일을 줄일 수 있다
    - 미묘한 기능이 있고, 이 기능이 어디에 쓰이는지를 설명하는 주석
- 불필요한 주석
  - 코드가 어떻게 동작하는지, 코드가 무엇을 하는지
- 코드를 간결하게 짤 수 없는 상황이나 코드 자체만으로 무슨 일을 하는지 판단하기 어려울 때만 주석을 작성할 것

<br />

## 4. 닌자 코드

> 유지보수 담당 개발자를 혹독하게 훈련하고자 사용한 편법

- 코드 짧게 쓰기
- 글자 하나만 쓰기 (a, b, c)
- 약어 사용하기 (list → lst)
- 포괄적인 명사 사용하기 (data, str, num)
- 철자가 유사한 단어 사용하기 (data와 date)
- 동의어 사용하기 (프린터 사용하는 함수는 printPage를 화면에 문자 출력하는 함수는 printText)
- 이름 재사용하기
  - 새로운 값을 저장할 때 기존 변수를 활용
  ```js
  function ninjaFunction(elem) {
    // 매개변수로 받아온 elem을 이용한 코드
    elem = clone(elem);
    // elem의 복제(clone)본을 이용한 코드
  }
  ```
- 재미로 언더스코어 사용하기
- 과장 형용사 사용하기 (super)
- 외부 변수 덮어쓰기
  ```js
  let user = authenticateUser();
  function render() {
    let user = anotherValue();
  }
  ```
- 부작용이 있는 코드 작성하기
  - 유용한 기능을 추가하기 (is..., check... 함수에 무언가를 바꾸는 기능 추가)
  - 예상치 않은 결과 반환 (check... 함수가 불리언 값이 아닌 다른 값을 반환)
- 함수에 다양한 기능 넣기 (코드 재사용 방지)

<br />

## 5. 테스트 자동화와 Mocha

### 테스트는 왜 해야 하는가?

- 코드를 수동으로 재실행하면서 테스트를 하면 무언가 놓칠 수 있다
- 테스팅 자동화는 테스트 코드가 실제 동작에 관여하는 코드와 별개로 작성되었을 때 가능. 테스트 코드를 이용하면 함수를 다양한 조건에서 실행해 볼 수 있는데, 이때 실행 결과와 기대 결과를 비교 가능

### Behavior Driven Development

- BDD는 테스트(test), 문서(documentation), 예시(example)를 한데 모아놓은 개념
- 거듭제곱 함수와 명세서
  ```js
  describe("pow", function() {
  // 구현하고자 하는 기능에 대한 설명
    it("주어진 숫자의 n 제곱", function() {
      // 첫번째 인수에는 특정 유스케이스에 대한 설명, 두번째 인수에는 유스케이스 테스트 함수
      assert.equal(pow(2, 3), 8);
      // 기능을 제대로 구현했다면 에러 없이 실행
    });
  });
  ```

### 개발 순서 
  - 반복적인(iterative) 성격
  1. 명세서 초안 작성 (기본적 테스트 포함)
  2. 명세서 초안을 보고 코드 작성
  3. Mocha 테스트 프레임워크 이용해 명세서 실행. 테스트를 모두 통과해 에러가 출력되지 않을 때까지 수정
  4. 모든 테스트 통과하는 코드 초안 완성
  5. 유스케이스 추가. 실패하는 테스트케이스 생길 것
  6. 다시 코드 수정
  7. 3~6 반복

### 스펙 실행하기, 코드 초안, 스팩 개선하기, 중첩 describe, 스펙 확장하기
- 라이브러리 : 브라우저나 서버 사이드 환경 모두 가리지 않고 사용 가능
  - Mocha : 핵심 테스트 프레임워크로, describe, it과 같은 테스팅 함수와 테스트 실행 관련 주요 함수를 제공
  - Chai : 다양한 assertion을 제공해 주는 라이브러리
  - Sinon : 함수의 정보를 캐내는 데 사용되는 라이브러리로, 내장 함수 등을 모방
```html
<!DOCTYPE html>
<html>
<head>
  <!-- 결과 출력에 사용되는 mocha css를 불러옵니다. -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.css">
  <!-- Mocha 프레임워크 코드를 불러옵니다. -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.js"></script>
  <script>
    mocha.setup('bdd'); // 기본 셋업
  </script>
  <!-- chai를 불러옵니다 -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/chai/3.5.0/chai.js"></script>
  <script>
    // chai의 다양한 기능 중, assert를 전역에 선언합니다.
    let assert = chai.assert;
  </script>
</head>

<body>
  <script>
    function pow(x, n) {
      if (n < 0) return NaN;
      if (Math.round(n) != n) return NaN;

      let result = 1;
      for (let i = 0; i < n; i++) {
        result *= x;
      }
      return result;
    }
  </script>

  <!-- 테스트(describe, it...)가 있는 스크립트를 불러옵니다. -->
  <script src="test.js"></script>

  <!-- 테스트 결과를 id가 "mocha"인 요소에 출력하도록 합니다.-->
  <div id="mocha"></div>

  <!-- 테스트를 실행합니다! -->
  <script>
    mocha.run();
  </script>
</body>
</html>
```
```js
// test.js
// 기존 it 블록에 assert를 하나 더 추가하기
describe("pow", function() {
  it("주어진 숫자의 n 제곱", function() {
    assert.equal(pow(2, 3), 8); // 이 assert가 실패하면 즉시 종료돠어 아래 결과를 알 수 없다
    assert.equal(pow(3, 4), 81);
  });
});

// 테스트를 하나 더 추가하기(it 블록 하나 더 추가하기) (권장 방식)
describe("pow", function() {
  it("2를 세 번 곱하면 8입니다.", function() {
    assert.equal(pow(2, 3), 8);
  });
  it("3을 네 번 곱하면 81입니다.", function() {
    assert.equal(pow(3, 4), 81);
  });

  it("n이 음수일 때 결과는 NaN입니다.", function() {
    assert.isNaN(pow(2, -1));
  });
  it("n이 정수가 아닐 때 결과는 NaN입니다.", function() {
    assert.isNaN(pow(2, 1.5));
  });
});
```
```js
// test.js
describe("pow", function() {
  function makeTest(x) {
    let expected = x * x * x;
    it(`${x}을/를 세 번 곱하면 ${expected}입니다.`, function() {
      assert.equal(pow(x, 3), expected);
    });
  }
  for (let x = 1; x <= 5; x++) {
    makeTest(x);
  }
});
```
```js
// test.js
describe("pow", function() {
  describe("x를 세 번 곱합니다.", function() {
    function makeTest(x) {
      let expected = x * x * x;
      it(`${x}을/를 세 번 곱하면 ${expected}입니다.`, function() {
        assert.equal(pow(x, 3), expected);
      });
    }
    for (let x = 1; x <= 5; x++) {
      makeTest(x);
    }
  });
  // describe와 it을 사용해 이 아래에 테스트 추가
});
```
- karma와 같은 고수준의 테스트 러너(test-runner)를 활용하면 다양한 종류의 테스트 자동 실행 가능
- 테스트 하나에선 한 가지만 확인하기
- before/after와 beforeEach/afterEach
  - before는 (전체) 테스트가 실행되기 전에 실행되고, after는 (전체) 테스트가 실행된 후에 실행
  - beforeEach는 매 it이 실행되기 전에 실행되고, afterEach는 매 it이 실행된 후에 실행
  ```js
  describe("test", function() {
    before(() => alert("테스트를 시작합니다 - 테스트가 시작되기 전"));
    after(() => alert("테스트를 종료합니다 - 테스트가 종료된 후"));

    beforeEach(() => alert("단일 테스트를 시작합니다 - 각 테스트 시작 전"));
    afterEach(() => alert("단일 테스트를 종료합니다 - 각 테스트 종료 후"));

    it('test 1', () => alert(1));
    it('test 2', () => alert(2));
  });
  ```

### 요약

- BDD에선 스펙을 먼저 작성하고 난 후에 구현을 시작. 구현이 종료된 시점에는 스펙과 코드 둘 다를 확보 가능
- 스펙의 용도
  - 테스트 : 함수가 의도하는 동작을 제대로 수행하고 있는지 보장
  - 문서 : 함수가 어떤 동작을 수행하고 있는지 설명 (describe와 it에 설명 작성)
  - 예시 : 실제 동작하는 예시를 이용해 함수를 어떻게 사용할 수 있는지 알려줌
- 테스팅 자동화를 수행하고 있는 프로젝트라면 코드 수정했을 때 생길 수 있는 추가적인 에러를 걱정하지 않아도 된다. 코드에 변화가 있어도 스펙을 실행해 테스트를 진행하면 몇 초 만에 에러 발생 여부를 확인할 수 있다
- 잘 테스트 된 코드는 더 나은 아키텍처를 만든다

### 과제
```js
// 올바르지 않은 코드. 사실상 하나의 테스트 함수이며, 에러가 발생해도 원인을 찾기 어렵다
it("주어진 숫자의 n 제곱", function() {
  let x = 5;

  let result = x;
  assert.equal(pow(x, 1), result);

  result *= x;
  assert.equal(pow(x, 2), result);

  result *= x;
  assert.equal(pow(x, 3), result);
});

// 테스트는 아래처럼 명확한 입력값, 출력값과 함께 여러 개의 it 블록으로 쪼개 작성해야 한다
describe("주어진 숫자의 n 제곱", function() {
  it("5를 1 제곱하면 5", function() {
    assert.equal(pow(5, 1), 5);
  });

  // Mocha는 아래 블록만 실행할 수 있다
  it.only("5를 2 제곱하면 25", function() {
    assert.equal(pow(5, 2), 25);
  });

  it("5를 3 제곱하면 125", function() {
    assert.equal(pow(5, 3), 125);
  });
});
```

<br />

## 6. 폴리필

> 자바스크립트 엔진은 표준 전체를 지원하지 않는다

- 바벨(Babel) : 트랜스파일러(transpiler)로, 모던 자바스크립트 코드를 구 표준을 준수하는 코드로 변경
- 역할
  - 트랜스파일러 : 코드를 재작성. 바벨을 실행하면 기존 코드가 구 표준을 준수하는 코드로 변경되고, 변경된 코드는 웹사이트 형태로 사용자에게 전달된다
    - 웹팩(webpack)과 같은 모던 프로젝트 빌드 시스템은 코드가 수정될 때마다 자동으로 트랜스파일러를 동작
  - 폴리필 : 변경된 표준을 준수할 수 있게 기존 함수의 동작 방식을 수정하거나, 새롭게 구현한 함수의 스크립트
    - core js : 다양한 폴리필을 제공(특정 기능의 폴리필만 사용하는 것도 가능)
    - polyfill.io : 기능이나 사용자의 브라우저에 따라 폴리필 스크립트를 제공해주는 서비스
- 트랜스파일러 없이 최신 기능을 사용할 수 있기 때문에 Chrome은 데모용으로 사용하기 좋다

<br />
<br />
