# 2.02 First steps

## 1. Hello, world!
### script 태그
- `<script>` 태그를 이용하면 자바스크립트 프로그램을 HTML 문서 대부분의 위치에 삽입 가능
- `<script>` 태그엔 자바스크립트 코드가 들어감

### 모던 마크업
- `<script>` 태그 속성
	- `type` 속성
		- HTML4에선 스크립트에 `type`을 명시하는 것이 필수였지만, 이젠 타입 명시가 필수가 아님
		- 모던 HTML 표준에선 이 속성의 의미가 바뀜
	- `language` 속성
		- 현재 사용하고 있는 스크립트 언어를 나타냄
	- 스크립트 전후에 위치한 주석
		-  모던 자바스크립트에선 이런 트릭을 사용하지 않
	```javascript
		```html no-beautify
		<script type="text/javascript"><!--
		    ...
		//--></script>
		```
	```

### 외부 스크립트
- js 코드의 양이 많은 경우, 파일로 소분하여 저장함
- `src` 속성을 사용해 HTML에 삽입
	 ```javascript
	 <script src="/path/to/script.js"></script>
	 ```
- 루트에서부터 파일이 위치한 절대 경로를 나타냄
- 현재 페이지에서의 상대 경로 사용 가능
- HTML 안에 직접 스크립트를 작성하는 방식은 대개 스크립트가 아주 간단할 때만 사용

## 2. 코드 구조

### 문(statement)
> 어떤 작업을 수행하는 문법 구조(syntax structure)와 명령어(command)
- 서로 다른 문은 세미콜론으로 구분함

### 세미콜론
- 줄 바꿈이 있다면 세미콜론은 생략 가능
	- 암시적 세미콜론으로 해석함
	- 이런 동작 방식을 [세미콜론 자동 삽입(automatic semicolon insertion)](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion)이라 부름
- 줄 바꿈이 항상 세미콜론을 의미하지는 않음
	```javascript
	alert(3 +
	1
	+ 2);
	```
- 세미콜론이 정말로 필요하지만 자바스크립트가 이를 추정하지 '못하는' 상황도 존재함
	- 자바스크립트가 대괄호 `[...]`앞에는 세미콜론이 있다고 가정하지 않음

### 주석
> 무슨 일이 왜 벌어지고 있는지를 설명하기 위해 사용
- 스크립트의 어느 곳에나 작성 가능
- 한 줄짜리 주석은 두 개의 슬래시  `//`로 시작
- 여러 줄의 주석은 슬래시와 별표  `/*`로 시작해 별표와 슬래시  `*/`로 끝남

## 3. 엄격 모드
> 새롭게 제정된 ES5에서는 새로운 기능이 추가되고 기존 기능 중 일부가 변경됨.
>  기존 기능을 변경하였기 때문에 하위 호환성 문제가 생길 수 있기 때문에 변경사항 대부분은 ES5의 기본 모드에선 활성화되지 않도록 설계됨. 
>  대신 `use strict`라는 특별한 지시자를 사용해 엄격 모드(strict mode)를 활성화 했을 때만 이 변경사항이 활성화되게 해놓음

### use strict
- 지시자 `"use strict"`, 혹은 `'use strict'`가 스크립트 최상단에 오면 스크립트 전체가 "모던한" 방식으로 동작함
```javascript
"use strict";
```
- `"use strict"`는 스크립트 최상단이 아닌 함수 본문 맨 앞에 올 수도 있음
	- 함수 본문 맨 앞에 오면 오직 해당 함수만 엄격 모드로 실행

### 'use strict'를 꼭 사용해야 하나요
- 모던 자바스크립트는 '클래스'와 '모듈'이라 불리는 진일보한 구조를 제공함
	- `use strict`가 자동으로 적용
- 코드를 클래스와 모듈을 사용해 구성한다면  `"use strict"`를 생략해도 됨

## 4. 변수와 상수

### 변수
> 데이터를 저장할 때 쓰이는 '이름이 붙은 저장소'
> ex) 온라인 쇼핑몰 애플리케이션을 구축하는 경우 상품이나 방문객 등의 정보를 저장할 때 변수를 사용

