# 2강 first-steps
## 1 - 1 Hello world

웹 페이지에 스크립트를 추가하는 방법.
```
<html>

<body>

  <p>스크립트 전</p>

*!*
  <script>
    alert( 'Hello, world!' );
  </script>
*/!*

  <p>스크립트 후</p>

</body>

</html>
```
위 코드처럼 html태그내에 script태그를 이용해서 삽입도 가능하다.<br>
하지만 저런 방법은 가독성을 해치고, 최근에는 JS에 많은 내용이 들어가 있기떄문에 JS파일로 소분하여 불러온다.

```
<script src="/path/to/script.js"></script> 
```
위처럼 파일 위치로 가능하고
```
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
```
URL로도 가능하다.
```
<script *!*src*/!*="file.js">
  alert(1); 
</script>
```
위같은 코드에서 alert(1)은 무시된다.

## 1 - 2 structure
코드블럭 만드는 방법을 매운다
### 문 (door아님)
문(statement)은 어떤 작업을 수행하는 문법 구조(syntax structure)와 명령어(command)를 의미합니다.<br>
```
alert('Hello'); alert('World');
```
위 코드처럼 ;을 첨가하면 하나의 문으로 나눠진것 하지만 가독성을 위해 암묵적으로 세미콜론 이후 줄을 나누는걸 명시한다.
```
alert('Hello');
alert('World');
```
줄 바꿈이 있다면 세미콜론(semicolon)을 생략할 수 있습니다.
```
alert('Hello')
alert('World')
```
하지만 줄 바꿈으로 문을 나눴더라도, 문 사이엔 세미콜론을 넣는 것이 좋습니다. 이를 권장하고 있습니다.

### 주석
시간이 흐름에 따라 자바스크립트 프로그램은 더욱더 복잡해졌습니다. 이로 인해 무슨 일이 왜 벌어지고 있는지를 설명해주는 주석(comment) 의 필요성이 요구되었습니다. 하지만 주석은 코드엔 영향을 끼치지 않는다.

#### 한줄주석
한줄짜리주석은 //(두개의 슬래시)로 시작된다.<br>
여러줄 주석은 /* 무슨내용*/와 같이 작성하며 여러줄에 걸쳐서 가능하다.
```
/*
안녕하세요~~
저
는
alert("good")
*/
```

## 1 - 3 strict-mode
### 엄격모드
ES5에서는 새로운 기능이 추가되고 기존 기능 중 일부가 변경되었습니다. 기존 기능을 변경하였기 때문에 하위 호환성 문제가 생길 수 있겠죠? 그래서 변경사항 대부분은 ES5의 기본 모드에선 활성화되지 않도록 설계되었습니다. 대신 use strict라는 특별한 지시자를 사용해 엄격 모드(strict mode)를 활성화 했을 때만 이 변경사항이 활성화되게 해놓았습니다.
### use strict
위에서 말한 엄격모드는 JS내에서 "use strict"를 타이핑하면 사용 가능하다.그리고 이 use strict는 파일상단에 위치해야된다.
### 그래서 use strict 꼭 사용해야하나 ?
'use strict'를 꼭 사용해야 하나요
모던 자바스크립트는 '클래스'와 '모듈'이라 불리는 진일보한 구조를 제공합니다(클래스와 모듈에 대해선 당연히 뒤에서 학습할 예정입니다). 이 둘을 사용하면 use strict가 자동으로 적용되죠. 따라서 이 둘을 사용하고 있다면 스크립트에 "use strict"를 붙일 필요가 없습니다.

결론은 이렇습니다. 코드를 클래스와 모듈을 사용해 구성한다면 "use strict"를 생략해도 됩니다. 그런데 아직은 이 둘을 배우지 않았으니 "use strict"를 귀한 손님처럼 모시도록 하겠습니다.

## 1 - 4 variables
### 변수와 상수
대다수의 자바스크립트 애플리케이션은 사용자나 서버로부터 입력받은 정보를 처리하는 방식으로 동작합니다. 아래와 같이 말이죠.

온라인 쇼핑몰 -- 판매 중인 상품이나 장바구니 등의 정보<br>
채팅 애플리케이션 -- 사용자 정보, 메시지 등의 정보<br>
변수는 이러한 정보를 저장하는 용도로 사용됩니다.

### 변수
변수(variable)는 데이터를 저장할 때 쓰이는 '이름이 붙은 저장소' 입며 자바스크립트에서는 `let`키워드를 사용한다.
```js run
let message;
message = 34; 

alert(message);//message = 34
```
아래와 같이 한줄에 여러 변수를 할당가능하지만 가독성을 위해서 권장하지 않는다.
```js run
let user = 'John', age = 25, message = 'Hello';
```
변수 두 개를 선언하고, 한 변수의 데이터를 다른 변수에 복사할 수도 있습니다.
```js run
let user;
let progamer = "모승";
user = progamer;
alert(user);//모승
alert(progamer);//모승
```
아래처럼 같은 변수를 두번 선언 불가능하다.
```js run
let user;
let user;//오류를 띄운다
```
### 변수 명명 규칙
* 변수명에는 오직 문자와 숫자, 그리고 기호 $와 _만 들어갈 수 있습니다.
* 첫 글자는 숫자가 될 수 없습니다.
* 변수명사이에 `-` 기호 불가능
* 소문자와 대문자 구분가능 `let apple` !== `let ApplE`

