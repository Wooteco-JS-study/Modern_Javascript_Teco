### ch1 : hello, world

<br/>

##### script 태그

- <code>script</code>태그를 이용하면 자바스크립트 프로그램을 HTML 문서 대부분의 위치에 삽입할 수 있다.
- 브라우저는 스크립트 태그를 마난면 안의 코드를 자동으로 처리한다.

```html
<!DOCTYPE html>
<html>
  <body>
    <p>스트립트 전</p>
    *!*
    <script>
      alert("hello, world!");
    </script>
    */!*
    <p>스크립트 후</p>
  </body>
</html>
```

##### 외부 스크립트

> 자바스크립트 코드 양이 많은 경우 파일로 소분하여 저장할 수 있다.

```html
/* 예시 */
<script src="/path/to/script.js"></script>
```

- 위의 스크립트 태그의 경로는 루트에서부터 파일이 위치한 절대 경로를 나타낸다.

절대경로 : 최상위 디렉토리부터 해당 파일까지 경유한 모든 경로를 전부 기입하는 방식. 외부 파일을 참조할 때 주로 사용한다. <br/>
장점으로는 루트 디렉토리를 항상 포함하기 때문에 외부에서도 절대경로를 이용하여 파일 연결이 가능하고, 어디에서나 해당 파일을 찾을 수 있다. <br/>
단점으로는 서버 주소가 달라지면 절대경로로 설정된 주소를 모두 수정해야하며, 상대경로에 비해 로딩속도가 느리다(DNS조회를 통해 해당파일을 찾기 때문에)

상대경로 : 현재 파일이 존재하는 디렉토리를 기준으로 해당 파일까지의 위치를 작성한 경로이다. 내부 파일을 연결할 때 주로 사용한다.<br/>
장점으로는 서버주소가 달라져도 이전 서버와 디렉토리 구조만 같다면 경로수정을 하지않아도 된다.

- 복수의 스크립트를 사용하기 위해서는 스크립트 태그를 여러 개 사용하면 된다.
- 스크립트가 길어지면 별개의 분리된 파일로 만들어 저장한다.

  - 별도 파일에 작성하면 브라우저가 스크립트를 다운받아 캐시에 저장하기 때문에, 여러 페이지에서 동일한 스크립트를 사용하는 경우, 캐시로부터 스크립트를 가져와 사용하기 때문에 트래픽이 절약되고 웹 페이지의 실제 속도가 빨라진다.

- <code>script</code>태그는 src속성과 내부 코드를 동시에 가지지 못한다.

```html
<script src="files.js">
  alert(1);
</script>
```
### ch2 : structure

<br/>

##### 문(statement)

> 어떤 작업을 수행하는 문법 구조와 명령어를 의미한다.

- 세미콜론으로 구분한다.
- 코드의 가독성을 높이기 위해 각 문은 서로 다른 줄에 작성하는 것이 일반적이다.

```js
console.log("hi");
console.log("every one!");
```

##### 세미콜론

- 줄 바꿈이 있다면 세미콜론 생략 가능
- 하지만 세미콜론 넣는 것을 권장

##### 주석(code-comments)

- 자바스크립트 엔진은 주석을 무시하기 때문에 주석의 위치는 실행에 영향을 주지 않는다.

```js
// 이 주석은 한 줄을 다 차지한다.
alert("hello");
/*
여러줄을 사용할때는 다음과 같이 이용한다. 
*/
alert("world");
```
### ch3 : 엄격모드

<br/>

> ES5에서 새로운 기능이 추가되고 기존 기능 중 일부가 변경되면서 하위 호환성 문제가 생길 수 있는 가능성이 생겼다. 그래서 변경사항 대부분은 ES5의 기본모드에서는 활성화되지 않도록 설계했다. 대신 <code>use Strict</code>라는 특별한 지시자를 사용하여 엄격모드를 활성화 했을 때만 이 변경사항이 활성화되게 해놓았다.

##### use Strict

- 지시자 <code>'use strict'</code>가 스크립트 최상단에 오면 스크립트 전체가 모던한 방식으로 동적한다.

```js
"use strict";
//이 코드는 모던한 방식으로 실행된다.
```

- 모던 자바스크립트는 클래스와 모듈을 제공한다. 이 둘을 사용하면 use strict가 자동으로 적용된다.

### ch4 : 변수와 상수

##### 변수

> 변수는 데이터를 저장할 때 쓰이는 '이름이 붙은 저장소'

- <code>let</code> 키워드로 생성

```js
let age;
age = 23;

let age = 23; // 이렇게도 선언 가능하다.
let name = "bae",
  age = "26",
  msg = "hi"; // 한 줄에 여러 변수를 선언하는 것도 가능하다.
```

- 같은 변수를 여러 번 선언하면 에러가 발생한다.

```js
let count = 0;
let count = 30; // error
```

##### 변수 명명 규칙

- 자바스크립트에는 2가지 제약 사항이 있다.

  1. 변수명에는 오직 문자와 숫자, 그리고 <code>$</code> ,<code> \_</code>만 들어갈 수 있다.
  2. 첫 글자는 숫자가 들어올 수 없다.

- 여러 단어를 조합하여 변수명을 만들 때는 카멜 표기법이 흔히 사용된다.

```js
let apple;
let AppLE;
// 위의 두 변수는 서로 다른 변수이다.
```