- 자바스크립트에선 `let` 키워드를 사용해 변수를 생성함
	```javascript
	let message = 'Hello!'; // 변수를 정의하고 값을 할당
	alert(message); // Hello!
	```
- 문자열이 변수와 연결된 메모리 영역에 저장되어서 변수명을 이용해 문자열에 접근 가능하게 됨
- `var`도 `let`처럼 변수를 선언하는 데 쓰이지만 `var`는 '오래된' 방식임

### 변수 명명 규칙
> 1.  변수명에는 오직 문자와 숫자, 그리고 기호  `$`와  `_`만 들어갈 수 있음
> 2.  첫 글자는 숫자가 될 수 없음

- 변수명을 만들 땐 [카멜 표기법(camelCase)](https://en.wikipedia.org/wiki/CamelCase)이 흔히 사용
	- 단어를 차례대로 나열하면서 첫 단어를 제외한 각 단어의 첫 글자를 대문자로 작성함
- [예약어(reserved name) 목록](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)에 있는 단어는 변수명으로 사용할 없음.
	- 예약어 예시: `let`, `class`, `return`, `function`
	- 자바스크립트 내부에서 이미 사용 중이기 때문임

### 상수
> 변화하지 않는 변수를 선언할 땐, `let` 대신 `const`를 사용

- 대문자 상수
	- 기억하기 힘든 값을 변수에 할당해 별칭으로 사용하는 것은 널리 사용되는 관습
	- 대문자와 밑줄로 구성된 이름으로 명명

### 바람직한 변수명
- 변수명은 간결하고, 명확해야 함
- 변수가 담고있는 것이 무엇인지 잘 설명할 수 있어야 함
> - `userName` 이나 `shoppingCart`처럼 사람이 읽을 수 있는 이름을 사용하세요.
> - 무엇을 하고 있는지 명확히 알고 있지 않을 경우 외에는 줄임말이나 `a`, `b`, `c`와 같은 짧은 이름은 피하세요.
> - 최대한 서술적이고 간결하게 명명해 주세요. `data`와 `value`는 나쁜 이름의 예시입니다. 이런 이름은 아무것도 설명해주지 않습니다. 코드 문맥상 변수가 가리키는 데이터나 값이 아주 명확할 때에만 이런 이름을 사용합시다.
> - 자신만의 규칙이나 소속된 팀의 규칙을 따르세요. 만약 사이트 방문객을 'user'라고 부르기로 했다면, 이와 관련된 변수를 `currentVisitor`나 `newManInTown`이 아닌 `currentUser`나 `newUser`라는 이름으로 지어야 합니다.

## 5. 자료형
> 자바스크립트에서 값은 항상 문자열이나 숫자형 같은 특정한 자료형에 속함
> 동적 타입(dynamically typed) 언어 = 자료의 타입은 있지만 변수에 저장되는 값의 타입은 언제든지 바꿀 수 있는 언어

### 숫자형
> 정수 및 부동소수점 숫자(floating point number)를 나타냄
```js
let n = 123;
n = 12.345;
```
- 숫자형엔 일반적인 숫자 외에 `Infinity`, `-Infinity`, `NaN`같은 '특수 숫자 값(special numeric value)'이 포함됨
	- `Infinity`는 어떤 숫자보다 더 큰 특수 값, [무한대(∞)](https://en.wikipedia.org/wiki/Infinity)를 나타냄
	- `NaN`은 계산 중에 에러가 발생했다는 것을 나타내주는 값

### BigInt
> 표준으로 채택된 지 얼마 안 된 자료형으로, 길이에 상관없이 정수를 나타낼 수 있음

```js
// 끝에 'n'이 붙으면 BigInt형 자료
const bigInt = 1234567890123456789012345678901234567890n;
```
### 문자형
> 문자열(string)을 따옴표로 묶음
> 1.  큰따옴표:  `"Hello"`
> 2.  작은따옴표:  `'Hello'`
> 3.  역 따옴표(백틱, backtick):  `` `Hello` ``
```js
let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed another ${str}`;
```
### Boolean형
> `true`와 `false` 두 가지 값밖에 없는 자료형

- 긍정(yes)이나 부정(no)을 나타내는 값을 저장할 때 사용
	- `true`는 긍정, `false`는 부정
```js
let isChecked= true; 
let isOpen = false; 
let isGreater = 4 > 1; // true
```

### 'null' 값
> 지금까지 소개한 자료형 중 어느 자료형에도 속하지 않는 값
> '존재하지 않는(nothing)' 값
> '비어 있는(empty)' 값
> '알 수 없는(unknown)' 값

### 'undefined' 값
> 값이 할당되지 않은 상태

- 변수는 선언했지만, 값을 할당하지 않았다면 해당 변수에 `undefined`가 자동으로 할당됨
```js
let age;
alert(age); // 'undefined'
```

### 객체와 심볼
> `객체(object)` = 데이터 컬렉션이나 복잡한 개체(entity)를 표현
> `심볼(symbol)` = 객체의 고유한 식별자(unique identifier)를 만들 때 사용

### typeof 연산자
> 인수의 자료형을 반환
> 1.  연산자:  `typeof x`
> 2.  함수:  `typeof(x)`

- 자료형에 따라 처리 방식을 다르게 하고 싶거나 변수의 자료형을 빠르게 알아내고자 할 때 유용

```js
typeof undefined // "undefined"
typeof 0 // "number"
typeof 10n // "bigint"
typeof true // "boolean"
typeof "foo" // "string"
typeof Symbol("id") // "symbol"
typeof Math // "object"
typeof null // "object" 
typeof alert // "function"
```
- `null`의 typeof 연산은 `"object"`인데, 이는 언어상 오류. 
	- null은 객체가 아님

## alert, prompt, confirm을 이용한 상호작용
> 브라우저 환경에서 사용되는 최소한의 사용자 인터페이스 기능

### alert
> 이 함수가 실행되면 사용자가 '확인(OK)' 버튼을 누를 때까지 메시지를 보여주는 창이 계속 떠있게 됨
```js
alert("Hello");
```
### prompt
> 함수가 실행되면 텍스트 메시지와 입력 필드(input field), 확인(OK) 및 취소(Cancel) 버튼이 있는 모달 창을 띄움

```js
result = prompt(title, [default]);
```
- `title`  : 사용자에게 보여줄 문자열
- `default`  : 입력 필드의 초깃값(선택값)
	- `default`를 감싸는 대괄호는 이 매개변수가 필수가 아닌 선택값이라는 것을 의미함
- 사용자가 입력 필드에 기재한 문자열을 반환
	- 사용자가 입력을 취소한 경우는 `null`이 반환

### 컨펌 대화상자
> 매개변수로 받은 `question(질문)`과 확인 및 취소 버튼이 있는 모달 창을 보여줌
```js
let isBoss = confirm("당신이 주인인가요?");

alert( isBoss ); // 확인 버튼을 눌렀다면 true가 출력
```

### 제약사항
1.  모달 창의 위치는 브라우저가 결정하는데, 대개 브라우저 중앙에 위치함
2.  모달 창의 모양은 브라우저마다 다름. 개발자는 창의 모양을 수정할 수 없음

## 7. 형 변환
> 함수와 연산자에 전달되는 값은 대부분 적절한 자료형으로 자동 변환되는 것
> 전달받은 값을 의도를 갖고 원하는 타입으로 변환(명시적 변환)해 주는 경우

### 문자형으로 변환
> 문자형의 값이 필요할 때 일어남

```js
let value = true;
alert(typeof value); // boolean

value = String(value); // 변수 value엔 문자열 "true"가 저장
alert(typeof value); // string
```

- `alert(value)`에서 value는 문자형이어야 함
	- 다른 형의 값을 전달받으면 이 값은 문자형으로 자동 변환됨
- `false`는 문자열 `"false"`로, `null`은 문자열 `"null"`로 변환
- 대부분 예측 가능한 방식으로 일어남

### 숫자형으로 변환
> 수학과 관련된 함수와 표현식에서 자동으로 일어남

```js
let str = "123";
alert(typeof str); // string

let num = Number(str); // 문자열 "123"이 숫자 123으로 변환

alert(typeof num); // number
```

| 전달받은 값 | 형 변환 후 |
|-------|-------------|
|`undefined`|`NaN`|
|`null`|`0`|
|<code>true&nbsp;and&nbsp;false</code> | `1` 과 `0` |
| `string` | 문자열의 처음과 끝 공백이 제거됩니다. 공백 제거 후 남아있는 문자열이 없다면 `0`, 그렇지 않다면 문자열에서 숫자를 읽습니다. 변환에 실패하면 `NaN`이 됩니다.|

- `null`과 `undefined`는 숫자형으로 변환 시 결과가 다르다는 점에 유의

### 불린형으로 변환
> 논리 연산을 수행할 때 발생

```js
alert( Boolean(1) ); // 숫자 1(true)
alert( Boolean(0) ); // 숫자 0(false)

alert( Boolean("hello") ); // 문자열(true)
alert( Boolean("") ); // 빈 문자열(false)
```

-   숫자  `0`, 빈 문자열,  `null`,  `undefined`,  `NaN`과 같이 직관적으로도 "비어있다고" 느껴지는 값들은  `false`
-   그 외의 값은  `true`로 변환

## 8. 기본 연산자와 수학

### 용어: '단항', '이항', '피연산자'
- 피연산자(operand): 연산자가 연산을 수행하는 대상
	- `5 * 2`에는 왼쪽 피연산자 `5`와 오른쪽 피연산자 `2`, 총 두 개의 피연산자가 있음
	- '인수(argument)'라는 용어로 불리기도 함
- 단항(unary) 연산자: 피연산자를 하나만 받는 연산자
	-  ex) 피연산자의 부호를 뒤집는 단항 마이너스 연산자 `-`
- 이행(binary) 연산자: 두 개의 피연산자를 받는 연산자

### 수학
-   덧셈 연산자  `+`
-   뺄셈 연산자  `-`
-   곱셈 연산자  `*`
-   나눗셈 연산자  `/`
-   나머지 연산자  `%`
	```js
	alert( 5 % 2 ); // 5를 2로 나눈 후의 나머지인 1을 출  력
    alert( 8 % 3 ); // 8을 3으로 나눈 후의 나머지인 2를 출력
	```
-   거듭제곱 연산자  `**`
	```js
	alert( 2 ** 2 ); // 4  (2 * 2)
	alert( 2 ** 3 ); // 8  (2 * 2 * 2)
	alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2)
	alert( 4 ** (1/2) ); // 2 (1/2 거듭제곱은 제곱근)
	alert( 8 ** (1/3) ); // 2 (1/3 거듭제곱은 세제곱근)
	```

### 이항 연산자 '+'와 문자열 연결
> 이항 연산자 `+`의 피연산자로 문자열이 전달되면 덧셈 연산자는 덧셈이 아닌 문자열을 병합(연결)
```js
let s = "my" + "string";
alert(s); // mystring
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```

### 단항 연산자 +와 숫자형으로의 변환
> 피연산자가 숫자가 아닌 경우엔 숫자형으로 변환
```js
alert( +true ); // 1
alert( +"" );   // 0
```
### 연산자 우선순위
> [우선순위 테이블(precedence table)](https://developer.mozilla.org/en/JavaScript/Reference/operators/operator_precedence)참고

### 할당 연산자
- `=`
- 할당 연산자 체이닝
	```js
	let a, b, c;

	a = b = c = 2 + 2;

	alert( a ); // 4
	alert( b ); // 4
	alert( c ); // 4
	```
	```js
	c = 2 + 2;
	b = c;
	a = c;
	```
	- 전자의 코드보다는 후자의 코드가 가독성이 좋음
- 복합 할당 연산자
	- `+=`, `-=`, `*=` `/=`
- 증가 · 감소 연산자
	- `++`, `--`
	-   `counter++`와 같이 피연산자 뒤에 올 때는, '후위형(postfix form)'이라고 부름
		- 값을 증가시키지만, 증가 전의 기존값을 사용할 때
	-   `++counter`와 같이 피연산자 앞에 올 때는, '전위형(prefix form)'이라고 부름
		- 값을 증가시키고 난 후, 증가한 값을 바로 사용할 때

### 비트 연산자
> 인수를 32비트 정수로 변환하여 이진 연산을 수행

-   비트 AND (  `&`  )
-   비트 OR (  `|`  )
-   비트 XOR (  `^`  )
-   비트 NOT (  `~`  )
-   왼쪽 시프트(LEFT SHIFT) (  `<<`  )
-   오른쪽 시프트(RIGHT SHIFT) (  `>>`  )
-   부호 없는 오른쪽 시프트(ZERO-FILL RIGHT SHIFT) (  `>>>`  )

### 쉼표 연산자
> 여러 표현식을 코드 한 줄에서 평가할 수 있게 해
> 코드를 짧게 쓰려는 의도로 가끔 사용
> 쉼표 연산자의 연산자 우선순위는 매우 낮
```js
let a = (1 + 2, 3 + 4);

alert( a ); // 7 (3 + 4의 결과)
```
- 첫 번째 표현식 `1 + 2`은 평가가 되지만 그 결과는 버려지고 `3 + 4`만 평가되어 `a`에 할당

## 9. 비교 연산자
-   보다 큼·작음:  `a > b`,  `a < b`
-   보다 크거나·작거나 같음:  `a >= b`,  `a <= b`
-   같음(동등):  `a == b`
	-   `a ​​= b`와 같이 등호가 하나일 때는 할당을 의미
-   같지 않음(부등): 같지 않음을 나타내는 수학 기호  `≠`는 자바스크립트에선  `a != b`로 나타냄
	-  할당연산자  `=`  앞에 느낌표  `!`를 붙여서 표시

### 불린형 반환
-   `true`가 반환되면, '긍정', '참', '사실'을 의미
-   `false`가 반환되면, '부정', '거짓', '사실이 아님'을 의미
```js
alert( 2 > 1 );  // true
alert( 2 == 1 ); // false
alert( 2 != 1 ); // true
```

### 문자열 비교
> 자바스크립트는 '사전' 순으로 문자열을 비교함. (= '사전편집(lexicographical)'순)
```js
alert( 'Z' > 'A' ); // true
alert( 'Glow' > 'Glee' ); // true
alert( 'Bee' > 'Be' ); // true
```
- 소문자가 대문자보다 더 큼
	- 유니코드에선 소문자가 대문자보다 더 큰 인덱스를 갖기 때문

### 다른 형을 가진 값 간의 비교
> 비교하려는 값의 자료형이 다르면 자바스크립트는 이 값들을 숫자형으로 바꿈
```js
alert( '2' > 1 ); // true, 문자열 '2'가 숫자 2로 변환된 후 비교
alert( '01' == 1 ); // true, 문자열 '01'이 숫자 1로 변환된 후 비교
alert( true == 1 ); // true
alert( false == 0 ); // true
```

### 일치 연산자
> `===`를 사용하면 형 변환 없이 값을 비교할 수 있음

- 엄격한(strict) 동등 연산자
- 자료형의 동등 여부까지 검사하기 때문에 피연산자 `a`와 `b`의 형이 다를 경우 `a === b`는 즉시 `false`를 반환
- '불일치' 연산자 `!==`는 부등 연산자 `!=`의 엄격한 버전임

### null이나 undefined와 비교하기
- 일치 연산자 `===`를 사용하여 `null`과 `undefined`를 비교 : 두 값의 자료형이 다르기 때문에 일치 비교 시 거짓이 반환
	- 동등 연산자 `==`를 사용하면 참 반환

```js
alert( null > 0 );  // false
alert( null == 0 ); // false
alert( null >= 0 ); // true

alert( undefined > 0 ); // false 
alert( undefined < 0 ); // false 
alert( undefined == 0 ); // false 
```

## if와 '?'를 사용한 조건 처리

### 'if' 문
> `if(...)`문은 괄호 안에 들어가는 조건을 평가하는데, 그 결과가 `true`이면 코드 블록이 실행

### 불린형으로의 변환
> `if (…)` 문은 괄호 안의 표현식을 평가하고 그 결과를 불린값으로 변환

- 숫자  `0`, 빈 문자열`""`,  `null`,  `undefined`,  `NaN`은 불린형으로 변환 시 모두  `false`가 되므로 'falsy(거짓 같은)' 값
- 이 외의 값은 불린형으로 변환시  `true`가 되므로 'truthy(참 같은)' 값

### 'else'절
> `if`문엔 `else` 절을 붙일 수 있음
>  `else` 뒤에 이어지는 코드 블록은 조건이 거짓일 때 실행
> 유사하지만 약간씩 차이가 있는 조건 여러 개를 처리해야 할 때 `else if` 사용

### 조건부 연산자 '?'
> 조건에 따라 다른 값을 변수에 할당해줘야 할 때 사용
> 물음표(question mark) 연산자라고도 불림
> 피연산자가 세 개이기 때문에 조건부 연산자를 '삼항(ternary) 연산자'라고도 불림

```js
let result = condition ? value1 : value2;
```
- `condition`이 truthy라면 `value1`이, 그렇지 않으면 `value2`가 반환


```js
let age = prompt('나이를 입력해주세요.', 18);

let message = (age < 3) ? '아기야 안녕?' :
  (age < 18) ? '안녕!' :
  (age < 100) ? '환영합니다!' :
  '나이가 아주 많으시거나, 나이가 아닌 값을 입력 하셨군요!';

alert( message );
```
- 물음표 연산자`?`를 여러 개 연결하면 복수의 조건을 처리가능

## 11. 논리 연산자
### || (OR)
```js
result = a || b;

alert( true || true );   // true
alert( false || true );  // true
alert( true || false );  // true
alert( false || false ); // false
```
OR 연산자와 피연산자가 여러 개인 경우:
```js
result = value1 || value2 || value3;
```
-   가장 왼쪽 피연산자부터 시작해 오른쪽으로 나아가며 피연산자를 평가
-   각 피연산자를 불린형으로 변환 후 그 값이  `true`이면 연산을 멈추고 해당 피연산자의  **변환 전**  원래 값을 반환
-   피연산자 모두를 평가한 경우(모든 피연산자가  `false`로 평가되는 경우)엔 마지막 피연산자를 반환
> 단락 평가(short circuit evaluation)
> - 연산자 왼쪽 조건이 falsy일 때만 명령어를 실행하고자 할 때 자주 쓰임
> ```js
> true || alert("not printed");
> false || alert("printed");
> ```

### && (AND)
```js
result = a && b;

alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```

```js
result = value1 && value2 && value3;
```
-   가장 왼쪽 피연산자부터 시작해 오른쪽으로 나아가며 피연산자를 평가
-   각 피연산자는 불린형으로 변환됩니다. 변환 후 값이  `false`이면 평가를 멈추고 해당 피연산자의  **변환 전**  원래 값을 반환
-   피연산자 모두가 평가되는 경우(모든 피연산자가  `true`로 평가되는 경우)엔 마지막 피연산자가 반환

### ! (NOT)
```js
result = !value;

alert( !true ); // false
alert( !0 ); // true

alert( !!"non-empty string" ); // true
alert( !!null ); // false

alert( Boolean("non-empty string") ); // true
alert( Boolean(null) ); // false
```

- `NOT` 연산자의 우선순위는 모든 논리 연산자 중에서 가장 높기 때문에 항상 `&&`나 `||` 보다 먼저 실행

## 12. nullish 병합 연산자 '??'
`a ?? b`의 평가 결과
-   `a`가  `null`도 아니고  `undefined`도 아니면  `a`
-   그 외의 경우는  `b`

### '??'와 '||'의 차이
-   `||`는 첫 번째  _truthy_  값을 반환
-   `??`는 첫 번째  _정의된(defined)_  값을 반환

```js
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```

### 연산자 우선순위
- `??`는 `=`와 `?` 보다는 먼저, 대부분의 연산자보다는 나중에 평가
- 안정성 관련 이슈 때문에  `??`는  `&&`나  `||`와 함께 사용하지 못함

## 13. while과 for 반복문
> _반복문(loop)_ 을 사용하면 동일한 코드를 여러 번 반복 가능

### 'while' 반복문
```js
while (condition) {
  // 코드
  // '반복문 본문(body)'이라 불림
}
```
### 'do..while' 반복문
> 조건이 truthy 인지 아닌지에 상관없이, 본문을 **최소한 한 번**이라도 실행하고 싶을 때만 사용
```js
do {
  // 반복문 본문
} while (condition);
```

### 'for' 반복문
```js
for (begin; condition; step) {
  // ... 반복문 본문 ...
}
```
| 구성 요소 | | |
|-------|----------|----------------------------------------------------------------------------|
| begin | `i = 0` | 반복문에 진입할 때 단 한 번 실행됨
| condition | `i < 3`| 반복마다 해당 조건이 확인되고, false이면 반복문을 멈춤 |
| body | `alert(i)`| condition이 truthy일 동안 계속해서 실행됨 |
| step| `i++` | 각 반복의 body가 실행된 이후에 실행됨 |

- 구성 요소 생략하기
	- `begin` 생략
		```js
		let i = 0;

		for (; i < 3; i++) {
		  alert( i ); // 0, 1, 2
		}
		```
	- `step` 생략
		```js
		let i = 0;

		for (; i < 3;) {
		  alert( i++ );
		}
		```
- `break`를 사용하면 언제든 원하는 때에 반복문을 빠져나올 수 있음
- `continue` 지시자는 `break`의 '가벼운 버전'
	- `continue`는 현재 실행 중인 이터레이션을 멈추고 반복문이 다음 이터레이션을 강제로 실행시키도록 함(조건을 통과할 때).

### break/continue와 레이블 ✨
> 중첩 반복문일 때 완전히 빠져나오려면 label을 쓰면 됨
> 반복문 앞에 콜론과 함께 쓰이는 식별자
```js
labelName: for (...) {
  ...
}
```
```js
outer: for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`(${i},${j})의 값`, '');

    // 사용자가 아무것도 입력하지 않거나 Cancel 버튼을 누르면 두 반복문 모두를 빠져나
    if (!input) break outer;

    // 입력받은 값을 가지고 무언가를 함
  }
}
alert('완료!');
```
## 14. switch문
> 복수의 `if` 조건문은 `switch`문으로 바꿀 수 있음
```js
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```
- `case`문 안에  `break`문이 없으면 조건에 부합하는지 여부를 따지지 않고 이어지는  `case`문을 실행


```js
let a = 3;