### 상수
변화하지 않는 변수를 선언할 땐, `let` 대신 `const`를 사용합니다.<br>
`const`로 선언한 상수는 재 할당이 불가능하다.
```
const user = "모승";
user = "승모"; // 불가능!
```

### 대문자 상수

기억하기 힘든 값을 변수에 할당해 별칭으로 사용하는 것은 널리 사용되는 관습입니다.<br>
이런 상수는 대문자와 밑줄로 구성된 이름으로 명명합니다.<br>
예시로 웹에서 사용하는 색상 표기법인 16진수 컬러 코드에 대한 상수를 한번 만들어보겠습니다.

```js run
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

// 색상을 고르고 싶을 때 별칭을 사용할 수 있게 되었습니다.
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```
위와같이 작성하면 가독성, 재사용성이 증가한다. 오타 감소

### 바람직한 변수명
* 변수명은 간결하고, 명확해야 합니다.
* 사람이 읽을 수 있는 이름을 사용
* 무엇을 하고 있는지 명확히 알고 있지 않을 경우 외에는 줄임말이나 `a`, `b`, `c`와 같은 짧은 이름은 피한다.
* 최대한 서술적이고 간결하게 명명해 주세요. `data`와 `value`는 나쁜 이름의 예시입니다.
* 자신만의 규칙이나 소속된 팀의 규칙을 따른다. 코드를 팀원간에 일치시킨다.


## 1 - 5 types
### 자료형
자바스크립트에는 타입이 여러가지가 있다.
#### 숫자형
```js run
let a = 2; 
let b = 1238901923701378192472874298471987489127401274014n;
```
일반적으로 숫자를 적으면 숫자형 타입이고 9007199254740991보다 큰값은 bigInt형이며 숫자뒤에 n을 붙여준다.
#### 문자형
```js run
let a = "모승";
let a = `일더하기 일은 귀요미가아니라 ${1+1}`
```
작은따옴표나 큰따옴표를 이용해서 string을 정의가능하고 `백틱(``)`키를 이용해서 변수나 식을 다룰 수 있다.
#### 불린형
```js run
let a = true;
let b = false;
let a = 4>1; //true;
```
#### null
```js run
let a = null;
```
null 값은 지금까지 소개한 자료형 중 어느 자료형에도 속하지 않는 값입니다. null 값은 오로지 null 값만 포함하는 별도의 자료형을 만듭니다.
#### undefined
```js run
let a ; //undefined;
let b = undefined;
```
undefined 값도 null 값처럼 자신만의 자료형을 형성합니다. undefined는 '값이 할당되지 않은 상태'를 나타낼 때 사용합니다.

#### 객체와 심볼
객체(object)형은 특수한 자료형입니다.<br>
객체형을 제외한 다른 자료형은 문자열이든 숫자든 한 가지만 표현할 수 있기 때문에 원시(primitive) 자료형이라 부릅니다. 반면 객체는 데이터 컬렉션이나 복잡한 개체(entity)를 표현할 수 있습니다.

#### typeof 연산자
typeof 연산자는 해당 변수의 타입을 알 수 있습니다.
```js run
typeof 0 // number
let b = "모승";
typeof b //string
```

## 1 - 6 alert-prompt-confirm
### alert
![image](https://user-images.githubusercontent.com/103626175/206084053-6838399d-fc37-497e-ace1-e7d5b400078e.png)

### prompt
![image](https://user-images.githubusercontent.com/103626175/206084015-8d100a88-d54c-4936-94ae-a3374072ec3f.png)

### confirm
![image](https://user-images.githubusercontent.com/103626175/206083973-4f658c8e-477d-434b-bd79-3f1c0444ed2e.png)

## 1 - 7 type-conversions
### 형 변환
함수와 연산자에 전달되는 값은 대부분 적절한 자료형으로 자동 변환됩니다. 이런 과정을 "형 변환(type conversion)"이라고 합니다.
### 문자형으로 변환
String(123) //"123"
### 숫자형으로 변환
Number("1234") //1234 <br>
단 숫자로 변환이 안되는값을 Numebr()에 인자로 넣으면 NaN을 띄운다.
### 불린형으로 변환
불린형으로 변환 시 적용되는 규칙은 다음과 같습니다.

* 숫자 0, 빈 문자열, null, undefined, NaN과 같이 직관적으로도 "비어있다고" 느껴지는 값들은 false가 됩니다.
* 그 외의 값은 true로 변환됩니다. 
```
 Boolean(1) //true
 Boolean(0) //false
```

## 1 - 8 operators
### 연산자