- 최대한 서술적이고 간결하게 명명
- 자신만의 규칙이나 소속된 팀의 규칙을 따르자.
- 무엇을 하고 있는지 명확히 알고 있지 않은 경우 외에는 줄임말이나 a,b,c 같은 짧은 이름은 피하자

##### 상수

> 변화하지 않는 변수를 선언할때는 <code>const</code>를 사용한다.

- 상수는 재할당할 수 없으므로 상수를 변경하려고 하면 에러가 발생한다.

```js
const day = 3;
day = 4; // error
```

- 대문자 상수
  - 기억하기 힘든 값을 할당할 때 이용(하드코딩한 값의 별칭을 만들때)

```js
const COLOR_RED = "#F00";
const COLOR_ORANGE = "#FF7F00";
```
### ch5 : 자료형

- 자바스크립트는 자료의 타입은 있지만 변수에 저장되는 값의 타입은 언제든지 바꿀 수 있는 '동적 타입 언어'이다.

##### 숫자형

```js
let number = 123;
number = 12.345;
```

- 숫자형은 정수 및 부동소수점 숫자를 나타낸다.
- 일반적인 숫자 외에 <code>Infinity</code>, <code>-Infinity</code>, <code>NaN</code> 같은 특수 숫자값이 포함된다.
- <code>Infinity</code>는 무한대를 나타낸다.
  - 어느 숫자든 0으로 나누면 무한대를 얻을 수 있다.
  - <code>Infinity</code>를 직접 참조할 수 있다.

```js
alert(1 / 0);
alert(Infinity);
```

- <code>NaN</code>은 계산 중에 에러가 발생했다는 것을 나타내주는 값. 부정확하거나 정의되지 않은 수학 연산을 사용하여 계산 에러가 발생하면 <code>NaN</code>이 반환된다.

```js
alert("문자열" / 2); // NaN
alert("문자열" / 2 + 5); // NaN
```

##### BigInt

```js
// 끝에 n이 붙으면 BigInt형 자료이다.
const bigInt = 1231656486151321354849451321354894n;
```

##### 문자형

```js
const string = "hi";
const string2 = "hi";
const string3 = `hi`;
```

- 백틱으로 변수나 표현식으로 감싼후 <code>${...}</code>안에 넣어주면, 원하는 변수나 표현식을 문자열 중간에 쉽게 넣을 수 있다.

```js
const name = "seongkyu";
console.log(`hi, ${name}!`); // hi, seongkyu!
console.log(`result : ${10 + 10}`); //result : 20
```

##### boolean형

- true/false 값이 존재한다.
- 비교결과를 저장할 때도 사용된다.

```js
const nameFieldChecked = false;
const isGreater = 4 > 1;
alert(isGreater); // true
```

##### null 값

- 어느 자료형에도 속하지 않는 값
- 다른 언어와 다르게 자바스크립트에서의 <code>null</code>은 존재하지 않는 값(nothing), 비어있는 값(empty), 알 수 없는(unknown)값을 나타내는 데 사용한다.

##### undefined 값

- <code>null</code>값 처럼 자신만의 자료형을 형성한다.
- '값이 할당되지 않은 상태'를 나타낼 때 사용한다.
- 변수는 선언했으나, 값을 할당하지 않았다면 해당 변수에 <code>undefined</code>가 자동으로 할당된다.

##### 객체와 심볼

- 객체(object)형은 특수한 자료형이다.
- 객체형을 제외한 다른 자료형은 문자열이든 숫자든 한 가지만 표현할 수 있기 때문에 **원시(primitive) 자료형**이라고 한다. 반면 객체는 데이터 컬렉션이나 복잡한 개체를 표현할 수 있다.
- 심볼형은 객체의 고유 식별자를 만들 때 사용된다.

---

##### 요약

- 숫자형 : 정수, 부동 소수점 숫자 등의 숫자를 나타낼 때 사용
- bigint : 길이 제약 없이 정수를 나타낸다.
- 문자형 : 빈 문자열이나 글자들로 이루어진 문자열을 나타낼 때 사용한다.
- 불린형 : true, false를 나타낼 때 사용한다.
- null : null 값만을 위한 독립 자료형. null은 알 수 없는 값을 나타낸다.
- undefined : undefined값만을 위한 독립 자료형. 할당되지 않은 값을 나타낸다.
- 객체형 : 복잡한 데이터 구조를 표현할 때 사용한다.
- 심볼형 : 객체의 고유 식별자를 만들 때 사용한다.

##### typeof 연산자

- 인수의 자료형을 반환한다. 자료형에 따라 처리 방식을 다르게 하고 싶거나 변수의 자료형을 빠르게 알아내고자 할 때 유용하다.
- 2가지 형태의 문법을 지원한다.
  1. 연산자 : <code>typeof x</code>
  2. 함수 : <code>typeof(x)</code>

### ch6 : alert, prompt, confirm

##### alert

- <code>alert</code>는 사용자가 확인버튼을 누를 때까지 메시지를 보여주는 창이 계속 떠있는 함수다.
- 메시지가 있는 창을 모달창(modal window)이라고 부른다.

```js
alert("hello");
```

##### prompt

```js
result = prompt(title, [default]);
// title : 사용자에게 보여줄 문자열
// default : 입력 필드의 초기값(선택값)

//ex)
let age = prompt('나이를 입력해주세요.', 100);
alert(`당신의 나이는 ${age}세입니다.`); // 당신의 나이는 100세입니다.
```