switch (a) {
  case 4:
    alert('계산이 맞습니다!');
    break;

  case 3: // (*) 두 case문을 묶음
  case 5:
    alert('계산이 틀립니다!');
    alert("수학 수업을 다시 들어보는걸 권유 드립니다.");
    break;

  default:
    alert('계산 결과가 이상하네요.');
}
```

## 15. 함수
> 함수는 프로그램을 구성하는 주요 '구성 요소(building block)
> 함수를 이용하면 중복 없이 유사한 동작을 하는 코드를 여러 번 호출 가능

### 함수 선언
```js
function name(parameter1, parameter2, ... parameterN) {
  // 함수 본문
}
```
### 지역 변수
> 함수 내에서 선언한 변수인 지역 변수(local variable)는 함수 안에서만 접근 가능
```js
function showMessage() {
  let message = "안녕하세요!"; // 지역 변수

  alert( message );
}

showMessage(); // 안녕하세요!

alert( message ); // ReferenceError: message is not defined (message는 함수 내 지역 변수이기 때문에 에러 발생)
```

### 외부 변수
> 함수 내부에서 함수 외부의 변수인 외부 변수(outer variable)에 접근 및 수정 가능
```js
let userName = 'John';

function showMessage() {
  let message = 'Hello, ' + *!*userName*/!*;
  alert(message);
}

