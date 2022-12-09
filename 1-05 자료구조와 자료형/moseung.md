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

### reduce
```js run
let value = arr.reduce(function(accumulator, item, index, array) {
  // ...
}, [initial]);
```

함수의 인수는 다음과 같습니다.

* accumulator -- 이전 함수 호출의 결과. initial은 함수 최초 호출 시 사용되는 초깃값을 나타냄(옵션)
* item -- 현재 배열 요소
* index -- 요소의 위치
* array -- 배열

## 5 = 6 iterable
반복 가능한(iterable, 이터러블) 객체는 배열을 일반화한 객체입니다. 이터러블 이라는 개념을 사용하면 어떤 객체에든 for..of 반복문을 적용할 수 있습니다.<br>
이터러블 객체의 핵심은 '관심사의 분리(Separation of concern, SoC)'에 있습니다.
```js run
let range = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },

  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    } else {
      return { done: true };
    }
  }
};

for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
```
### 문자열은 이터러블입니다
그래서 아래처럼 for .. of 사용가능
```js run
for (let char of "test") {
  // 글자 하나당 한 번 실행됩니다(4회 호출).
  alert( char ); // t, e, s, t가 차례대로 출력됨
}

```

### 명시적 호출
```js run
let str = "Hello";

// for..of를 사용한 것과 동일한 작업을 합니다.
// for (let char of str) alert(char);

*!*
let iterator = str[Symbol.iterator]();
*/!*

while (true) {
  let result = iterator.next();
  if (result.done) break;
  alert(result.value); // 글자가 하나씩 출력됩니다.
}
```

### Array.from
범용 메서드 Array.from는 이터러블이나 유사 배열을 받아 '진짜' Array를 만들어줍니다. 이 과정을 거치면 이터러블이나 유사 배열에 배열 메서드를 사용할 수 있습니다.

## 5 - 7 Map,Set
### Map
맵(Map)은 키가 있는 데이터를 저장한다는 점에서 객체와 유사합니다. 다만, 맵은 키에 다양한 자료형을 허용한다는 점에서 차이가 있습니다. 즉 객체와 다르게 Map의 key에는 다양한 자료형이 들어갈 수 있다.ex) 1,true
* new Map() -- 맵을 만듭니다.
* map.set(key, value) -- key를 이용해 value를 저장합니다.
* map.get(key) -- key에 해당하는 값을 반환합니다. key가 존재하지 않으면 undefined를 반환합니다.
* map.has(key) -- key가 존재하면 true, 존재하지 않으면 false를 반환합니다.
* map.delete(key) -- key에 해당하는 값을 삭제합니다.
* map.clear() -- 맵 안의 모든 요소를 제거합니다.
* map.size -- 요소의 개수를 반환합니다.

객체를 키로 사용할 수 있다는 점은 맵의 가장 중요한 기능 중 하나입니다. 객체에는 문자열 키를 사용할 수 있습니다. 하지만 객체 키는 사용할 수 없습니다.

### Set
`셋(Set)`은 중복을 허용하지 않는 값을 모아놓은 특별한 컬렉션입니다. 셋에 키가 없는 값이 저장됩니다.
* `new Set(iterable)` -- 셋을 만듭니다. `이터러블` 객체를 전달받으면(대개 배열을 전달받음) 그 안의 값을 복사해 셋에 넣어줍니다.
* `set.add(value)` -- 값을 추가하고 셋 자신을 반환합니다.
* `set.delete(value)` -- 값을 제거합니다. 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 `true`, 아니면 `false`를 반환합니다.
* `set.has(value)` -- 셋 내에 값이 존재하면 `true`, 아니면 `false`를 반환합니다.
* `set.clear()` -- 셋을 비웁니다.
* `set.size` -- 셋에 몇 개의 값이 있는지 세줍니다.

```js run
let set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// 어떤 고객(john, mary)은 여러 번 방문할 수 있습니다.
set.add(john);
set.add(pete);
set.add(mary);
set.add(john);
set.add(mary);

// 셋에는 유일무이한 값만 저장됩니다.
alert( set.size ); // 3

for (let user of set) {
  alert(user.name); // // John, Pete, Mary 순으로 출력됩니다.
}
```