- 함수가 실행되면 텍스트 메시지와 입력필드, 확인 및 취소 버튼이 있는 모달 창을 띄워준다.

##### confirm

```js
result = confirm(question);
// ex)
let isBoss = confirm("당신이 주인인가요?");
alert(isBoss); // 확인 버튼을 눌렀다면 true출력
```

- <code>confirm</code>함수는 매개변수로 받은 question과 확인 및 취소 버튼이 있는 모달창을 보여준다.
- 사용자가 확인버튼을 누르면 <code>true</code>, 그 외의 경우는 <code>false</code>를 반환한다.
### ch7 : 형변환

> 함수와 연산자에 전달되는 값은 대부분 적절한 자료형으로 자동 변환된다.

##### 문자형으로 변환

- 문자형으로의 형 변환은 문자형의 값이 필요할 때 일어난다.
- <code>alert</code>메서드는 매개변수로 문자형을 받기 때문에, <code>alert(value)</code>에서 value는 문자형이어야 한다. 만약, 다른 형의 값을 전달받으면 이 값은 문자형으로 자동 변환된다.
- <code>String(value)</code> 함수를 호출하여 전달받은 값을 문자열로 변환할 수도 있다.

```js
let value = true;
alert(typeof value); // boolean

value = String(value);
alert(typeof value); //string
```

##### 숫자형으로 변환

- 숫자형으로 변환은 수학과 관련된 함수와 표현식에서 자동으로 일어난다.

```js
alert("6" / "2"); // 3, 문자열이 숫자형으로 자동변환된 후 연산 수행
```

- <code>Number(value)</code>함수를 사용하면 주어진 값을 숫자형으로 명시하여 변환할 수 있다.

```js
let string = "123";
alert(typeof string); // string

let number = Number(string); // 문자열 '123'이 숫자 123으로 변환된다.
alert(typeof number); // number
```

- 숫자형 값을 사용하여 무엇을 하려고 할 때, 그 값을 문자 기반 form을 통해 입력받는 경우에는 위와 같이 명시적 형변환이 필수이다.
- 숫자 이외의 글자가 들어가 있는 문자열을 숫자형으로 변환하려고 하면 그 결과는 <code>NaN</code>이 된다.
- 숫자형으로 변환 시 적용되는 규칙
  - <code>undefined</code> -> <code>NaN</code>
  - <code>null</code> -> <code>0</code>
  - <code>true</code> and <code>false</code> -> <code>1</code> 과 <code>0</code>
  - <code>string</code> -> 문자열의 처음과 끝 공백이 제거. 공백 제거후 남아있는 문자열이 없다면 <code>0</code>, 그렇지 않다면 문자열에서 숫자를 읽는다. 변환에 실패하면 <code>NaN</code>이 된다.

##### 불린형으로 변환

- 불린형으로 변환 시 적용되는 규칙
  - <code>0</code>, 빈 문자열, <code>null</code>, <code>undefined</code>, <code>NaN</code>과 같이 직관적으로도 비어있다고 느껴지는 값들은 <code>false</code>가 된다.
  - 그 외의 값들은 <code>true</code>로 변환

```js
alert(Boolean(" ")); // 공백 문자열도 비어있지 않는 문자열이므로 true로 변환된다.
alert(Boolean("")); // false (빈문자열)
```


### ch8 : 기본 연산자

- 피연산자(operand) : 연산자가 연산을 수행하는 대상이다. <code> 6 \* 2</code>에서 <code>6</code>과<code>2</code>가 피연산자에 해당한다.
- 피연산자는 인수(argument)라는 용어로 불리기도 한다.
- 피연산자를 하나만 받는 연산자를 단항연산자라고 부른다.
- 2개의 피연산자를 받는 연산자를 이항 연산자라고 부른다.

##### 이항 연산자 '+'와 문자열 연결

- <code>+</code>연산자는 대개 숫자를 더한 결과를 반환한다.
- 그러나 피연산자로 문자열이 전달되면 문자열 병합을 한다.

```js
alert("1" + 2); // '12'
```

##### 단항 연산자 '+'와 숫자형으로의 변환

- <code>+</code>는 단항 연산자로도 활용이 가능하다.
- 피연산자가 숫자가 아닌 경우에 숫자형으로의 변환이 일어난다.
- 이항 연산자보다 우선순위가 높다.

```js
const x = 1;
console.log(+x); // 1
const y = -2;
console.log(+y); / -2
console.log(+true); // 1
console.log(+""); // 0

const day = '30';
const min = '10';
console.log( +day + +min); // 40
```

##### 값을 반환하는 할당 연산자

- 자바스크립트에서 대부분의 연산자는 값을 반환한다.
- <code>x = value</code>을 호출하면 <code>value</code>가 <code>x</code>에 쓰여지고, 이에 더하여 <code>value</code>가 반환된다.

```js
let a = 1;
let b = 2;
let c = 3 - (a = b + 1);
alert(a); // 3
alert(c); // 0
```

- 하지만 실 사용할때는 위와 같은 코드방식은 지양

##### 할당 연산자 체이닝

```js
let a, b, c;
a = b = c = 2 + 2;
console.log(a); // 4
console.log(b); // 4
console.log(c); // 4
```

- 위와 같이 할당 연산자를 여러 개 연결(체이닝)한 경우, 평가는 우측부터 진행된다. (c,b,a 순으로 값이 할당됨)

##### 증감 연산자

