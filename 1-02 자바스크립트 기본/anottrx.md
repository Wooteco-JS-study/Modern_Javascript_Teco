<br />
<h1 align="center">1-02 자바스크립트 기본(first-steps)</h1>
<br />

> 자바스크립트 기본 문법

<br />

## 목차

1. [Hello, world!](#1)
2. [코드 구조](#2)
3. [엄격 모드](#3)
4. [변수와 상수](#4)
5. [자료형](#5)
6. [alert, prompt, confirm을 이용한 상호작용](#6)
7. [형 변환](#7)
8. [기본 연산자와 수학](#8)
9. [비교 연산자](#9)
10. [if와 '?'를 사용한 조건 처리](#10)
11. [논리 연산자](#11)
12. [nullish 병합 연산자 '??'](#12)
13. [while과 for 반복문](#13)
14. [switch문](#14)
15. [함수](#15)
16. [함수 표현식](#16)
17. [화살표 함수 기본](#17)
18. [기본 문법 요약](#18)

<br />

<div id="1"></div>

## 1. Hello, world!

> 실행 환경에 독립적인 코어 자바스크립트(core JavaScript)를 다룬다

### `<script>` 태그

- HTML 문서 대부분에 삽입 가능하며, 자바스크립트 코드가 안에 들어간다
- 속성(attribute) → 요즘은 잘 사용하지 않는다
  - type 속성 → 필수가 아니고, 자바스크립트 모듈에서 사용 가능
    - `<script type=text/javascript>` 
  - language 속성 → 자바스크립트가 기본 언어이므로 불필요
- 외부 스크립트
  ```html
  <script src="/path/to/script.js"></script>
  ```
  - 스크립트를 별도 파일에 작성하면 브라우저가 해당 스크립트를 다운받아 캐시에 저장 → 트래픽 절약, 속도 향상
- `<script>`는 `src`와 내부 코드를 동시에 가지지 못한다

### 과제

- alert 창 띄우기
  ```html
  <script>
    alert('경고창');
  </script>
  ```  
- 외부 스크립트 이용해 alert 창 띄우기
  ```html
  <script src="script.js"></script>
  ```
  ```js
  // script.js
  alert('경고창');
  ```

<br />

<div id="2"></div>

## 2. 코드 구조

> 코드 블록 만들기

- 문(statement) : 작업을 수행하는 문법 구조(syntax structure)와 명령어(command)
- 세미콜론(semicolon) : 줄바꿈은 보통 세미콜론을 의미
  - 자바스크립트가 세미콜론의 필요성을 인지 못하는 경우도 존재
    ```js
    alert('에러') // 작동
    [1, 2].forEach(alert) // 작동 안 함
    ```
    → 대괄호`[]` 앞에는 세미콜론이 있다고 가정하지 않기 때문
  - 세미콜론은 생략할 수 있지만 사용을 권장
- 주석(comment) : 한 줄은 `// 주석` 여러 줄은 `/* 주석 */`
  - 맥 단축키 : `Cmd+/`, `Cmd+Option+/`
  - 중첩 주석 불가능
  - 프로덕션 서버 배포 전에 코드 압축/삭제해주는 도구가 있다

<br />

<div id="3"></div>

## 3. 엄격 모드

> ECMAScript5(ES5)가 등장하고 기능 추가/변경되면서 하위 호환성 문제가 발생    
> → 변경사항 대부분 ES5 기본 모드에선 비활성화, `use strict` 사용시에만 활성화

### use strict

- 엄격 모드는 대개 스크립트 전체에 적용하지만, 함수 본문 맨 앞에 있을 경우 해당 함수에만 적용
  ```js
  "use strict";
  // 이 코드는 모던한 방식으로 실행된다
  ```
- 엄격 모드 적용을 취소할 방법은 없다

### 브라우저 콘솔

- 기본적으로 브라우저 콘솔은 `use strict`가 적용되지 않는다
  ```js
  // Firefox, Chrome 등 유명한 브라우저만 가능
  'use strict'; // Shift+Enter를 눌러 줄 바꿈
  // 코드 입력
  // Enter 눌러 실행
  ```
  ```js
  (function() {
    'use strict';
    // 코드 입력
  })()
  ```

### `use strict`를 꼭 사용해야 하나요

- 코드를 클래스와 모듈을 사용해 구성한다면 `use strict` 생략 가능   
  → 자동으로 적용되기 때문

### 과제

- 변수 가지고 놀기
  ```js
  let admin, name;
  name = "John";
  admin = name;
  alert(admin); // "John"
  ```
- 올바른 이름 선택하기
  ```js
  let planetName; // ourPlanetName
  let userName; // currentUserName
  ```
- 대문자 상수 올바로 사용하기
  ```js
  const BIRTHDAY = '18.04.1982'; // 대문자 적합
  const age = someCode(BIRTHDAY); // 대문자 적합하지 않음
  ```

<br />

<div id="4"></div>

## 4. 변수와 상수

### 변수

- 변수는 let을 이용해 선언
  - 같은 변수를 여러 번 선언하면 에러 발생
- 가독성을 위해서는 한 줄에 하나의 변수만 작성 권장
- 함수형 언어는 변숫값 변경 금지

### 변수 명명 규칙
- 변수명 : 문자, 숫자, `$`, `_`만 가능하고, 첫 글자는 숫자 불가능
- 주로 카멜 표기법(camelCase) 사용
- 대소문자 구분 (`num !== Num`)
- 한국어 등 모든 언어로 변수명 사용 가능 (`let 현재금액`)
- [예약어(reserved name) 목록](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#keywords)에 있는 단어는 변수명으로 사용 불가능
  - `let`, `class`, `return`, `function` 등
- use strict 없이 간단하게 값을 할당할 수 있었다
  ```js
  // "use strict"
  num = 5;
  alert(num); // 5
  ```

### 상수

- 변수 값이 절대 변하지 않고 코드가 실행되기 전 이미 그 값이 무엇인지 알거나, 런타임 시에 계산되지만 최초 할당 이후 변하지 않는 경우 `const`를 사용
- 상수의 변수명은 주로 대문자와 `_` 사용

### 바람직한 변수명

- 사람이 읽기 쉽고, 서술적이고 간결하며, 소속된 팀의 규칙을 따를 것 → 변수가 담고 있는 것이 무엇인지 쉽게 알 수 있다
  - data, value, a 등은 좋지 않은 예시

<br />

<div id="5"></div>

## 5. 자료형

> 변수에 저장되는 값의 타입을 바꿀 수 있는 언어는 `동적 타입(dynamically typed) 언어`

- 숫자형(number type) : 정수 및 부동소수점 숫자(floating point number) (±2^53)
  - 특수 숫자 값(special numeric value) : Infinity, -Infinity, NaN
- BigInt : (2^53-1)(9007199254740991)보다 큰 값 또는 -(2^53-1) 보다 작은 정수 (길이 제약 없이 정수 표현 가능)
  - 정수 리터럴 끝에 n을 붙여 만든다
  ```js
  const bigInt = 1234567890123456789012345678901234567890n;
  ```
- 문자형(string) : 자바스크립트는 글자형(character)이 없고 오직 문자형만 있다
- 불린형(논리 타입) : true와 false
- null 값 : 존재하지 않는(nothing) 값, 비어 있는(empty) 값, 알 수 없는(unknown) 값
- undefined 값 : 값이 할당되지 않은 상태
  - 직접 할당 가능하지만 변수가 비어있거나 알 수 없는 상태라는 걸 나타내려면 null 사용 권장
- 객체(object) : 복잡한 데이터 구조를 표현할 때 사용
  - 데이터 컬렉션이나 복잡한 개체(entity)를 표현 가능
  - 객체형을 제외한 다른 자료형은 한 가지만 표현할 수 있기 때문에 원시(primitive) 자료형
- 심볼(symbol)형 : 객체의 고유한 식별자(unique identifier)를 만들 때 사용
- typeof 연산자 : 피연산자의 자료형을 문자열 형태로 반환
  ```js
  typeof x // 연산자
  typeof(x) // 함수
  typeof Math // 수학 연산을 제공하는 내장 객체이므로 "object"
  typeof null // "object" (언어 자체의 오류)
  typeof alert // "function"
  ```

### 과제
```js
let name = "Ilya";
alert( `hello ${1}` ); // hello 1
alert( `hello ${"name"}` ); // hello name
alert( `hello ${name}` ); // hello Ilya
```

<br />

<div id="6"></div>

## 6. alert, prompt, confirm을 이용한 상호작용

> 모달 창이 떠 있는 동안 스크립트의 실행은 중지된다      
> 모달 창의 대가     
>  1. 모달 창의 위치는 브라우저가 결정(보통 브라우저 중앙)
>  2. 모달 창의 모양은 브라우저마다 다르고, 창의 모양을 수정 불가능

- alert : 확인 버튼 있는 모달 창
  ```js
  alert("Hello");
  ```
- prompt : 텍스트 메시지, 입력 필드(input field), 확인(OK), 취소(Cancel) 버튼이 있는 모달 창 
  ```js
  result = prompt(title, [default]);
  // title: 사용자에게 보여줄 문자열
  // default: 입력 필드의 초깃값(선택값)

  let age = prompt('나이를 입력해주세요.', 100);
  alert(`당신의 나이는 ${age}살 입니다.`); // 당신의 나이는 100살입니다.
  ```
  - 인수를 감싸는 대괄호(`[]`) → 선택
  - 취소 또는 ESC 누를 경우 null 반환
  - Internet Explorer(IE)는 기본값 없을 경우 undefined가 나오므로 `''`라도 전달할 것 권장
- 컨펌 대화상자 : 매개변수로 받은 question(질문)과 확인 및 취소 버튼 → 확인은 true, 취소 또는 ESC 누를 경우 false 반환
  ```js
  let isBoss = confirm("당신이 주인인가요?");
  alert( isBoss ); // 확인 버튼을 눌렀다면 true
  ```

### 과제
```js
let name = prompt('이름을 입력해주세요.', '');
alert(name);
```

<br />

<div id="7"></div>

## 7. 형 변환

> 형 변환(type conversion) : 적절한 자료형으로 자동 변환하거나 의도적으로 원하는 타입으로 변환(명시적 변환)하는 것

- 문자형으로 변환 : `String(x)`
- 숫자형으로 변환 : `Number(x)`
  - undefined → NaN, null → 0, true → 1, false → 0
  - string → 문자열 앞뒤 공백 제거후 남아있는 문자열이 없다면 0, 숫자만 있다면 해당 숫자, 실패하면 NaN
- 불린형으로 변환 : `Boolen(x)`
  - 0, 빈 문자열, null, undefined, NaN → false
  - ' ', 'hi' 등 그 외의 값은 true

<br />

<div id="8"></div>

## 8. 기본 연산자와 수학

- 피연산자(operand) : 연산자가 연산을 수행하는 대상 (인수(argument))
- 단항(unary) 연산자 : 피연산자를 하나만 받는 연산자
- 이항(binary) 연산자 : 두 개의 피연산자를 받는 연산자
```js
let x = 1, y = 2;
console.log(5 * 2); // 5와 2는 피연산자, +는 이항 연산자
x = -x; // -는 단항 연산자
```
- 덧셈 연산자 : +
  - 숫자 더하거나 문자열 병합
  ```js
  alert( 2 + '1' ); // "21"
  alert(2 + 2 + '1' ); // '41'
  ```
    - 다른 산술 연산자는 숫자형이 아닌 경우 숫자형으로 바꾼다
    ```js
    alert( 6 - '2' ); // 4
    alert( '6' / '2' ); // 3
    ```
  - 단항 연산자로 사용될 경우 Number()와 동일한 역할 수행
- 뺄셈 연산자 : -
- 곱셈 연산자 : *
- 나눗셈 연산자 : /
- 나머지 연산자(remainder operator) : %
- 거듭제곱 연산자 : **
  ```js
  alert( 2 ** 3 ); // 8
  alert( 8 ** (1/3) ); // 2 
  ```
- [연산자 우선순위 테이블](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#table) : 숫자 높을수록 우선순위가 높다
- 할당 연산자 : =
  ```js
  let a = 1, b = 1;
  let c = 3 - (a = b + 1); // 값을 반환하는 할당 연산자
  alert( a ); // 3
  alert( c ); // 0
  let c, d;
  c = d = 2 + 2; // 할당 연산자 체이닝
  ```
- 복합 할당 연산자 : +=, -=
- 증가·감소 연산자 : ++, --
  - 후위형(postfix form) : counter++와 같이 피연산자 뒤에 올 때
  - 전위형(prefix form) : ++counter와 같이 피연산자 앞에 올 때
- 비트 연산자(bitwise operator) : 인수를 32비트 정수로 변환해 이진 연산을 수행
  - 비트 AND ( & )
  - 비트 OR ( | )
  - 비트 XOR ( ^ )
  - 비트 NOT ( ~ )
  - 왼쪽 시프트(LEFT SHIFT) ( << )
  - 오른쪽 시프트(RIGHT SHIFT) ( >> )
  - 부호 없는 오른쪽 시프트(ZERO-FILL RIGHT SHIFT) ( >>> )
- 쉼표 연산자(comma operator)
  ```js
  let a = (1 + 2, 3 + 4);
  alert( a ); // 7 (마지막 표현식의 평가 결과만 반환)
  ```

### 과제
  ```js
  let a = 2;
  let x = 1 + (a *= 2);
  console.log(a, x); // 4, 5
  ```
  ```js
  "" + 1 + 0 // 1
  "" - 1 + 0 // -1
  true + false // 1
  6 / "3" // 2
  "2" * "3" // 6
  4 + 5 + "px" // 9px
  "$" + 4 + 5 // $45
  "4" - 2 // 2
  "4px" - 2 // NaN
  7 / 0 // Infinity
  "  -9  " + 5 // "  -9  5"
  "  -9  " - 5 // -14
  null + 1 // 1
  undefined + 1 // NaN
  " \t \n" - 2 // 0 -2 = -2 (공백 처리되어 0으로 변환)
  ```

<br />

<div id="9"></div>

## 9. 비교 연산자

- 불린형 반환 : true, false
- 문자열 비교 : 유니코드 순서대로 비교 (소문자 > 대문자)
  - 사전 순서대로 문자열 비교 (사전편집(lexicographical))
  ```js
  alert( 'Z' > 'A' ); // true
  alert( 'Glow' > 'Glee' ); // true
  alert( 'Bee' > 'Be' ); // true
  ```
- 다른 형을 가진 값 간의 비교
  - 비교하려는 값의 자료형이 다르면 숫자형으로 바꾼다
  ```js
  alert( '2' > 1 ); // true
  alert( '01' == 1 ); // true  
  ```
  - 흥미로운 상황
    ```js
    let a = 0;
    alert( Boolean(a) ); // false
    let b = "0";
    alert( Boolean(b) ); // true
    alert(a == b); // true!
    ```
- 일치 연산자
  - 동등 연산자(equality operator) ==
  - 일치 연산자(strict equality operator) === : 형 변환 없이 값을 비교 (엄격한(strict) 동등 연산자)
- null이나 undefined와 비교하기
  - undefined와 null을 비교하는 경우에만 true를 반환하고, null이나 undefined를 다른 값과 비교할 때는 무조건 false를 반환
  ```js
  alert( null == undefined ); // true
  alert( null === undefined ); // false
  ```
  - null은 0, undefined는 NaN으로 변환
    ```js
    alert( null == 0 ); // false
    alert( null >= 0 ); // true
    alert( undefined < 0 ); // false (NaN으로 변환)
    alert( undefined == 0 ); // false
    ```  
  - 일치 연산자 ===를 제외한 비교 연산자의 피연산자에 undefined나 null이 오지 않도록 주의
  - undefined나 null이 될 가능성이 있는 변수가 <, >, <=, >=의 피연산자가 되지 않도록 주의 → null, undefined 여부를 확인하는 코드를 따로 추가하는 습관 기를 것

### 과제

```js
5 > 4 // true
"apple" > "pineapple" // false
"2" > "12" // true
undefined == null // true
undefined === null // false
null == "\n0\n" // false
null === +"\n0\n" // false (형이 다르다)
```

<br />

<div id="10"></div>

## 10. if와 '?'를 사용한 조건 처리

- if문의 조건이 true라면 코드 블록 실행
  - 가독성 때문에 중괄호({}) 사용 권장
  - falsy 값 : 0, 빈 문자열"", null, undefined, NaN
- else 절은 조건이 false일 때 실행
- else if로 복수 조건 처리 가능
- 조건부(conditional) 연산자 ? (물음표(question mark) 연산자, 삼항(ternary) 연산자)
  ```js
  let result = condition ? value1 : value2;
  ```
- 다중 ? : 복수의 조건 처리 가능
- 부적절한 ? : ?를 if 대용으로 쓰는 것은 좋지 않다
  ```js
  let company = prompt('자바스크립트는 어떤 회사가 만들었을까요?', '');
  (company == 'Netscape') ?
    alert('정답입니다!') : alert('오답입니다!');
  ```  
- 여러 분기를 만들어 처리할 때는 if를 사용

### 과제
```js
let result = prompt("자바스크립트의 '공식' 이름은 무엇일까요?", '');
if(result === 'ECMAScript') {
  alert('정답입니다!')
} else {
  alert('모르셨나요? 정답은 ECMAScript입니다!');
}
```
```js
let message = (login == '직원') ? '안녕하세요.' :
  (login == '임원') ? '환영합니다' :
  (login == '') ? '로그인이 필요합니다.' :
  '';
```

<br />

<div id="11"></div>

## 11. 논리 연산자

- || (OR) : 하나라도 true면 true 반환
- 첫 번째 truthy를 찾는 OR 연산자 ‘||’
  - 반환 값은 형 변환을 하지 않은 원래 값
  - 연산 수행 순서
    - 피연산자 가장 왼쪽부터 시작해서 오른쪽으로 나아가며 비교
    - true면 연산을 멈추고 해당 피연산자의 변환 전 원래 값 반환
    - 모두 평가했는데 모두 false면 마지막 피연산자 반환
  ```js
  let firstName = "", lastName = "", nickName = "바이올렛";
  alert( firstName || lastName || nickName || "익명"); // 바이올렛
  ```
- && (AND) : 모두가 참일 때 true 반환
- 첫 번째 falsy를 찾는 AND 연산자 ‘&&’
  - 연산 수행 순서
    - 피연산자 가장 왼쪽부터 시작해서 오른쪽으로 나아가며 비교
    - false면 연산을 멈추고 해당 피연산자의 변환 전 원래 값 반환
    - 모두 평가했는데 모두 true면 마지막 피연산자 반환
  ```js
  alert( 1 && 2 && null && 3 ); // null
  alert( 1 && 2 && 3 ); // 마지막 값, 3
  ```
- AND 연산자는 첫 번째 falsy를 반환, OR은 첫 번째 truthy를 반환
- &&의 우선순위가 ||보다 높다
- if를 ||나 &&로 대체하면 가독성이 좋지 않으므로 권장하지 않는다
- ! (NOT)
  - 피연산자를 불린형(true / false)으로 변환 후, 해당 값의 역을 반환
  - !! : 불린형으로 변환 (Boolean()과 동일)
  ```js
  alert( !0 ); // true
  alert( !!"non-empty string" ); // true
  ```

### 과제
```js
alert( alert(1) || 2 || alert(3) ); // 1, 2
// 1. alert(1) 실행
// 2. alert메서드는 undefined를 반환
// 3. 2는 truthy이기 때문에 실행이 멈추고 2가 반환
```
```js
alert( 1 && null && 2 ); // 첫 번째 falsy인 null 출력
```
```js
alert( alert(1) && alert(2) ); // 1, undefined
// 1. undefined가 반환
// 2. alert(1) 실행
// 3. falsy인 undefined 출력
```
```js
alert( null || 2 && 3 || 4 ); // 3
// && 먼저 실행 → null || 3 || 4
// 첫 번째 truthy인 3 출력
```
```js
if (!(age >= 14 && age <= 90))
```
```js
if (-1 || 0) alert( 'first' ); // -1 || 0 은 -1 이므로 truthy라서 실행 
if (-1 && 0) alert( 'second' ); // 실행 안 됨
if (null || -1 && 1) alert( 'third' ); // null || 1라서 실행
```

<br />

<div id="12"></div>

## 12. nullish 병합 연산자 '??'

> nullish 병합 연산자(nullish coalescing operator) ??를 사용하면 값이 할당된 변수를 찾거나 변수에 기본값을 할당하는 용도로 사용 가능

- `a ?? b` 연산 결과 → a가 null과 undefined 모두 아니면 a, 그 외는 b
  ```js
  x = (a !== null && a !== undefined) ? a : b;
  ```
- '??'와 '||'의 차이
  - ||는 첫 번째 truthy 값을 반환
  - ??는 첫 번째 정의된(defined) 값을 반환
  ```js
  let height = 0;
  alert(height || 100); // 100 (0을 falsy로 취급)
  alert(height ?? 100); // 0
  ```
- ?? 우선순위는 낮기 때문에 괄호`()`와 함께 사용 권장
- ??는 안정성 관련 이슈 때문에 &&나 ||와 함께 사용 불가능하므로 괄호`()`와 함께 사용 필요
  ```js
  let x = 1 && 2 ?? 3; // SyntaxError: Unexpected token '??'

  let x = (1 && 2) ?? 3; // 2 (동작)
  ```
```js
// height가 null이나 undefined라면 100을 할당
height = height ?? 100;
```

<br />

<div id="13"></div>

## 13. while과 for 반복문

> 반복문(loop)을 사용하면 동일한 코드 여러 번 반복 가능

- `while` : 각 반복이 시작하기 전에 조건을 확인
  ```js
  let i = 3;
  while (i) { // i가 0이 되면 조건이 falsy가 되므로 반복문 중지
    alert( i );
    i--;
  }
  ```
- `do..while` : 각 반복이 끝난 후에 조건을 확인
  - 본문을 최소한 한 번이라도 실행하고 싶을 때만 사용
  - 대다수는 while이 적합
- `for (;;)` : 각 반복이 시작하기 전에 조건을 확인(추가 세팅 가능)
  ```js
  for (begin; condition; step) { }

  for (let i = 0; i < 3; i++) { // i가 0부터 3이 될 때까지 호출
    alert(i); // 0, 1, 2 출력
  }
  ```
  - 구성 요소 생략 가능
  ```js
  let i = 0; // i 선언 후 값 할당
  for (; i < 3; i++) { } // begin 생략

  for (; i < 3;) { // step 생략 
    alert( i++ );
  }
  for (;;) { } // 무한 반복문
  ```
- 반복문 빠져나오기 : break
- 다음 반복으로 넘어가기 : continue는 현재 반복을 종료시키고 다음 반복으로 넘어간다
- ‘?’ 오른쪽엔 break나 continue 사용 불가능
  ```js
  (i > 5) ? alert(i) : continue; // 문법 에러
  ```
- break/continue와 레이블
  ```js
  outer: for (let i = 0; i < 3; i++) {
    inner: // 별도의 줄에 작성 가능
    for (let j = 0; j < 3; j++) {
      let input = prompt(`(${i},${j})의 값`, '');
      
      // 사용자가 아무것도 입력하지 않거나 Cancel 버튼을 누르면 두 반복문 모두를 빠져나온다
      if (!input) break outer;
    }
  }
  alert('완료!');
  ```

### 과제
```js
for (let i = 0; i < 5; ++i) alert( i ); // 1234
for (let i = 0; i < 5; i++) alert( i ); // 1234
```
```js
// 사용자가 유효한 값을 입력할 때까지 프롬프트 창 띄우기
let num;
do {
  num = prompt("100을 초과하는 숫자를 입력해주세요.", 0);
} while (num <= 100 && num);
```

<br />

<div id="14"></div>

## 14. switch문

> 특정 변수를 다양한 상황에서 비교할 수 있고, 코드 자체가 비교 상황을 잘 설명한다

- 비교하려는 값과 case문의 값의 형과 값이 같아야 해당 case문이 실행
```js
let a = 2 + 2;
let b = 3;

switch (a) {
  case 2: // 여러 개의 case문 묶기
  case 3:
    alert( '비교하려는 값보다 작습니다.' );
    break;
  case b + 1: // 어떤 표현식이든 가능
    alert( '비교하려는 값과 일치합니다.' );
    // break문이 없으면 조건에 부합하는지 여부를 따지지 않고 이어지는 case문을 실행
  default: // 필수는 아니다
    alert( "어떤 값인지 파악이 되지 않습니다." );
}
```

<br />

<div id="15"></div>

## 15. 함수

> 함수 : 프로그램을 구성하는 주요 구성 요소(building block)       
> 함수는 중복을 없애고, 코드를 정돈하며 가독성을 높인다

- 함수 선언(function declaration)을 이용해 함수를 만들 수 있다
- 함수 내에서 선언한 변수인 지역 변수(local variable)는 함수 안에서만 접근 가능
- 함수 내부에서 함수 외부의 변수인 외부 변수(outer variable)에 접근 및 수정 가능
  - 함수 내부에 외부 변수와 동일한 이름을 가진 변수가 선언되면 내부 변수는 외부 변수를 가린다
  ```js
  let userName = 'John';
  function showMessage() {
    let userName = "Bob"; // 같은 이름
    alert('Hello, ' + userName); // Bob
  }
  showMessage();
  alert( userName ); // John
  ```
- 전역 변수(global variable) : 함수 외부에 선언된 변수로 최소한 사용 권장
- 매개변수(parameter) : 임의의 데이터를 함수 안에 전달 가능 (인자(parameter))
  - 매개변수 : 함수 선언 방식 괄호 사이에 있는 변수(선언)
  - 인수 : 함수를 호출할 때 매개변수에 전달되는 값(호출)
  - 함수 호출 시 매개변수에 인수를 전달하지 않으면 undefined이므로 기본값(default value)을 설정하면 된다
  ```js
  function showMessage(from, text = "no text given") {
    alert( from + ": " + text );
  }
  showMessage("Ann"); // Ann: no text given
  showMessage("Ann", undefined); // Ann: no text given

  function showMessage2(from, text = anotherFunction()) {
    // anotherFunction()은 text값이 없을 때만 호출됨
    // anotherFunction()의 반환 값이 text의 값이 됨
  }
  ```
  ```js
  // 구식 자바스크립트에서 매개변수 기본값 설정하는 방법
  function showMessage(from, text) {
    // 방법 1
    if (text === undefined) {
      text = 'no text given';
    }
    // 방법 2
    text = text || 'no text given';
    alert( from + ": " + text );
  }

  // 매개변수 'count'가 `undefined` 또는 `null`이면 'unknown'을 출력해주는 함수
  function showCount(count) {
    // nullish 병합 연산자(nullish coalescing operator) ?? 사용
    alert(count ?? "unknown");
  }

  showCount(0); // 0
  showCount(null); // unknown
  showCount(); // unknown
  ```
- 반환 값(return value) : return문
  - return문이 없거나 return 지시자만 있는 함수는 undefined 반환
    ```js
    function doNothing() { /* empty */ }
    function doNothing2() {
      return;
    }
    alert( doNothing() === undefined ); // true
    alert( doNothing2() === undefined ); // true
    ```
  - return과 값 사이 줄을 삽입할 경우 자동으로 세미콜론이 생겨서 문제가 발생할 수 있다
- 함수 이름짓기 → 함수는 동작을 수행하므로 주로 동사
  - "get…" – 값을 반환함
  - "calc…" – 무언가를 계산함
  - "create…" – 무언가를 생성함
  - "check…" – 무언가를 확인하고 불린값을 반환함
- 함수는 하나의 동작만 담당할 것
- 함수의 이름을 잘 지으면 주석과 같은 역할을 한다
- 아주 짧은 함수 이름
  - jQuery 프레임워크에서 쓰이는 함수 $
  - Lodash 라이브러리의 핵심 함수 _ 

### 과제
```js
function checkAge(age) {
  return (age > 18) || confirm('동의를 받으셨나요?');
}
```

<br />

<div id="16"></div>

## 16. 함수 표현식

> 자바스크립트는 함수를 특별한 종류의 값으로 취급

- 함수 표현식(Function Expression)을 사용해서 함수 생성 가능
  - 자바스크립트는 괄호가 있어야만 함수가 호출된다
  ```js
  let sayHi = function() {
    alert( "Hello" );
  }; // 값처럼 취급되어 변수에 할당된 것이므로 구문의 끝으로 취급되어 ;가 붙는다

  alert( sayHi ); // funtion() { alert( "Hello" ); } 출력
  ```
- 콜백 함수 : 함수를 함수의 인수로 전달하고, 필요하다면 인수로 전달한 그 함수를 나중에 호출(called back)하는 것
  ```js
  function ask(question, yes, no) {
    if (confirm(question)) yes()
    else no();
  }
  // showOk와 showCancel은 콜백 함수 또는 콜백
  function showOk() {
    alert( "동의하셨습니다." );
  }
  function showCancel() {
    alert( "취소 버튼을 누르셨습니다." );
  }

  // 사용법: 함수 showOk와 showCancel가 ask 함수의 인수로 전달됨
  ask("동의하십니까?", showOk, showCancel);
  ```
- 함수는 동작을 나타내는 값

### 함수 표현식 vs 함수 선언문
- 함수 표현식: 함수는 표현식이나 구문 구성(syntax construct) 내부에 생성
  - 실제 실행 흐름이 해당 함수에 도달했을 때 함수를 생성 → 실행 흐름이 함수에 도달했을 때부터 해당 함수 사용 가능
  ```js
  // 함수 표현식
  let sum = function(a, b) {
    return a + b;
  };
  ```
- 함수 선언문: 함수는 주요 코드 흐름 중간에 독자적인 구문 형태로 존재
  - 함수 선언문이 정의되기 전에도 호출 가능
  - 자바스크립트는 스크립트를 실행하기 전에 준비단계에서 전역에 선언된 함수 선언문을 모두 찾아 함수를 생성한다. 즉, 초기화 단계에서 함수 선언 방식으로 정의한 함수가 생성된다. 그리고 스크립트는 함수 선언문이 모두 처리된 이후에 실행되므로, 스크립트 어디어든 함수 선언문으로 선언한 함수에 접근할 수 있다
  ```js
  // 함수 선언문
  function sum(a, b) {
    return a + b;
  }
  ```
- 엄격 모드에서 함수 선언문이 코드 블록 내에 위치하면 해당 함수는 블록 내 어디서든 접근 가능하지만 블록 밖에서는 함수에 접근 불가능
  ```js
  let age = prompt("나이를 알려주세요.", 18);
  let hello;
  if (age < 18) {
    welcome(); // 실행
    function welcome() {
      alert("안녕!");
    }
    hello = function() {
      alert("안녕안녕!");
    };
  } else {
    function welcome() {
      alert("안녕하세요!");
    }
    hello = function() {
      alert("안녕!");
    };
  }

  // 함수를 나중에 호출합니다.
  welcome(); // Error: welcome is not defined
  hello(); // 동작한다
  ```
- 함수 선언문으로 함수를 정의하면, 함수가 선언되기 전에 호출할 수 있어서 코드 구성을 좀 더 자유롭게 할 수 있고 가독성도 좋으므로 함수 선언문 권장
- 조건에 따라 함수를 선언해야 한다면 함수 표현식 사용 → 함수 선언문을 사용하지 못할 때 사용 권장

<br />

<div id="17"></div>

## 17. 화살표 함수 기본

> 화살표 함수(arrow function)를 통해 함수 표현식보다 더 간결하게 함수 생성 가능

```js
let sum = (a, b) => a + b;
let double = n => n * 2; // 인수가 1개면 괄호 생략
let sayHi = () => alert("안녕하세요!"); // 인수가 없을 때

let age = prompt("나이를 알려주세요.", 18);
let welcome = (age < 18) ?
  () => alert('안녕') :
  () => alert("안녕하세요!");
welcome();

let sum = (a, b) => {  // 본문 여러 줄일 때는 중괄호
  let result = a + b;
  return result; // 중괄호 사용할 경우 return 지시자로 결괏값을 반환 필수
};
alert( sum(1, 2) ); // 3
```

<br />

<div id="18"></div>

## 18. 기본 문법 요약

- 코드 구조
- 엄격 모드 (use strict)
  - use strict가 없으면 하위 호환성을 지키며 모던하지 않은 옛날 방식으로 동작
- 변수
- 상호작용 : 호스트 환경이 브라우저라면 UI 함수를 이용해 사용자와 상호작용 가능
- 연산자
- 반복문
- switch문
- 함수
  - 함수 선언문
  - 함수 표현식
  - 화살표 함수

<br />
<br />
