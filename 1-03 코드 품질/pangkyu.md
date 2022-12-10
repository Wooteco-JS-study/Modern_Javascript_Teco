
### ch1 : debugging

> 디버깅(debugging) : 스크립트 내 에러를 검출해 제거하는 일련의 과정

##### 중단점(break point)

- 자바스크립트의 실행이 중단되는 코드 내 지점
- 중단점을 이용하면 실행이 중지된 시점에 변수가 어떤 값을 담고 있는지 알 수 있다.
- 실행이 중지된 시점을 기준으로 명령어를 실행할 수 있다.
  - 조건부 중단점 : 표현식이 참인 경우에만 실행을 중지시킬 수 있다. 조건부 중단점을 설정하면 변수에 특정 값이 할당될 때나 함수 매개변수에 특정 값이 들어올 때만 실행을 중단시킬 수 있다.
- <code>debugger</code>명령어를 적어주면 중단점을 설정한 것과 같은 효과

```js
function hello(name) {
  let phrase = `hi, ${name}!`;

  debugger;
  say(phrase);
}
```

##### 디버깅 영역의 하위 패널

1. watch : 표현식을 평가하고 결과를 보여준다.

   - 중단 시점의 값을 보여준다. 입력한 표현식은 실행 과정 중에 계속해서 재평가된다.

2. call stack : 코드를 해당 중단점으로 안내한 실행 경로를 역순으로 표시
3. scope : 현재 정의된 모든 변수를 출력한다.
   - local : 함수의 지역변수
   - global : 함수 바깥에 정의된 전역 변수

##### console.log

- 코드에 console.log를 적절히 넣으면 디버거 없이도 무슨 일이 일어나고 있는지 충분히 파악 가능하다.

### ch2 : 코딩 스타일

> 개발자는 가능한 간결하고 읽기 쉬운 코드를 작성해야한다.

##### 중괄호

- 대부분의 자바스크립트 프로젝트에서 여는 중괄호는 이집션(Egyptian)스타일을 따라 새로운 줄이 나니 상응하는 키워드와 같은 줄에 작성.
- 여는 중괄호 앞에는 공백이 하나 있어야한다.

```js
if (condition) {
  // code
}
```

- 코드가 짧다면 중괄호 없이 한 줄에 쓰는 방법도 괜찮다.

```js
if (n < 0) console.log('n은 0보다 작다);
```

##### 가로 길이

- 코드의 가로 길이가 길어진다면 여러 줄로 나누어 작성하는 게 좋다.
- 최대 가로 길이는 팀원들과 합의. 대개 80~120자로 제한한다.

```js
// 백틱(`)을 사용하면 문자열을 여러 줄로 쉽게 나눌 수 있습니다.
let str = `
  ECMA International's TC39 is a group of JavaScript developers,
  implementers, academics, and more, collaborating with the community
  to maintain and evolve the definition of JavaScript.
`;

if (id === 123 && moonPhase === "Waning Gibbous" && zodiacSign === "Libra") {
  letTheSorceryBegin();
}
```

##### 들여쓰기

1. 가로 들여쓰기 : 스페이스 두 개 혹은 네 개를 사용해 만듦
   - 혹은 탭 키를 이용하여 만들 수 있다.
   - 탭 대신 스페이스를 이용했을 때의 장점 중 하나는 들여쓰기 정도를 좀 더 유연하게 변경할 수 있다.

```js
show(parameters,
     aligned,
     one,
     after,
     another){
    //...
}
```

2. 세로 들여쓰기 : 논리 블록 사이에 넣어 코드를 분리해주는 새 줄
   - 함수 하나에 논리 블록 여러개가 들어갈 수 있다.
   - 변수 선언, 반복문, 리턴문 사이에 세로 들여쓰기를 해주는 빈 줄을 넣어 코드를 분리

```js
function pow(x, n) {
  let result = 1;
  //
  for (let i = 0; i < n; i++) {
    result *= x;
  }
  //
  return result;
}
```

##### 세미콜론

- 모든 구문의 끝에는 세미콜론을 써주는 것이 좋다.

##### 중첩 레벨

- 가능한 너무 깊은 중첩문은 지양하자
- 반복문을 사용할 때 중첩문의 깊이가 깊어지면 <code>continue</code> 지시자를 쓰는 것이 좋은 대안이 될 수 있다.

```js
for (let i = 0; i < 10; i++) {
  if (cond) {
    //...
  }
}