- <code>counter++</code> : 후위형(postfix form)
- <code>++counter</code> : 전위형(prefix form)
- 후위형과 전위형은 피연산자를 <code>1</code>만큼 증가시킨다는 점에서 동일한 일을 한다.
- 두 형의 차이는 반환 값을 사용할 때 드러난다.

```js
// 반환 값을 사용하지 않는 경우라면, 전위형과 후위형의 차이는 없다.
let counter = 0;
counter++;
++counter;
alert(counter); // 2, 위 두 라인은 동일 연산을 수행
```

```js
// 값을 증가시키고 난 후, 증가한 값을 바로 사용하려면 전위형 증가 연산자를 사용
let counter = 0;
alert(++counter); // 1
```

```js
// 값을 증가시키지만, 증가 전의 기존값을 사용하려면 후위형 증가 연산자를 사용
let counter = 0;
alert(counter++); // 0
```

##### 쉼표 연산자

- 코드를 짧게 쓰려는 의도로 가끔 사용된다.
- 여러 표현식을 코드 한 줄에서 평가할 수 있도록 한다. 이때, 표현식 각각이 모두 평가되지만, 마지막 표현식의 평가 결과만 반환된다.

```js
const a = (1 + 2, 3 + 4); // 7이 a에 들어감
```

- 여러 동작을 하나의 줄에서 처리하려는 복잡한 구조에서 사용

```js
for (a = 1, b = 3, c = a * b; a < 10; a++) {}
```

- 코드 가독성은 구리다.


### ch9 : 비교 연산자

##### 불린형 반환

- <code>true</code>가 반환되면, '참'을 의미한다.
- <code>false</code>가 반환되면, '거짓'을 의미한다.

```js
// 반환된 불린값을 변수에 넣어 할당할 수 있다.
const result = 5 > 4;
console.log(result); // true
```

##### 문자열 비교

- '사전'순으로 문자열을 비교한다.
- 실제 단어를 사전에 실을 때 단어를 구성하는 문자 하나하나를 비교하여 등재 순서를 정하는 것처럼 자바스크립트도 문자열을 구성하는 문자 하나하나를 비교해가며 문자열을 비교한다.

```js
console.log("Z" > "A"); // true
console.log("Glow" > "Glee"); // true
console.log("Bee" > "Be"); // true
```

- 문자열 비교 시 적용되는 알고리즘은 다음과 같다.

  1. 두 문자열의 첫 글자를 비교한다.
  2. 첫 번째 문자열의 첫 글자가 다른 문자열의 첫 글자보다 크면(작으면), 첫 번째 문자열이 두 번째 문자열보다 크다고(작다고)결론 내고 비교를 종료한다.
  3. 두 문자열의 첫 글자가 같으면 두 번째 글자를 1번과 같은 방법으로 비교한다.
  4. 글자 간 비교가 끝날 때까지 이 과정을 반복한다.
  5. 비교가 종료되었고, 문자열의 길이도 같다면 두 문자열은 동일하다고 결론을 낸다. 비교가 종료되었지만 두 문자열의 길이가 다르면 길이가 긴 문자열이 더 크다고 결론 낸다.

- 자바스크립트는 대/소문자를 따진다.

```js
console.log("a" > "A"); // true
// 자바스크립트 내부에서 사용하는 유니코드에서는 소문자가 대문자보다 더 큰 인덱스를 갖기때문에
```

##### 다른 형을 가진 값 간의 비교

- 비교하려는 값의 자료형이 다르면 자바스크립트는 값들을 숫자형으로 바꾸고 비교한다.

```js
console.log("01" == 1); // true, 문자열 '01'이 숫자 1로 변환 후 비교
console.log(false == 0); // true
```

##### 일치 연산자

- 동등 연산자(equality operator) <code>==</code>은 <code>0</code>과 <code>false</code>를 구별하지 못한다.

```js
console.log(0 == false); // true
console.log("" == false); // true
```

- 일치 연산자(strict equality operator) <code>===</code>를 사용하면 형 변환 없이 값을 비교할 수 있다.
- 피연산자 간의 형이 다를 경우 false를 반환한다.

```js
console.log(0 === false); // false, 피연산자의 형이 다르다 .
```

- 비교결과가 명확하기 때문에 에러가 발생할 확률을 줄여준다.

##### null이나 undefined와 비교하기

```js
console.log(null == undefined); // true
console.log(null === undefined); // false
```

- 산술 연산자나 기타 비교 연산자를 사용하여 <code>null</code>과 <code>undefined</code>를 비교하면 숫자형으로 변환된다.
  - <code>null</code> -> <code>0</code>
  - <code>undefined</code> -><code>NaN</code>

##### null vs 0

```js
console.log(null > 0); // false
console.log(null == 0); // false
console.log(null >= 0); // true
```

##### 비교가 불가능한 undefined

```js
console.log(undefined > 0); // false
console.log(undefined < 0); // false
console.log(undefined == 0); // false
```

- undefined가 NaN으로 변환되는데(숫자형으로의 변환), NaN이 피연산자인 경우 비교 연산자는 항상 false를 반환한다.

### ch10 : if-else

##### if문

- <code>if(...)</code>문은 괄호 안에 들어가는 조건을 평가하는데, 그 결과가 <code>true</code>일 시 코드 블록이 실행된다.

```js
const year = prompt("ECMAScript-2015 명세는 몇 년도에 출판되었을까요?", "");
if (year == 2015) alert("정답입니다.");
```

##### 불린형으로의 변환