## 5 - 8 weakmap-weakset
배열이 메모리에 남아있는 한, 배열의 요소인 이 객체도 메모리에 남아있게 됩니다. 이 객체를 참조하는 것이 아무것도 없더라도 말이죠.
```js run
let john = { name: "John" };

let array = [ john ];

john = null; // 참조를 null로 덮어씀

*!*
// john을 나타내는 객체는 배열의 요소이기 때문에 가비지 컬렉터의 대상이 되지 않습니다.
// array[0]을 이용하면 해당 객체를 얻는 것도 가능합니다.
*/!*
alert(JSON.stringify(array[0]));

```


위크맵은 맵과 유사한 컬렉션입니다. 위크맵을 구성하는 요소의 키는 오직 객체만 가능합니다. 키로 사용된 객체가 메모리에서 삭제되면 이에 대응하는 값 역시 삭제됩니다.<br>

위크셋은 셋과 유사한 컬렉션입니다. 위크셋엔 객체만 저장할 수 있습니다. 위크셋에 저장된 객체가 도달 불가능한 상태가 되면 해당 객체는 메모리에서 삭제됩니다.

## 5 - 9 keys-values-entries
일반 객체엔 다음과 같은 메서드를 사용할 수 있습니다.

* Object.keys(obj) -- 객체의 키만 담은 배열을 반환합니다.
* Object.values(obj) -- 객체의 값만 담은 배열을 반환합니다.
* Object.entries(obj) -- [키, 값] 쌍을 담은 배열을 반환합니다.

```js run
let user = {
  name: "John",
  age: 30
};
Object.keys(user) = ["name", "age"]
Object.values(user) = ["John", 30]
Object.entries(user) = [ ["name","John"], ["age",30] ]

```

### 객체 변환하기
```js run
let prices = {
  banana: 1,
  orange: 2,
  meat: 4,
};

*!*
let doublePrices = Object.fromEntries(
  // 객체를 배열로 변환해서 배열 전용 메서드인 map을 적용하고 fromEntries를 사용해 배열을 다시 객체로 되돌립니다.
  Object.entries(prices).map(([key, value]) => [key, value * 2])
);
*/!*
//doubleprices는 value가 2배인 객체

alert(doublePrices.meat); // 8
```

## 5 - 10 destructuring-assignment
### 배열 분해하기
```js run
배열이 어떻게 변수로 분해되는지 예제를 통해 살펴봅시다.

// 이름과 성을 요소로 가진 배열
let arr = ["Bora", "Lee"]

*!*
// 구조 분해 할당을 이용해
// firstName엔 arr[0]을
// surname엔 arr[1]을 할당하였습니다.
let [firstName, surname] = arr;
*/!*

alert(firstName); // Bora
alert(surname);  // Lee
```
배열의 요소를 직접 변수에 할당하는 것보다 코드 양이 줄어든다는 점만 다릅니다.
```js
// let [firstName, surname] = arr;
let firstName = arr[0];
let surname = arr[1];
```
쉼표를 사용하면 필요하지 않은 배열 요소를 버릴 수 있습니다.

```js run
*!*
// 두 번째 요소는 필요하지 않음
let [firstName, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];
*/!*

alert( title ); // Consul
```

두 번째 요소는 생략되었지만, 세 번째 요소는 `title`이라는 변수에 할당된 것을 확인할 수 있습니다. 할당할 변수가 없기 때문에 네 번째 요소 역시 생략되었습니다.<br>
배열뿐만 아니라 모든 이터러블(iterable, 반복 가능한 객체)에 구조 분해 할당을 적용할 수 있습니다.

```js
let [a, b, c] = "abc"; // ["a", "b", "c"]
let [one, two, three] = new Set([1, 2, 3]);
```
### 객체 분해
```js run
let options = {
  title: "Menu",
  width: 100,
  height: 200
};

*!*
let {title, width, height} = options;
*/!*

alert(title);  // Menu
alert(width);  // 100
alert(height); // 200
```

프로퍼티가 없는 경우를 대비하여 =을 사용해 기본값을 설정하는 것도 가능합니다. 아래와 같이 말이죠.

```js run
let options = {
  title: "Menu"
};

*!*
let {width = 100, height = 200, title} = options;
*/!*

alert(title);  // Menu
alert(width);  // 100
alert(height); // 200
```

중첩 객체와 콜론을 조합하면 좀 더 복잡한 구조 분해도 가능합니다.