showMessage(); // Hello, John
```
- 외부 변수는 지역 변수가 없는 경우에만 사용 가능
	- 함수 내부에 외부 변수와 동일한 이름을 가진 변수가 선언되었다면, 내부 변수는 외부 변수를 가림

### 매개변수(parameter)
> 매개변수(parameter)를 이용하면 임의의 데이터를 함수 안에 전달 가능
> 매개변수는 _인자(parameter)_ 라고 불리기도 함
```js
function showMessage(from, text) { // 인자: from, text
  alert(from + ': ' + text);
}

showMessage('Ann', 'Hello!'); // Ann: Hello!
showMessage('Ann', "What's up?"); // Ann: What's up? 
```

-   매개변수는 함수 선언 방식 괄호 사이에 있는 변수입니다(선언 시 쓰이는 용어).
-   인수는 함수를 호출할 때 매개변수에 전달되는 값입니다(호출 시 쓰이는 용어).

### 기본 값
> 자바스크립트에선 함수를 호출할 때마다 매개변수 기본값을 평가함
```js
function showMessage(from, text = "no text given") {
  alert( from + ": " + text );
}

showMessage("Ann"); // Ann: no text given
```

### 반환 값
```js
function sum(a, b) {
  return a + b;
}

let result = sum(1, 2);
alert( result ); // 3
```
- 실행 흐름이 지시자 `return`을 만나면 함수 실행은 즉시 중단되고 함수를 호출한 곳에 값을 반환
- `return`문이 없거나 `return` 지시자만 있는 함수는 `undefined`를 반환
	- `return undefined`와 동일하게 동작

### 함수 이름짓기
> 함수가 어떤 동작을 하는지 축약해서 설명해 주는 동사를 접두어로 붙여 함수 이름을 만드는 게 관습

-   `"get…"`  -- 값을 반환함
-   `"calc…"`  -- 무언가를 계산함
-   `"create…"`  -- 무언가를 생성함
-   `"check…"`  -- 무언가를 확인하고 불린값을 반환함

```js
showMessage(..)     // 메시지를 보여줌
getAge(..)          // 나이를 나타내는 값을 얻고 그 값을 반환함
calcSum(..)         // 합계를 계산하고 그 결과를 반환함
createForm(..)      // form을 생성하고 만들어진 form을 반환함
checkPermission(..) // 승인 여부를 확인하고 true나 false를 반환함
```

## 16. 함수 표현식
```js
// 함수 선언
let sayHi = function() {
  alert( "Hello" );
};