for (let i = 0; i < 10; i++) {
  if (!cond) continue;
}
```

##### 함수의 위치

- '헬퍼'함수 여러 개를 만들어 사용하고 있다면 아래 처럼 코드 구졸르 정돈할 수 있다.

1. 헬퍼 함수를 사용하는 코드 위에서 헬퍼 함수를 모아 선언

```js
function createElement() {
  //...
}

function setHandler(elem) {
  //...
}

function walkAround() {
  //...
}

let elem = createElement();
setHandler(elem);
walkAround();
```

2. 코드를 먼저, 함수는 그 다음에

```js
let elem = createElement();
setHandler(elem);
walkAround();

function createElement() {
  //...
}

function setHandler(elem) {
  //...
}

function walkAround() {
  //...
}
```

3. 혼합 : 코드 바로 위에서 필요한 헬퍼 함수 그때마다 선언하기

- 대개 두번째 방법으로 코드를 정돈하는 것을 선호
  - 사람들이 코드가 무엇을 하는지를 생각하며 코드를 읽기때문에 코드가 먼저나오는 것이 자연스럽기 때문

##### 스타일 가이드

- 코드를 어떻게 작성할지에 대한 전반적인 규칙을 담은 문서
- 팀원 전체가 동일한 스타일 가이드로 코드 작성을 하면, 누가 코드를 작성했나에 관계없이 동일한 스타일의 코드를 만들 수 있다.
- 구글 자바스크립트 스타일 가이드, 에어비앤비 자바스크립트 스타일 가이드 등등

##### Linter

- 이 도구를 사용하면 내가 작성한 코드가 스타일 가이드를 준수하고 있는지 자동으로 확인하고, 스타일 개선과 관련된 제안을 받을 수 있다.
- JSLint, ESLint 등등


### ch3 : 주석

> 어떻게 코드가 동작하는지, 왜 코드가 동작하는지를 설명하는 데 쓰인다

- 한 줄 짜리 주석 : <code>//</code>
- 여러 줄짜리 주석 : <code>/_ ... _/</code>
- 주석 없이 코드 자체만으로 코드가 무슨일을 하는지(self-descriptive) 쉽게 이해할 수 있어야 한다.(설명이 담긴 주석이 많으면 안된다. )

##### 좋은 주석

- 아키텍처를 설명하는 주석 : 고차원 수준 컴포넌트 개요, 컴포넌트 간 상호작용에 대한 설명, 상황에 따른 제어 흐름 등은 주석에 넣는 것이 좋다.
- 함수 용례와 매개변수 정보를 담고 있는 주석 : [JSDoc](https://en.wikipedia.org/wiki/JSDoc)라는 특별한 문법을 사용하면 함수에 관한 문서를 쉽게 작성할 수 있다.

```js
/**
 * x를 n번 곱한 수를 반환함
 *
 * @param {number} x 거듭제곱할 숫자
 * @param {number} n 곱할 횟수, 반드시 자연수여야 함
 * @return {number} x의 n 거듭제곱을 반환함
 */