- <code>0</code>, <code>""</code>, <code>null</code>, <code>undefined</code>, <code>NaN</code>은 불린형으로 변환 시 모두 <code>false</code>가 된다. 이런 값들은 'falsy'값이라고 부른다.
- 이 외의 값은 불린형으로 변환시 <code>true</code>가 되므로 'truthy'값이라고 부른다.

##### else

- <code>if</code>문에는 <code>else</code>절을 붙일 수 있다. <code>else</code>뒤에 이어지는 코드 블록은 조건이 거짓일 때 실행된다.

##### 조건부 연산자 '?'

- 조건에 따라 다른 값을 변수에 할당해줘야 할 경우

```js
let accessAllowed;
let age = prompt("나이를 입력해주세요.", "");
if (age > 18) {
  accessAllowed = true;
} else {
  accessAllowed = false;
}
alert(accessAllowed);
// ? 연산자로 더 짧고 간결하게 변형
let accessAllowed = age > 18 ? true : false;
```

##### 다중 '?'

- <code>?</code>를 여러 개 연결하여 복수 조건을 처리한다.

```js
let age = prompt("나이를 입력해주세요.", 18);
let message =
  age < 3
    ? "아기야 안녕?"
    : age < 18
    ? "안녕!"
    : age < 100
    ? "환영합니다"
    : "나이가 아주 많으시거나, 나이가 아닌 값을 입력했습니다.";
alert(message);
```

##### 부적절한 '?'

```js
const company = prompt("자바스크립트는 어떤 회사가 만들었을까요?", "");
company == "Netscape" ? alert("정답입니다") : alert("오답입니다");
```

- 개발자 입장에서는 if문을 사용할때보다 코드 길이가 짧아진다는 점때문에 사용할 수 있으나 가독성이 떨어진다.
- 물음표 연산자 <code>?</code>는 조건에 따라 반환 값을 달리하려는 목적으로 만들어졌다. 여러 분기를 만들어 처리할 때는 <code>if</code>사용


### ch11 : 논리연산자

> 자바스크립트에는 3종류의 논리연산자 <code>||</code>(OR), <code>&&</code>(AND), <code>!</code>(NOT)이 있다.

##### <code>||</code> (OR)

```js
result = a || b;
```

- OR 연산자는 불린 값을 조작하는 데 쓰인다. 인수 중 하나라도 <code>true</code>이면 <code>true</code>을 반환하고 아니면 <code>false</code>를 반환한다.

##### 첫 번째 truthy를 찾는 OR 연산자

- 자바스크립트에서만 제공하는 논리연산자 OR의 '추가'기능

```js
// OR 연산자와 피연산자가 여러 개인 경우
result = value1 || value2 || value3;
```

- 가장 왼쪽 피연산자부터 시작하여 오른쪽으로 나아가며 피연산자를 평가한다.
- 각 피연산자를 불린형으로 변환한다. 변환 후 그 값이 <code>true</code>면 연산을 멈추고 해당 피연산자의 변환 전 원래 값을 반환한다.
- 피연산자 모두를 평가한 경우(모든 피연산자가 <code>false</code>로 평가되는 경우)에는 마지막 피연산자를 반환한다.
- <code>||</code>연산자를 여러 개 체이닝하면 첫 번째 truthy를 반환한다.

```js
alert(1 || 0); // 1 (1은 truthy)
alert(null || 1); // 1 (1은 truthy)
alert(undefined || null || 0); // 0(모두 falsy므로, 마지막 값을 반환한다. )
```

```js
// 변수 또는 표현식으로 구성된 목록에서 첫 번째 truthy 얻기

const firstName = "";
const lastName = "";
const nickName = "바이올렛";
alert(firstName || lastName || nickName || "익명"); // 바이올렛 , 만약 모든 변수가 falsy면 '익명'이 출력되었을 것
```

##### &&(AND)

```js
result = a && b;
```

- 두 피연산자가 모두 참일 때 <code>true</code>를 반환한다. 그 외의 경우에는 <code>false</code>를 반환한다.
- OR연산자와 마찬가지로 AND연산자의 피연산자도 타입에 제약이 없다.

##### 첫 번째 falsy를 찾는 AND 연산자 &&

- AND연산자는 아래와 같은 순서로 동작

  - 가장 왼쪽 피연산자부터 시작하여 오른쪽으로 나아가며 피연산자를 평가한다.
  - 각 피연산자는 불린형으로 변환된다. 변환 후 값이 <code>false</code>이면 평가를 멈추고 해당 피연산자의 변환 전 원래 값을 반환한다.
  - 피연산자 모두가 평가되는 경우(모든 피연산자가 <code>true</code>로 평가되는 경우)에는 마지막 피연산자가 반환된다.

- OR연산자의 알고리즘과 유사하지만, AND연산자가 첫번째 falsy를 반환하는 반면, OR은 첫 번째 truthy를 반환한다.

##### !(NOT)

- 논리 연산자 NOT은 느낌표 <code>!</code>를 써서 만들 수 있다.

```js
result = !value;
```

- NOT 연산자는 인수를 하나만 받고, 다음 순서대로 연산을 수행한다.
  - 피연산자를 불린형으로 변환한다.
  - 위에서 변환된 값의 역을 반환한다.

```js
alert(!true); // false
```

- NOT을 두개 연달아 사용하면 값을 불린형으로 변환할 수 있다.

```JS
alert(!!'non-empty string'); // true
alert(!!null); // false
```