```js run
let options = {
  title: "My menu",
  items: ["Item1", "Item2"]
};

*!*
function showMenu({
  title = "Untitled",
  width: w = 100,  // width는 w에,
  height: h = 200, // height는 h에,
  items: [item1, item2] // items의 첫 번째 요소는 item1에, 두 번째 요소는 item2에 할당함
}) {
*/!*
  alert( `${title} ${w} ${h}` ); // My Menu 100 200
  alert( item1 ); // Item1
  alert( item2 ); // Item2
}

showMenu(options);
```

## 5 - 11 Date
Date 객체의 메서드를 사용하면 연, 월, 일 등의 값을 얻을 수 있습니다.

* getFullYear() : 연도(네 자릿수)를 반환합니다.
* getMonth() : 월을 반환합니다(0 이상 11 이하).
* getDate() : 일을 반환합니다(1 이상 31 이하). 어! 그런데 메서드 이름이 뭔가 이상하네요.
* getHours(), getMinutes(), getSeconds(), getMilliseconds() : 시, 분, 초, 밀리초를 반환합니다.

## 5 - 12 json
복잡한 객체를 다루고 있다고 가정해 봅시다. 네트워크를 통해 객체를 어딘가에 보내거나 로깅 목적으로 객체를 출력해야 한다면 객체를 문자열로 전환해야 할겁니다.<br>

JSON (JavaScript Object Notation)은 값이나 객체를 나타내주는 범용 포맷으로, RFC 4627 표준에 정의되어 있습니다. JSON은 본래 자바스크립트에서 사용할 목적으로 만들어진 포맷입니다. 그런데 라이브러리를 사용하면 자바스크립트가 아닌 언어에서도 JSON을 충분히 다룰 수 있어서, JSON을 데이터 교환 목적으로 사용하는 경우가 많습니다. 특히 클라이언트 측 언어가 자바스크립트일 때 말이죠. 서버 측 언어는 무엇이든 상관없습니다.
* JSON.stringify -- 객체를 JSON으로 바꿔줍니다.
* JSON.parse -- JSON을 객체로 바꿔줍니다.

```js run
let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  wife: null
};

*!*
let json = JSON.stringify(student);
*/!*

alert(typeof json); // 문자열이네요!

alert(json);
*!*
/* JSON으로 인코딩된 객체:
{
  "name": "John",
  "age": 30,
  "isAdmin": false,
  "courses": ["html", "css", "js"],
  "wife": null
}
*/
*/!*
```

### replacer로 원하는 프로퍼티만 직렬화하기
```js run
let room = {
  number: 23
};

let meetup = {
  title: "Conference",
  participants: [{name: "John"}, {name: "Alice"}],
  place: room // meetup은 room을 참조합니다.
};

room.occupiedBy = meetup; // room references meetup

alert( JSON.stringify(meetup, *!*['title', 'participants']*/!*) );
// {"title":"Conference","participants":[{},{}]}
```

### space로 가독성 높이기
```js run
let user = {
  name: "John",
  age: 25,
  roles: {
    isAdmin: false,
    isEditor: true
  }
};

alert(JSON.stringify(user, null, 2));
/* 공백 문자 두 개를 사용하여 들여쓰기함:
{
  "name": "John",
  "age": 25,
  "roles": {
    "isAdmin": false,
    "isEditor": true
  }
}
*/

/* JSON.stringify(user, null, 4)라면 아래와 같이 좀 더 들여써집니다.
{
    "name": "John",
    "age": 25,
    "roles": {
        "isAdmin": false,
        "isEditor": true
    }
}
*/
```

### Json.parse
JSON.parse를 사용하면 JSON으로 인코딩된 객체를 다시 객체로 디코딩 할 수 있습니다.
```js run
// 문자열로 변환된 배열
let numbers = "[0, 1, 2, 3]";

numbers = JSON.parse(numbers);

alert( numbers[1] ); // 1
```
### reviver
```js run
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str);

*!*
alert( meetup.date.getDate() ); // 에러! date는 Date객체가 아니라 문자열이기떄문
*/!*
```
```js run
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

*!*
let meetup = JSON.parse(str, function(key, value) {
  if (key == 'date') return new Date(value);
  return value;
});
*/!*

alert( meetup.date.getDate() ); // 이제 제대로 동작하네요!
```