function pow(x, n) {
  ...
}
```

- 왜 이런 방법으로 문제를 해결했는지를 설명하는 주석 : 당장 봐서는 명확해 보이지 않는 해결 방법에 대한 설명
- 미묘한 기능이 있고, 이 기능이 어디에 쓰이는 지를 설명하는 주석 : 직감에 반하는 미묘한 동작을 수행하는 코드가 있으면 달아주는 것이 좋다.

### ch4 : 닌자 코드

> 아래대로 하면 절.대 안된다 반대로만 하자!

##### 코드 짧게 쓰기

```js
i = i ? (i < 0 ? Math.max(0, len + i) : i) : 0;
```

##### 글자 하나만 사용하기

- 글자 하나만 사용하여 변수 이름을 짓기(<code>a</code>, <code>b</code> 등)
- 변수 이름이 짧아지면 변수를 찾기 힘들고 무엇을 의미하는지 해석하기 힘들다.

##### 약어 사용하기

- <code>list</code> -> <code>lst</code>
- <code>userAgent</code> -> <code>ua</code> 등등

##### 포괄적인 명사 사용하기

- <code>obj</code>, <code>data</code>, <code>elem</code>같이 다양한 개념을 포괄할 수 있는 명사를 사용
- 새로운 변수명이 더는 떠오르지 않으면? <code>data1, elem5</code>처럼 숫자 붙이기

##### 철자가 유사한 단어 사용

- ex) <code>date</code>, <code>data</code>같이 유사한 철자를 가진 단어를 조합해 사용

##### 동의어 사용하기

- 유사한 뜻을 가진 단어를 사용

##### 이름 재사용하기

- 새로운 값을 저장할 때, 기존 변수를 활용하면 변수선언을 최대한 피한다.
- 함수를 구현 중이라면 내부 변수를 선언하지 않고, 매개변수에서 넘어온 값만 사용

```js
// ex
function ninjaFunction(elem) {
  //매개변수로 받아온 elem을 이용한 코드
  elem = clone(elem);
  // elem의 복제본을 이용한 코드
}
```

##### 재미로 언더스코어 사용하기

- <code>\_name</code>과 같은 것으로 작성자만 언더스코어가 무엇을 의미를 알고, 장난식으로 붙이거나 의미를 계속 바꿔가며 붙인다.

##### 과장 형용사 사용

- 개체 앞에 적절한 형용사를 붙여 해당 개체가 얼마나 멋있는지 자랑하자

##### 외부 변수 덮어쓰기

- 함수 내부와 외부에 동일한 이름을 가진 변수를 선언하여 사용하면 이름 짓는 데 골머리 썩이지 않는다

##### 부작용이 있는 코드 작성하기

- <code>isReady()</code>, <code>findTags()</code>같은 함수에 무언가를 바꿀 수 있는 기능 혹은 예상하지 않은 결과를 반환하기

##### 함수에 다양한 기능 넣기

- 함수가 할 수 있는 동작을 이름에 한정 짓지 않고 만들기
- 함수 하나에 여러 기능을 넣으면 코드 재사용도 방지한다.

### ch5 : 테스트 자동화와 mocha

> 테스팅 자동화는 테스트 코드가 실제 동작에 관여하는 코드와 별개로 작성되었을 때 가능하다. 테스트 코드를 이용하면 함수를 다양한 조건에서 실행해 볼 수 있는데, 이때 실행 결과와 기대 결과를 비교할 수 있다.

- 코드를 수동으로 재실행하면서 테스트를 하면 무언가 놓치기 쉽다.

##### Behavior Driven Development(BDD)

- BDD는 테스트(test), 문서(documentation), 예시(example)를 한데 모아놓은 개념
- BDD에서는 스펙을 먼저 작성한 뒤에 구현을 시작한다. 구현이 종료된 시점에는 스펙과 코드 둘 다 확보할 수 있다.

##### 거듭제곱 함수와 명세서

- 만들어진 산출물을 BDD에서 명세서(specification)또는 짧게 줄여 스펙(spec)이라고 부른다. 명세서에는 아래와 같이 유스 케이스에 대한 자세한 설명과 테스트가 담겨있다.

```js
describe("pow", function () {
  it("주어진 숫자의 n 제곱", function () {
    assert.equal(pow(2, 3), 8);
  });
});
```

- <code>describe('title', function() {...})</code> : 구현하고자 하는 기능에 대한 설명. <code>it</code>블록을 한데 모아주는 역할도 한다.
- <code>it('유스 케이스 설명', function(){...})</code> : <code>it</code>의 첫 번째 인수에는 특정 유스 케이스에 대한 설명이 들어간다. **누구나 읽을 수 있고 이해할 수 있는 자연어**로 적는다. 두 번째 인수에는 유즈케이스 테스트 함수가 들어간다.
- <code>assert.equal(value1, value2)</code> : 기능을 제대로 구현했다면 <code>it</code>블록 내의 코드가 에러 없이 실행된다.

##### 개발 순서

1. 명세서 초안 작성. 초안에는 기본적인 테스트도 들어간다.
2. 명세서 초안을 보고 코드 작성
3. 코드가 작동하는지 확인하기 위해 테스트 프레임워크를 사용하여 명세서를 실행. 이때, 코드가 잘못 작성되었으면 에러가 출력된다. 개발자는 테스트를 모두 통과해 에러가 더는 출력되지 않을 때까지 코드를 수정한다.
4. 모든 테스트를 통과하는 코드 초안이 완성된다.
5. 명세서에 지금까지 고려하지 않았던 유스케이스 몇 가지를 추가한다. (테스트가 실패하기 시작)
6. 3번으로 돌아가 테스트를 모두 통과할 때까지 코드를 수정
7. 기능이 완성될 때까지 3~6단계를 반복

##### 스펙 실행하기

- Mocha : 핵심 테스트 프레임워크, <code>describe</code>, <code>it</code>같은 테스팅 함수와 테스트 실행 관련 주요 함수를 제공
- Chai : 다양한 assertion을 제공하는 라이브러리
- Sinon : 함수의 정보를 캐내는 데 사용되는 라이브러리, 내장 함수 등을 모방한다.

##### 코드 초안

- 오로지 테스트 통과만을 목적

```js
function pow(x, n) {
  return 8;
}
```

##### 스펙 개선하기

- 스펙에 테스트를 추가하는 방법은 2가지가 있다.

1. 기존 <code>it</code>블록에 <code>assert</code>를 하나 더 추가

```js
describe("pow", function () {
  it("주어진 숫자의 n 제곱", function () {
    assert.equal(pow(2, 3), 8);
    assert.equal(pow(3, 4), 81);
  });
});
```

2. 테스트를 하나 더 추가하기(<code>it</code>블록 하나 더 추가)

```js
describe("pow", function () {
  it("2를 세번 곱하면 8이다.", function () {
    assert.equal(pow(2, 3), 8);
  });
  it("3을 네번 곱하면 81이다.", function () {
    assert.equal(pow(3, 4), 81);
  });
});
```

- <code>assert</code>에서 에러가 발생하면 <code>it</code>블록은 즉시 종료
  - 기존 <code>it</code>블록에 <code>assert</code>를 하나 더 추가하면 첫 번째 <code>assert</code>가 실패했을 때 두 번째 <code>assert</code>의 결과를 알 수 없다.
- 두 번째 처럼 <code>it</code>블록을 추가하여 테스트를 분리 작성하는 것을 추천
- **테스트 하나에선 한 가지만 확인**

##### 코드 개선하기

- 실제 우리가 구현하려는 기능을 생각하며 작성

```js
function pow(x, n) {
  let result = 1;
  for (let i = 0; i < n; i++) {
    result *= x;
  }
  return result;
}
```

- 함수가 제대로 작동하는지 확인하기 위해 더 많은 값을 테스트

```js
describe("pow", function () {
  function makeTest(x) {
    let expected = x * x * x;
    it(`${x}를 세 번 곱하면 ${expected}입니다.`, function () {
      assert.equal(pow(x, 3), expected);
    });
  }
  for (let x = 1; x <= 5; x++) {
    makeTest(x);
  }
});
```

##### 중첩 describe

- 새로운 테스트 하위그룹(subgroup)을 정의할 때 사용된다.
- 중첩 describe를 쓰면 그룹을 만들 수 있다.

```js
describe("pow", function () {
  describe("x를 세 번 곱합니다.", function () {
    function makeTest(x) {
      let expected = x * x * x;
      it(`${x}을/를 세 번 곱하면 ${expected}입니다.`, function () {
        assert.equal(pow(x, 3), expected);
      });
    }

    for (let x = 1; x <= 5; x++) {
      makeTest(x);
    }
  });

  // describe와 it을 사용해 이 아래에 더 많은 테스트를 추가할 수 있습니다.
});
```

```js
describe("test", function () {
  before(() => alert("테스트를 시작합니다 - 테스트가 시작되기 전"));
  after(() => alert("테스트를 종료합니다 - 테스트가 종료된 후"));

  beforeEach(() => alert("단일 테스트를 시작합니다 - 각 테스트 시작 전"));
  afterEach(() => alert("단일 테스트를 종료합니다 - 각 테스트 종료 후"));

  it("test 1", () => alert(1));
  it("test 2", () => alert(2));
});
```

- <code>beforeEach/afterEach</code>와 <code>before/after</code>는 대개 초기화 용도로 사용된다. 카운터 변수를 0으로 만들거나 테스트가 바뀔 때(또는 테스트 그룹이 바뀔 때)마다 해줘야 하는 작업이 있으면 이들을 이용할 수 있다.

```js
assert.equal(value1, value2); // value1과 value2의 동등성을 확인(value1 == value2)
assert.strictEqual(value1, value2); // value1과 value2의 일치성을 확인(value1 === value2)
assert.notEqual, assert.notStrictEqual; // 비 동등성, 비 일치성을 확인
assert.isTrue(value); // value가 true인지 확인
assert.isFalse(value); // value가 false인지 확인
// 그 외 다양한 assertion이 있다.  http://chaijs.com/api/assert/
```

### ch6 : 폴리필

- 자바스크립트는 끊임없이 진화하는 언어.
- 엔진별로 어떤 기능을 지원하는지는 https://kangax.github.io/compat-table/es6/ 에서 확인

##### 바벨(Babel)

- 바벨은 트랜스파일러로 모던 자바스크립트 코드를 구 표준을 준수하는 코드로 바꿔준다.
- 주요역할
  - 트랜스파일러(transpiler) : 바벨은 코드를 재작성해주는 트랜스파일러 프로그램. 이를 실행하면 기존 코드가 구 표준을 준수하는 코드로 변경되는데, 이 코든느 웹사이트 형태로 사용자에게 전달된다. 웹팩과 같은 모던 프로젝트 빌드 시스템은 코드가 수정될 때마다 자동으로 트랜스파일러를 동작시킨다.
  - 폴리필 : 명세서에는 새로운 문법이나 기존에 없던 내장 함수에 대한 정의가 추가된다. 새로운 문법을 사용하여 코드를 작성하면 트랜스파일러는 이를 구 표준을 준수하는 코드로 변경한다. 반면, 새롭게 표준에 추가된 함수는 명세서 내 정의를 읽고 이에 맞게 직접 함수를 구현해야 사용할 수 있다. 자바스크립트에서는 원하기만 하면 어떤 함수라도 스크립트에 추가할 수 있고 기존 함수를 수정할 수 있다. 개발자는 스크립트에 새로운 함수를 추가/수정하여 스크립트가 최신 표준을 준수할 수 있게 작업할 수 있다. 이렇게 변경된 표준을 준수하도록 기존 함수의 동작 방식을 수정하거나 새롭게 구현한 함수의 스크립트를 폴리필이라 부른다. **구현이 누락된 새로운 기능을 메꿔주는 역할**을 한다.