### ch12 : 병합연산자

> 병합연산자 <code>??</code>를 사용하면 짧은 문법으로 여러 피연산자 중 그 값이 '확정되어있는' 변수를 찾을 수 있다.

```js
// nulish 병합 연산자 ?? 없이 사용하는 경우
x = a !== null && a !== undefined ? a : b;

// 병합연산자를 사용하는 경우
x = a ?? b;
```

- <code>a ?? b</code>의 평가 결과
  - <code>a</code>가 <code>null</code>도 아니고 <code>undefined</code>도 아니면 <code>a</code>
  - 그 외의 경우는 <code>b</code>

##### ?? 와 || 차이

- <code>??</code>는 <code>||</code>와 유사해 보이지만 중요한 차이점이 있다.
  - <code>||</code>는 첫 번째 truthy값을 반환
  - <code>??</code>는 첫 번째 정의된 값을 반환

```js
height = height ?? 100;
// height에 값이 정의되지 않은 경우 height에 100이 할당된다.
```

```js
let height = 0;
alert(height || 100); // 100
alert(height ?? 100); // 0
```

- <code>height || 100 </code>은 <code>height</code>에 <code>0</code>을 할당했지만 <code>0</code>을 falsy한 값으로 취급했기 때문에 <code>null</code>이나 <code>undefined</code>를 할당한 것과 동일하게 처리한다. 따라서 <code>height || 100</code>의 평가 결과는 <code>100</code>이다.
- 그러나 <code>height ?? 100</code>의 평가 결과는 <code>height</code>가 정확히 <code>null</code>나 <code>undefined</code>일 경우에만 <code>100</code>이 된다.
- 이런 특징으로 높이처럼 0이 할당될 수 있는 변수를 사용하여 기능을 개발할때 ||보다 ??가 적합하다.

- 그러나 자바스크립트에서 규정한 안정성 관련 이슈로 인해 <code>??</code>는 <code>&&</code>나 <code>||</code>와 함께 사용하지 못한다.
- 괄호를 사용하면 제약을 피할 수 있다.

```js
let x = 1 && 2 ?? 3; // 신택스 에러
let x = (1&&2) ?? 3; // 2
```

### ch13 : while과 for 반복문

##### while

```js
// condition이 참인 동안 code가 계속 돌아간다.
while (condition) {
  // code
}
```

- 조건이 계속 truthy하다면 무한 반복이 된다.

##### do-while

```js
do {
  // code
} while (condition);
```

- code가 먼저 실행되고, 조건을 확인하여 truthy인 동안 반복이 된다.(최소 1번은 실행된다.)

##### for

```js
for (begin; condition; step) {
  // code
}
/*
begin : 반복문에 진입할 때 단 한번 실행된다. (ex : i = 0;)
condition : 반복마다 해당 조건을 확인. false이면 반복문을 멈춘다. (ex : i < 3;)
code : condition이 truthy일 동안 계속 실행된다. 
step : 각 반복문의 코드가 실행된 이후에 실행된다. 
*/
```

##### 구성 요소 생략하기

- for 반복문이 시작될 때 아무것도 할 필요가 없으면 <code>begin</code>부분을 생략하는 것이 가능하다.

```js
let i = 0;
for (; i < 3; i++) {
  alert(i);
}

// step 부분도 생략이 가능하다.
for (; i < 3; ) {
  alert(i++);
}

// 모든 구성요소를 생략할 수도 있다.
for (;;) {
  // 끊임없이 본문 실행
}
```

##### 반복문 빠져나오기

- 반복문의 조건이 falsy가 되면 반복문은 종료된다.
- <code>break</code>문을 사용하면 언제든 원하는 때에 빠져나올 수 있다.

```js
let sum = 0;
while (true) {
  let value = +prompt("숫자를 입력하세요.", "");
  if (!value) break;
  sum += value;
}
alert("합계:" + sum);
```

- 사용자가 아무것도 입력하지 않거나 prompt창에 있는 cancel버튼을 누르면 활성화 된다.
- 반복문의 시작지점이나 끝 지점에서 조건을 확인하는 것이 아닌 본문 가운데 혹은 본문 여러곳에서 조건을 확인해야 하는 경우에 '무한 반복문 + break'조합을 사용하면 좋다.

##### 다음 반복으로 넘어가기 (continue)

- <code>continue</code>는 전체 반복문을 멈추지 않는다. 대신 현재 실행중인 이터레이션을 멈추고 반복문이 다음 이터레이션을 강제로 실행하도록한다.
- <code>continue</code>는 현재 반복을 종료시키고 다음 반복으로 넘어가고 싶을 때 사용한다.

```js
for (let i = 0; i < 10; i++) {
  if (i % 2 == 0) continue; // 조건이 참이면 남아있는 본문은 실행x
  alert(i); // 1, 3, 5, 7, 9가 차례대로 출력
}

// 위에 있는 예시와 같은 동작을 하지만, 중첩레벨이 하나 늘어난다.
for (let i = 0; i < 10; i++) {
  if (i % 2) {
    alert(i);
  }
}
```

- 삼항 연산자에서는 continue를 사용할 수 없다.

```js
(i > 5) ? alert(i) : continue; // 문법 에러 발생
```

##### break/continue와 레이블

- 여러 개의 중첩 반복문을 한 번에 빠져나와야 하는 경우

