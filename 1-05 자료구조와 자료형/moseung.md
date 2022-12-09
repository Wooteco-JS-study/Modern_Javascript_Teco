# 5강 자료구조와 자료형
## 5 - 1 primitive-methods
자바스크립트는 원시값(문자열, 숫자 등)을 마치 객체처럼 다룰 수 있게 해줍니다. 원시값에도 객체에서처럼 메서드를 호출할 수 있다. ex) string.toUpperCase() string은 객체가 아닌데 객체의 메소드처럼 접근이 가능함
### 원시값을 객체처럼 사용하기
#### 방법
문자열 str은 원시값이므로 원시값의 프로퍼티(toUpperCase)에 접근하는 순간 특별한 객체가 만들어집니다. 이 객체는 문자열의 값을 알고 있고, toUpperCase()와 같은 유용한 메서드를 가지고 있습니다.
메서드가 실행되고, 새로운 문자열이 반환됩니다(alert 창에 이 문자열이 출력됩니다).특별한 객체는 파괴되고, 원시값 str만 남습니다.<br>
단 null과 undefined는 불가능하다.

## 5 - 2 number
### 숫자를 입력하는 다양한 방법
```js run
let billion = 1e9;  // 10억, 1과 9개의 0
------
let billion = 1000000000 //e표기법으로 가능
------
let ms = 1e-6;// 0.000001 1에서 왼쪽으로 6번이동.
```
#### 16진수 2진수 8진수
```js run
let a = 0b11111111; // 255의 2진수
let b = 0o377; // 255의 8진수
let c =  0xff ; // 255의 16진수
```

### toString
num.toString(base) 메서드는 base진법으로 num을 표현한 후, 이를 문자형으로 변환해 반환합니다.
```js run
let num = 255;

alert( num.toString(16) );  // ff
alert( num.toString(2) );   // 11111111
```

### 어림수 구하기
* Math.floor : 소수점 첫째 자리에서 내림(버림). 3.1은 3, -1.1은 -2가 됩니다.
* Math.ceil : 소수점 첫째 자리에서 올림. 3.1은 4, -1.1은 -1이 됩니다.
* Math.round : 소수점 첫째 자리에서 반올림. 3.1은 3, 3.6은 4, -1.1은 -1이 됩니다.
* Math.trunc (Internet Explorer에서는 지원하지 않음) : 소수부를 무시. 3.1은 3이 되고 -1.1은 -1이 됩니다.

### isNaN과 isFinite
* isNaN(value) -- 인수를 숫자로 변환한 다음 NaN인지 테스트함
* isFinite(value) -- 인수를 숫자로 변환하고 변환한 숫자가 NaN/Infinity/-Infinity가 아닌 일반 숫자인 경우 true를 반환함

## 5 - 3 string
작은따옴표와 큰따옴표는 기능상 차이가 없습니다. 그런데 백틱엔 특별한 기능이 있습니다. 표현식을 ${…}로 감싸고 이를 백틱으로 감싼 문자열 중간에 넣어주면 해당 표현식을 문자열 중간에 쉽게 삽입할 수 있죠. 이런 방식을 템플릿 리터럴(template literal)이라고 부릅니다.
### template literal
```js run
function sum(a, b) {
  return a + b;
}

alert(`1 + 2 = ${sum(1, 2)}.`); // 1 + 2 = 3. 이처럼 동적으로 할당가능
```

### 특수 기호
![image](https://user-images.githubusercontent.com/103626175/206750713-056d773d-3a1b-4ee4-883f-afc3bad0da41.png)

### 문자열의 길이
```js run
const a = "모승";
console.log(a.length);//2
```

### 문자열 찾기
* str.indexOf
* includes, startsWith, endsWith

### 부분 문자열 추출하기
substring, substr, slice

## 5 - 4 array
순서가 있는 컬렉션을 저장할 때 쓰는 자료구조인 배열.<br>
이렇게 배열은 자바스크립트의 일곱 가지 원시 자료형에 해당하지 않고, 원시 자료형이 아닌 객체형에 속하기 때문에 객체처럼 동작합니다.
```js run
let fruits = ["바나나"]

let arr = fruits; // 참조를 복사함(두 변수가 같은 객체를 참조)

alert( arr === fruits ); // true

arr.push("배"); // 참조를 이용해 배열을 수정합니다.

alert( fruits ); // 바나나,배 - 요소가 두 개가 되었습니다. //객체 동작 원리와 똑같다 참조값이 같은
```
### 성능
push와 pop은 빠르지만 shift와 unshift는 느립니다.<br>
**이유**
* 인덱스가 0인 요소를 제거합니다.
* 모든 요소를 왼쪽으로 이동시킵니다. 이때 인덱스 1은 0, 2는 1로 변합니다.
* length 프로퍼티 값을 갱신합니다.

### 반복문
for문은 배열을 순회할 때 쓰는 가장 오래된 방법입니다. 순회시엔 인덱스를 사용합니다.
```js run
let arr = ["사과", "오렌지", "배"];

*!*
for (let i = 0; i < arr.length; i++) {
*/!*
  alert( arr[i] ); //사과, 오렌지,배
}
 ```
## 5 - 5 array-methods
### splice
배열에서 요소를 하나만 지우고 싶다면 어떻게 해야 할까요?
```js run
arr.splice(index[, deleteCount, elem1, ..., elemN])
```
### slice
arr.slice는 arr.splice와 유사해 보이지만 훨씬 간단합니다.
```js run
arr.slice([start], [end])
```

### forEach
arr.forEach는 주어진 함수를 배열 요소 각각에 대해 실행할 수 있게 해줍니다.

### 배열탐색
indexOf, lastIndexOf와 includes

### find
```js run
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);

alert(user.name); // John
```
