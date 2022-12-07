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
연산자는 이미 다들 알고 있을것 같아서 특이점만 정리했습니다.
### 연산자 우선순위
![image](https://user-images.githubusercontent.com/103626175/206088161-ff0796db-19c0-4510-825f-deafd52fb89f.png)
### 복합 할당 연산자
```
let n = 2;
n = n + 5;
n = n * 2;
-----------
let n =2;
n+=5;
m*=2;
//위아래 값이 똑같다. 여기서 연산자`+`와 할당연산자`=`를 같이 쓰는걸 복합할당 연산자라고한다.
```

## 1 - 9 comparison
### 비교 연산자
자바스크립트에서 기본 수학 연산은 아래와 같은 문법을 사용해 표현할 수 있습니다.<br>
* 보다 큼·작음: a > b, a < b
* 보다 크거나·작거나 같음: a >= b, a <= b
* 같음(동등): a == b. 등호 =가 두 개 연달아 오는 것에 유의하세요. a ​​= b와 같이 등호가 하나일 때는 할당을 의미합니다.
* 같지 않음(부등): 같지 않음을 나타내는 수학 기호 ≠는 자바스크립트에선 a != b로 나타냅니다. 할당연산자 = 앞에 느낌표 !를 붙여서 표시합니다.
* ==은 얕은비교 ===은 깊은비교고 ==은 지양합니다.

## 1 - 10 if,else
### if, else
```js run
if(a==="사람"){
console.log("사람입니다")
}else if(a==="동물"){
console.log("동물입니다")
}else{
console.log("식물입니다.")
}
```
위와 같이 소괄호안에 조건을 체크해서 분기별로 다른 문을 실행한다.
### 조건부 연산자 '?'
조건부 연산자 ? 는 조건에 따라 다른변수를 할당할떄 사용한다.<br>
예를들어
```js run
const compare = a>b;
const result = a?"a가 큼":"b가 큼"
```
#### 위처럼 분기별로 다른 값을 할당해야할떄 사용해야지 if문을 대신해서 사용하면 오히려 가독성을 해친다.

### 다중 연산
```js run
let age = prompt('나이를 입력해주세요.', 18);

let message = (age < 3) ? '아기야 안녕?' :
  (age < 18) ? '안녕!' :
  (age < 100) ? '환영합니다!' :
  '나이가 아주 많으시거나, 나이가 아닌 값을 입력 하셨군요!';

alert( message );
```
위처럼 다중?을 사용해서 연산이 가능하다.

## 1 - 11 logical-operators
논리 연산자라고 하며 ||(OR), &&(AND), !(NOT)이 있습니다.

### || OR
위의 연산자는 Boolean으로 봤을때 여러 인자가 하나라도 true라면 true를 리턴한다.
```js run
const a = true;
const b = false;
const c = true;
console.log(a||b||c); //true
```

여기서 중요한것은 ||연산자는 첫 번째 truthy를 찾는다는것이다.
```js run
const a = false;
const b = false;
const c = "모승";
console.log(a||b||c); //"모승"
```
만약에 위의 값에서 b==="중간이용"이라면 console창에서 "중간이용"을 출력할것이다.

### && AND
위의 연산자는 OR과 반대이고 여러 인자중 하나라도 False라면 False를 리턴한다.<br>
그리고 OR과 다르게 첫 번째 falsy를 찾으며 모든값이 true라면 맨 마지막인자를 리턴한다.
```js run
const a = false;
const b = "b";
const c = "모승";
console.log(a && b && c); //false
```
만약에 a값이 논리적으로 true인 값이라면 c의 값이 출력된다. "모승"

<br>
&&가 ||보다 우선순위가 높다. 먼저 계산한다.
```js run
      const a = false;
      const b = "b";
      const c = "c";
      const d = "d";
      console.log(a && b || c && d);
```
위에서 &&가 우선이기 때문에 먼저 연산하면 false || "d"가 되고 이를 다시 연산하면 "d"가 출력된다.

### ! not
NOT 연산자는 인수를 하나만 받고, 다음 순서대로 연산을 수행합니다.

* 피연산자를 불린형(true / false)으로 변환합니다.
* 1에서 변환된 값의 역을 반환합니다.
```js run
const a = "모승";
console.log(!a); // "모승"은 문자열이기에 true로 변환되고 해당값의 역이기 때문에 false가 정답이다.
```

!NOT 연산자는 모든 논리연산자중에서 우선순위가 제일높다.

## 1 - 12 nullish-coalescing-operator
### nullish 병합 연산자 ??
nullish 병합 연산자(nullish coalescing operator) ??를 사용하면 짧은 문법으로 여러 피연산자 중 그 값이 '확정되어있는' 변수를 찾을 수 있습니다.
```run js
let firstName = null;
      let lastName = undefined;
      let nickName = "바이올렛";
      console.log(firstName ?? lastName ?? nickName); // "바이올렛"
```
위에서 nickName을 제외한 값은 정의되어 있지 않기 때문에 "바이올렛"이 리턴된다. 만약 nickName=null로 정의되있지 않다면 마지막에 정의되있지않은 값인 null이 리턴된다.

### '??'와 '||'의 차이
위에서 보면 ||연산자와 ??연산자가 얼핏 똑같아 보이는데 간단한 예로들자면
```run js
let firstName = null;
      let lastName = false;
      let nickName = "바이올렛";
      console.log(firstName ?? lastName ?? nickName); // false
```
위에서 ??가 아니라 ||연산자를 사용할경우 "바이올렛"이 리턴되는데 ??연산자를 사용할경우 false가 리턴된다.(false로 값이 정의되있기 때문)

### ??의 우선순위는 낮다
??의 우선순위는 낮기떄문에 해당 연산자를 쓸경우 왠만하면 ()안에 값을 정의해주는게 좋다.
```js run
let height = null;
let width = null;

// 괄호를 추가!
let area = (height ?? 100) * (width ?? 50);

alert(area); // 5000
```
그리고 연관성 이슈때문에 &&나 ||와 함께 ??는 사용불가능하다.

## 1 - 13 while-for
### while
while반복문은 소괄호 안에 조건이 false가 될때까지 코드블럭내에 문을 실행합니다.
```js run
let i = 0;
while (i < 3) { // 0, 1, 2가 출력됩니다.
  alert( i );
  i++;
}
```
반복문 본문이 한 번 실행되는 것을 반복(iteration, 이터레이션) 이라고 부릅니다. 위 예시에선 반복문이 세 번의 이터레이션을 만듭니다.

### 'do..while' 반복문
do..while 문법은 조건이 truthy 인지 아닌지에 상관없이, 본문을 최소한 한 번이라도 실행하고 싶을 때만 사용해야 합니다
```js run
let i = 0;
do {
  alert( i );
  i++;
} while (i < 0); // 0이 출력된다 일반적인 while문이었으면 출력안된다.
```
### for
for문은 워낙 유명하기때문에 특이점만 짚어보겠습니다.
```js run
let i = 0;

for (; i < 3;) {
  alert( i++ );
}
```
위처럼 부분적으로 생략가능하다

### 반복문 빠져나오기
#### break
반복문 안에서 break를 마주하면 해당 반복문을 종료합니다.
```js run
let sum = 0;
for(i=1;i<3;i++){
if(sum===3){
break;
}
sum+=i;
}
```
위와같이 진행되면 i=2일떄까지만 반복되고 3일때는 종료되서 결국 sum===3;

#### continue
반복문 안에서 continue를 마주치면 해당 문을 건너뛰고 다음부터 진행한다.
```js run
let sum = 0;
for(i=1;i<3;i++){
if(i===2){
break;
}
sum+=i;
}
```
위와같이 진행되면 i=2일때 해당문을 건너뛰고(이터레이션을 건너뛰고) sum===4;

#### label break
label break는 중첩 반복문 안에서 원하는 반복문을 종료하고 싶을떄 사용합니다.
```js run
first:for(i=0;i<3;i++){
        second:for(j=0;j<5;j++){
          if(j===2) break first;
        }
      }
```
위와 같이 작성시 j===2가 되면 상위 반복문인 first가 종료됩니다.

## 1 - 14 switch
복수의 if 조건문은 switch문으로 바꿀 수 있습니다. switch문을 사용한 비교법은 특정 변수를 다양한 상황에서 비교할 수 있게 해줍니다. 코드 자체가 비교 상황을 잘 설명한다는 장점도 있습니다.
```js run
const x = "value1" 
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]
  case 'value2':  // if (x === 'value2')
    ...
    [break]
  default:
    ...
    [break] // default는 필수가 아님
}
```

## 1 - 15 function-basics
### 함수
스크립트를 작성하다 보면 유사한 동작을 하는 코드가 여러 곳에서 필요할 때가 많습니다. 즉 재사용을 위함<br>
함수는 이미 잘 알기 때문에 추가적인 부분을 적었습니다.
#### 기본값
함수인자에 아무값도 들어오지 않았다면 기본값을 사용 가능합니다. 최신 문법입니다.
```js run
function test(input="기본이용"){
console.log(input);//"기본이용"출력
}
test();
```
### 함수 이름짓기
함수는 어떤 동작을 수행하기 위한 코드를 모아놓은 것입니다. 따라서 함수의 이름은 대개 동사입니다. 함수 이름은 가능한 한 간결하고 명확해야 합니다. 함수가 어떤 동작을 하는지 설명할 수 있어야 하죠. 코드를 읽는 사람은 함수 이름만 보고도 함수가 어떤 기능을 하는지 힌트를 얻을 수 있어야 합니다.<br>
이 외에 아래와 같은 접두어를 사용할 수 있습니다.
* "get…" -- 값을 반환함
* "calc…" -- 무언가를 계산함
* "create…" -- 무언가를 생성함
* "check…" -- 무언가를 확인하고 불린값을 반환함

### 함수 == 주석
함수는 간결하고, 한 가지 기능만 수행할 수 있게 만들어야 합니다. 함수가 길어지면 함수를 잘게 쪼갤 때가 되었다는 신호로 받아들이셔야 합니다. 함수를 쪼개는 건 쉬운 작업은 아닙니다. 하지만 함수를 분리해 작성하면 많은 장점이 있기 때문에 함수가 길어질 경우엔 함수를 분리해 작성할 것을 권유합니다.
<br>
함수를 간결하게 만들면 테스트와 디버깅이 쉬워집니다. 그리고 함수 그 자체로 주석의 역할까지 합니다!

## 1 - 16 function-expressions
### 함수 표현식
자바스크립트는 함수를 특별한 종류의 값으로 취급합니다. 다른 언어에서처럼 "특별한 동작을 하는 구조"로 취급되지 않습니다.
```js run
function sayHi() {
  alert( "Hello" );
}
------
let sayHi = function(){
alert("Hello")
}
---
function sayHi() {
  alert( "Hello" );
}
sayHi=2;
//sayHi는 2로 재할당된다.
```
위 아래가같으며 sayHi는 let으로 선언된 값이기 때문에 sayHi는 다른 원시값으로 재 할당이 가능합니다. 

### 콜백 함수
함수를 값처럼 전달하는 예시, 함수 표현식에 관한 예시입니다.
```js run
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}
*/!*

function showOk() {
  alert( "동의하셨습니다." );
}

function showCancel() {
  alert( "취소 버튼을 누르셨습니다." );
}

// 사용법: 함수 showOk와 showCancel가 ask 함수의 인수로 전달됨
ask("동의하십니까?", showOk, showCancel);
----------
ask(
  "동의하십니까?",
  function() { alert("동의하셨습니다."); },
  function() { alert("취소 버튼을 누르셨습니다."); }
); // 이처럼 이름 없이 등록한 함수는 익명함수라고 합니다.
```
위에서 showOk,showCancel은 콜백 혹은 콜백함수라고 부릅니다.
### 함수 표현식 vs 함수 선언문
함수 표현식은 실제 실행 흐름이 해당 함수에 도달했을 때 함수를 생성합니다. 따라서 실행 흐름이 함수에 도달했을 때부터 해당 함수를 사용할 수 있습니다.
```js run
      b();
      function b() {
        console.log("b");
      }
      a();
      let a = function () {
        console.log("a");
      };
```
위에서 함수 b는 함수 표현식입니다.<br>
자바스크립트는 스크립트를 실행하기 전, 준비단계에서 전역에 선언된 함수 선언문을 찾고, 해당 함수를 생성합니다. 그래서 b값은 호출이 됩니다.<br>
하지만 a는 함수 선언식으로 해당 함수에 도달했을때부터 사용가능합니다. 즉 해당함수를 선언한 아래에서부터 사용가능하므로 a는 에러를 띄웁니다.

## 1 - 17 arrow-functions-basics
### 화살표 함수 기본
함수 표현식보다 단순하고 간결한 문법으로 함수를 만들 수 있는 방법이 있습니다.
```js run
let func = function(arg1, arg2, ...argN) {
  return expression;
};
-----------
let func = (arg1, arg2, ...argN) => expression
//위의 함수를 아래 arrow함수로 간단하게 선언가능하다.
```
화살표 함수는 본문이 한 줄인 함수를 작성할 때 유용합니다. 본문이 한 줄이 아니라면 다른 방법으로 화살표 함수를 작성해야 합니다.

* 중괄호 없이 작성: (...args) => expression -- 화살표 오른쪽에 표현식을 둡니다. 함수는 이 표현식을 평가하고, 평가 결과를 반환합니다.
* 중괄호와 함께 작성: (...args) => { body } -- 본문이 여러 줄로 구성되었다면 중괄호를 사용해야 합니다. 다만, 이 경우는 반드시 return 지시자를 사용해 반환 값을 명기해 주어야 합니다.