```js
for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    let input = prompt(`(${i}, ${j}의 값`, "");
    // 여기에서 멈춰서 아래쪽의 완료를 출력하려면 ?
  }
}
alert("완료");
```

- 레이블(label)을 사용하면 빠져나올 수 있다.

```js
labelName: for(...){
    // code
}
```

- 반복문 안에서 break<labelName>문을 사용하면 레이블에 해당하는 반복문을 빠져나올 수 있다.

```js
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    let input = prompt(`${i}, ${j}의 값`, "");
    if (!input) break outer;
    // code
  }
}
alert("완료");
```

- <code> break outer</code>는 <code>outer</code>라는 레이블이 붙은 반복문을 찾고, 해당 반복문을 빠져나오게 한다.

```js
// 별도의 줄에 쓰는 것도 가능하다.
outer: for (let i = 0; i < 3; i++) {
  // code
}
```

                             
### ch14 : switch

- 복수의 <code>if</code>조건문을 <code>switch</code>문으로 바꿀 수 있다.
- <code>switch</code>문을 사용한 비교법은 특정 변수를 다양한 상황에서 비교할 수 있게 해준다. 코드 자체가 비교 상황을 잘 설명한다는 장점이 있다.

##### 문법

```js
switch (x) {
  case "value1":
    break;
  case "value2":
    break;
  default:
    break;
}
```

- 변수 <code>x</code>의 값과 첫 번째 <code>case</code>문의 값 <code>'value1'</code>를 일치 비교한 후, 두 번째 <code>case</code>문의 값 <code>'value2'</code>와 비교한다.
- <code>case</code>문에서 변수 <code>x</code>의 값과 일치하는 값을 찾으면 해당 <code>case</code>문의 아래 코드가 실행된다. 이때, <code>break</code>문을 만나거나 <code>switch</code>문이 끝나면 코드의 실행은 멈춘다.
- 값과 일치하는 <code>case</code>문이 없으면, <code>default</code>문 아래의 코드가 실행된다.(<code>default</code>가 있는경우)

- 실행하려는 코드가 같으면 아래 처럼 묶을 수 있다.

```js
const a = 3;
switch (a) {
  case 4:
    alert("계산이 맞습니다");
    break;
  case 3:
  case 5:
    alert("계산이 틀리다");
    break;
  default:
    alert("계산결과가 이상하다");
}
```
### ch15 : function-basics

- 함수 선언방식을 사용하면 함수를 만들 수 있다.
- 함수의 주요 용도 중 하나는 중복 코드 피하기이다.

```js
function showMessage() {
  alert("안녕");
}
```

##### 지역 변수

- 함수 내에서 선언한 변수인 지역변수(local variable)는 함수 안에서만 접근할 수 있다.

```js
function showMessage() {
  let message = "안녕하세요"; // 지역 변수
  alert(message);
}
showMessage();
alert(message); // error
```

##### 외부 변수

- 함수 내부에서 함수 외부의 변수인 외부변수(outer variable)에 접근/수정할 수 있다.
- 외부 변수는 지역 변수가 없는 경우에만 사용할 수 있다.

```js
let userName = "John";

function showMessage() {
  userName = "Bob"; // (1) 외부 변수를 수정함

  let message = "Hello, " + userName;
  alert(message);
}

alert(userName); // 함수 호출 전이므로 *!*John*/!* 이 출력됨

showMessage();

alert(userName); // 함수에 의해 *!*Bob*/!* 으로 값이 바뀜
```

##### 매개 변수

- 매개변수(parameter)를 이용하면 임의의 데이터를 함수 안에 전달할 수 있다. 인자라고 부르기도 함
- 함수의 매개변수에 전달된 값을 인수(argument)라고 부르기도 한다.

```js
function showMessage(from, text) {
  alert(from + ":" + text);
}
const from = "Ann";
showMessage(from, "hello");
```

##### 기본값

- 함수 호출 시 매개변수에 인수를 전달하지 않으면 그 값은 <code>undefined</code>가 된다.

```js
function showMessage(from, text = "no text given") {
  alert(from + ":" + text);
}
showMessage("Ann"); // Ann: no text given
```

- 매개변수에 값을 전달해도 그 값이 <code>undefined</code>와 엄격히 일치한다면 기본값이 할당된다.

##### 매개변수 기본 값을 설정할 수 있는 또 다른 방법

```js
// 함수 선언 후에 매개변수 기본값을 설정하는 경우
function showMessage(text) {
  if (text === undefined) {
    text = "빈 문자열";
  }
  alert(text);
}
showMessage();

// ||를 사용하는 경우
function showMessage(text) {
  text = text || "빈 문자열";
}

// ??를 사용하는 경우
function showCount(count) {
  alert(count ?? "unknown");
}
showCount(0); // 0
showCount(); // unknown
showCount(null); // unknown
```

##### 반환 값

- 함수를 호출했을 때, 함수를 호출한 그곳에 특정 값을 반환하게 할 수 있다.

```js
function sum(a, b) {
  return a + b;
}
const result = sum(1, 2);
alert(result); // 3
```

- <code>return</code>를 만나면 함수 실행은 즉시 중단되고 함수를 호출한 곳에 값을 반환한다.

```js
// return; 만 반환하면 undefined를 반환한다.
function doNothing() {
  return;
}
alert(doNothing() === undefined); // true
```

##### 함수 이름짓기

- 함수는 어떤 동작을 수행하기 위한 코드를 모아놓은 곳
- 가능한 간결하고 명확해야 하며, 함수 이름만 보고도 어떤 기능을 하는지 힌트를 얻을 수 있어야한다.
- 대게 동사로 이름을 짓는다.
- 함수는 이름에 언급되어 있는 동작을 정확히 수행해야 하고 그 이외의 동작은 수행해서는 안된다.

  - getAge 함수는 나이를 얻어오는 동작만 수행해야 한다. (출력해주는 동작은 들어가면 안된다.)
  - createForm 함수는 form을 만들고 이를 반환하는 동작만 해야한다. (그 외 동작[추가,수정 등]은 들어가면 안된다. )

- 예외인 경우 : $(제이쿼리), \_(lodash)

##### 함수 == 주석

- 함수는 간결하고, 한 가지 기능만 수행하도록 만들어야 한다.
- 함수가 간결하면 테스트와 디버깅이 쉬워진다.
- 그리고 함수 그 자체로 주석의 역할까지 한다.

```js
function showPrimes(n) {
  nextPrime: for (let i = 2; i < n; i++) {
    for (let j = 2; j < i; j++) {
      if (i % j == 0) continue nextPrime;
    }
    alert(i); // 소수
  }
}
```

```js
function showPrimes(n) {
  for (let i = 2; i < n; i++) {
    if (!isPrime(i)) continue;

    alert(i); // a prime
  }
}

function isPrime(n) {
  for (let i = 2; i < n; i++) {
    if (n % i == 0) return false;
  }
  return true;
}
```
### ch16 : function-expressions

- 함수 선언 방식 외에 함수 표현식을 사용하여 함수를 만들 수 있다.

```js
const sayHi = function () {
  alert("hi");
};
```

- 함수를 생성하고 변수에 값을 할당하는 것처럼 함수가 변수에 할당되어있다.
- 함수가 어떤 방식으로 만들어졌는지에 관계없이 함수는 값이고, 따라서 변수에 할당 가능하다.

```js
function sayHi() {
  alert("hi");
}
const func = sayHi; // (1)
func(); // hi
sayHi(); // hi
```

- (1)에서 sayHi를 func에 복사하였는데, 괄호가 없어 sayHi 함수 그 자체를 복사했으며, 만약 괄호가 있었다면 함수호출결과가 func에 저장되었을 것이다.

##### 콜백 함수

```js
// 함수는 반드시 question을 해야하고, 사용자의 답변에 따라 yes()나 no()를 호출한다.
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}
function showOk() {
  alert("동의");
}
function showCancel() {
  alert("취소");
}
// 사용법 : 함수 showOk와 showCancel이 ask 함수의 인수로 전달
ask("동의하시나요?", showOk, showCancel);
```

- 함수를 함수의 인수로 전달하고, 필요하다면 인수로 전달한 그 함수를 나중에 호출(called back)하는 것이 콜백 함수의 개념

##### 함수 표현식 vs 함수 선언문

1. 문법의 차이
   - 함수 선언문 : 함수는 주요 코드 흐름 중간에 독자적인 구문 형태로 존재
   - 함수 표현식 : 함수는 표현식이나 구문 구성 내부에 생성된다.

```js
// 함수 선언문
function sum(a, b) {
  return a + b;
}

// 함수 표현식
let sum = function (a, b) {
  return a + b;
};
```

2. 자바스크립트 엔진이 언제 함수를 생성하는 지
   - 함수 선언문 : 함수 선언문이 정의되기 전에도 호출할 수 있다.
   - 함수 표현식 : 실제 실행 흐름이 해당 함수에 도달했을 때 함수를 생성
   - 전역 함수 선언문은 스크립트 어디에 있든지 어디에서든 사용할 수 있다.

```js
sayHi("john");
function sayHi(name) {
  alert(`hi, ${name}`);
}
```

- sayHi는 스크립트 실행 준비단계에서 생성되므로, 스크립트 내 어디섣느 접근할 수 있다.

```js
sayHi("john"); // error
const sayHi = function (name) {
  alert(`hi, ${name}`);
};
```

- 함수 표현식은 실행 흐름이 표현식에 도착해야 만들어진다.

3. 스코프
   - 엄격 모드에서 함수 선언문이 코드 블록 내에 위치하면 해당 함수는 블록 내 어디섣느 접근 가능하다. 그러나 블록 밖에서는 함수에 접근하지 못한다.

```js
// 함수 선언문을 사용하면 의도대로 코드가 동작하지 않음
let age = prompt("나이를 알려주세요.", 18);

// 조건에 따라 함수를 선언함
if (age < 18) {
  function welcome() {
    alert("안녕!");
  }
} else {
  function welcome() {
    alert("안녕하세요!");
  }
}

// 함수를 나중에 호출합니다.
welcome(); // Error: welcome is not defined
```

```js
let age = prompt("나이를 알려주세요.", 18);

let welcome;

if (age < 18) {
  welcome = function () {
    alert("안녕!");
  };
} else {
  welcome = function () {
    alert("안녕하세요!");
  };
}

welcome(); // 제대로 동작합니다.
```

### ch17 : arrow-functions-basics

##### 화살표 함수

```js
const sum = (a, b) => a + b;
const sayHi = () => alert("하이");
const double = (n) => n * 2;
```

##### 본문이 여러 줄인 화살표 함수

- 평가해야할 표현식이나 구문이 여러 개인 경우 중괄호 안에 코드를 넣어주어야한다.
- <code>return</code>지시자를 사용하여 명시적으로 결과값 반환한다.