// 함수 표현식
let sayHi = function() {
  alert( "Hello" );
};
```

### 콜백 함수
```js
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "동의하십니까?",
  function() { alert("동의하셨습니다."); },
  function() { alert("취소 버튼을 누르셨습니다."); }
);
```
- 이름 없이 선언한 함수는 _익명 함수(anonymous function)_ 라고 함
 
### 함수 표현식 vs 함수 선언문

- _함수 선언문:_ 함수는 주요 코드 흐름 중간에 독자적인 구문 형태로 존재
	- 함수 선언문이 정의되기 전에도 호출 가능
	- 자바스크립트는 스크립트를 실행하기 전, 준비단계에서 전역에 선언된 함수 선언문을 찾고, 해당 함수를 생성
	- 스크립트는 함수 선언문이 모두 처리된 이후에서야 실행됨
	- 엄격 모드에서 함수 선언문이 코드 블록 내에 위치하면 해당 함수는 블록 내 어디서든 접근할 수 있지만, 블록 밖에서는 함수에 접근하지 못함
- _함수 표현식:_ 함수는 표현식이나 구문 구성(syntax construct) 내부에 생성됨
	- 실제 실행 흐름이 해당 함수에 도달했을 때 함수를 생성

## 17. 화살표 함수 기본
```js
let func = (arg1, arg2, ...argN) => expression
```
- 인수가 하나밖에 없다면 인수를 감싸는 괄호를 생략 가능
```js
let double = n => n * 2;

alert( double(3) ); // 6
```
