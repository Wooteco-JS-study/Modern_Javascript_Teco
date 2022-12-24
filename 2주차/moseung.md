# 6강 advanced Function
## 5 - 1 recursion
문제 해결을 하다 보면 함수에서 다른 함수를 호출해야 할 때가 있습니다. 이때 함수가 자기 자신을 호출할 수도 있는데, 이를 재귀 라고 부릅니다.
### 두가지 사고방식
빈복문으로 합 구하기
```js run
function pow(x, n) {
  let result = 1;

  // 반복문을 돌면서 x를 n번 곱함
  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}

alert( pow(2, 3) ); // 8
```
재귀적인 방법으로 구하기
```js run
function pow(x, n) {
  if (n == 1) {
    return x;
  } else {
    return x * pow(x, n - 1);
  }
}

alert( pow(2, 3) ); // 8
```
즉 종합하면 재귀를 사용하면, 간결하고 유지보수가 쉬운 코드를 만들 수 내부 메모리를 사용하기떄문에 최대 재귀깊이 제한을 자바스크립트 엔진에서 둔다.

### 실행 컨텍스트와 스택

함수 내부에 중첩 호출이 있을 때는 아래와 같은 절차가 수행됩니다.

* 현재 함수의 실행이 일시 중지됩니다.
* 중지된 함수와 연관된 실행 컨텍스트는 실행 컨텍스트 스택(execution context stack) 이라는 특별한 자료 구조에 저장됩니다.
* 중첩 호출이 실행됩니다.
* 중첩 호출 실행이 끝난 이후 실행 컨텍스트 스택에서 일시 중단한 함수의 실행 컨텍스트를 꺼내오고, 중단한 함수의 실행을 다시 이어갑니다.

그럼 위에서 재귀적인 방법을 실제로 따라가봅시다.
```js run
function pow(x, n) {
  if (n == 1) {
    return x;
  } else {
    return x * pow(x, n - 1);
  }
}

alert( pow(2, 3) ); // 8
```
pow(2,3)을 넣으면 return 되기전에 새로운 pow(2, 2)가 실행됩니다. pow(2,2)를 따라가도 역시 pow(2,1)이 생성되고 이떄는 n=1이 떄문에 2라는 값이 리턴되고 이때 pow(2,1)은 끝났으므로 pow(2,2)q부터 차차 실행된다.

### 재귀 구조
재귀적으로 정의된 자료구조인 재귀적 자료 구조는 자기 자신의 일부를 복제하는 형태의 자료 구조입니다.<br>
재귀를 사용하면 무조건 맞다는 아니지만 유지보수측면에 유리하기 떄문에 반복문과 재귀를 적절히 잘 사용하는것이 필요하다.

## 5 - 2 rest-parameters-spread
### 나머지 매개변수 ...
함수 정의 방법과 상관없이 함수에 넘겨주는 인수의 개수엔 제약이 없습니다.아래와 같이 말이죠.
```js run
function sum(a, b) {
  return a + b;
}

alert( sum(1, 2, 3, 4, 5) );
```
이렇게 작성해도 a,b만 값을 처리하고 에러를 출력하지 않는다.
```js run
function sumAll(...args) { 
  console.log(args) // [1,2,3]을 출력
  let sum = 0;

  for (let arg of args) sum += arg;

  return sum;
}

sumAll(1, 2, 3) ; // 6
```
아래처럼 남은 변수를 배열로 모으는것도 가능하다.
```js run
function showName(firstName, lastName, ...titles) {
  alert( firstName + ' ' + lastName ); // Moseung Kim

  // 나머지 인수들은 배열 titles의 요소가 됩니다.
  // titles = ["Software Engineer", "Researcher"]
  alert( titles[0] ); // Software Engineer
  alert( titles[1] ); // Researcher
  alert( titles.length ); // 2
}
showName("Moseung", "Kim", "Software Engineer", "Researcher");
```
### arguments 객체
유사 배열 객체(array-like object)인 arguments를 사용하면 인덱스를 사용해 인수에 접근할 수 있습니다.
```js run
function showName() {
  alert( arguments.length ); //2
  alert( arguments[0] ); // 
  alert( arguments[1] );

  // arguments는 이터러블 객체이기 때문에
  // for(let arg of arguments) alert(arg); 를 사용해 인수를 펼칠 수 있습니다.
}

// 2, moseung, Kim 출력됨
showName("moseung", "Kim");

// 1, moseung, undefined가 출력됨(두 번째 인수는 없음)
showName("moseung");
```
위의 arguments는 아래 사진과 같다.
![image](https://user-images.githubusercontent.com/103626175/209424166-0cacf941-ead1-45b5-9867-417efc4902cb.png)
말 그대로 유사배열이기 때문에 배열의 method를 사용할순없다.

### 스프레드 문법 [#spread-syntax]
지금까지 매개변수 목록을 배열로 가져오는 방법에 대해 살펴보았습니다.그런데 개발을 하다 보면 반대되는 기능이 필요할 때가 생깁니다. 배열을 통째로 매개변수에 넘겨주는 것 같이 말이죠.<br>
그때 스프레드 문법이 유용하다.
```js run
let arr = [3, 5, 1];

*!*
alert( Math.max(arr) ); // NaN
*/!*
```
하지만 스프레드 문법을 사용하면
```js run
let arr = [3, 5, 1];

*!*
alert( Math.max(...arr) ); // 5
*/!*
```
#### 배열과 객체의 복사
스프레드 문법을 사용하면 배열과 객체의 복사도 가능하다.
```js run
let arr = [1, 2, 3];
let arrCopy = [...arr]; // 배열을 펼쳐서 각 요소를 분리후, 매개변수 목록으로 만든 다음에
                        // 매개변수 목록을 새로운 배열에 할당함

// 배열 복사본의 요소가 기존 배열 요소와 진짜 같을까요?
alert(JSON.stringify(arr) === JSON.stringify(arrCopy)); // true

// 두 배열은 같을까요?
alert(arr === arrCopy); // false (참조가 다름)

// 참조가 다르므로 기존 배열을 수정해도 복사본은 영향을 받지 않습니다.
arr.push(4);
alert(arr); // 1, 2, 3, 4
alert(arrCopy); // 1, 2, 3
```
```js run
let obj = { a: 1, b: 2, c: 3 };
let objCopy = { ...obj }; // 객체를 펼쳐서 각 요소를 분리후, 매개변수 목록으로 만든 다음에
                          // 매개변수 목록을 새로운 객체에 할당함

// 객체 복사본의 프로퍼티들이 기존 객체의 프로퍼티들과 진짜 같을까요?
alert(JSON.stringify(obj) === JSON.stringify(objCopy)); // true

// 두 객체는 같을까요?
alert(obj === objCopy); // false (참조가 다름)

// 참조가 다르므로 기존 객체를 수정해도 복사본은 영향을 받지 않습니다.
obj.d = 4;
alert(JSON.stringify(obj)); // {"a":1,"b":2,"c":3,"d":4}
alert(JSON.stringify(objCopy)); // {"a":1,"b":2,"c":3}
```

## 5 - 3 closure
### 코드블록
```js run
{
  // 지역 변수를 선언하고 몇 가지 조작을 했지만 그 결과를 밖에서 볼 수 없습니다.

  let message = "안녕하세요."; // 블록 내에서만 변숫값을 얻을 수 있습니다.

  alert(message); // 안녕하세요.
}

alert(message); // ReferenceError: message is not defined
```
위처럼 코드블록 내에서 선언한 변수들은 외부에서 호출이 불가능하다.

### 중첩함수
함수 내부에서 선언한 함수는 '중첩(nested)' 함수라고 부릅니다.
```js run
function sayHiBye(firstName, lastName) {

  // 헬퍼(helper) 중첩 함수
  function getFullName() {
    return firstName + " " + lastName;
  }

  alert( "Hello, " + getFullName() );
  alert( "Bye, " + getFullName() );
}
```
그리고 아래처럼 쉽게 이해가 안되는 counter라는 함수를 생성할 수 있습니다.
```js run
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();

alert( counter() ); // 0
alert( counter() ); // 1
alert( counter() ); // 2
```

### 렉시컬 환경
위의 함수에서 왜 counter가 잘 동작하는지 알아봅시다.<br>
모든 함수는 함수가 생성된 곳의 렉시컬 환경을 기억한다는 점입니다. 함수는 [[Environment]]라 불리는 숨김 프로퍼티를 갖는데, 여기에 함수가 만들어진 곳의 렉시컬 환경에 대한 참조가 저장됩니다.<br>
그래서 counter에는 count를 증가시켜주는 함수를 지니고 그 떄 생성됐던 환경을 기억하기 때문에 count라는 변수를 기억하고 있습니다. 그래서 매번 호출때마다 1씩 증가된 상태로 리턴 됩니다.
[자세한 설명](https://github.com/endmoseung/ko.javascript.info/blob/master/1-js/06-advanced-functions/03-closure/article.md)

### 가비지 컬렉션
함수 호출이 끝나면 함수에 대응하는 렉시컬 환경이 메모리에서 제거됩니다. 함수와 관련된 변수들은 이때 모두 사라지죠. 함수 호출이 끝나면 관련 변수를 참조할 수 없는 이유가 바로 여기에 있습니다. 자바스크립트에서 모든 객체는 도달 가능한 상태일 때만 메모리에 유지됩니다.<br>

그런데 호출이 끝난 후에도 여전히 도달 가능한 중첩 함수가 있을 수 있습니다. 이때는 이 중첩함수의 [[Environment]] 프로퍼티에 외부 함수 렉시컬 환경에 대한 정보가 저장됩니다. 도달 가능한 상태가 되는 것이죠.<br>

함수 호출은 끝났지만 렉시컬 환경이 메모리에 유지되는 이유는 바로 이 때문입니다.

## 5 - 4 var
### var는 블록 스코프가 없습니다.
```js run
if (true) {
  var test = true; // 'let' 대신 'var'를 사용했습니다.
}

*!*
alert(test); // true(if 문이 끝났어도 변수에 여전히 접근할 수 있음)
*/!*
```
let으로 선언할시에는 test에 접근이 불가능하지만 var은 스코프가 없기떄문에 접근이 가능하다.
```js run
for (var i = 0; i < 10; i++) {
  // ...
}

*!*
alert(i); // 10, 반복문이 종료되었지만 'i'는 전역 변수이므로 여전히 접근 가능합니다.
*/!*
```
위처럼 반복문에서 var은 전역으로 작용하기때문에 호출이 가능하다.
### 선언하기전에 사용가능한 var
```js run
function sayHi() {
  phrase = "Hello";

  console.log(phrase);//"Hello"
  
  var phrase;
}
sayHi();
```
분명 phrase를 호출하기 직전인데 위에서 사용이 가능한 모습.<br>
이렇게 변수가 끌어올려 지는 현상을 '호이스팅(hoisting)'이라고 부릅니다. var로 선언한 모든 변수는 함수의 최상위로 '끌어 올려지기(hoisted)' 때문입니다

## global object
전역 객체를 사용하면 어디서나 사용 가능한 변수나 함수를 만들 수 있습니다. 전역 객체는 언어 자체나 호스트 환경에 기본 내장되어 있는 경우가 많습니다.<br>

브라우저 환경에선 전역 객체를 window, Node.js 환경에선 global라고 부르는데, 각 호스트 환경마다 부르는 이름은 다릅니다.<br>
그리고 브라우저에서 let이나 const가 아닌 var로 선언한 전역 함수나 전역 변수는 전역 객체의 프로퍼티가 됩니다.
```js run
var gVar = 5;

alert(window.gVar); // 5 (var로 선언한 변수는 전역 객체 window의 프로퍼티가 됩니다)
```

### 요약
* 전역 객체를 사용하면 어디서든 접근 가능한 변수를 만들 수 있습니다.

* 전역 객체엔 Array와 같은 내장 객체, window.innerHeight(뷰포트의 높이를 반환함)같은 브라우저 환경 전용 변수 등이 저장되어 있습니다.

* 전역 객체는 globalThis라는 보편적인 이름으로 불립니다.

* 하지만 '관습'에 따라 브라우저에서는 window, Node.js에서는 global이라는 이름으로 불릴 때가 많습니다. globalThis는 제안 목록에 추가 된 지 얼마 안 된 기능이기 때문에, 비 크로미움 기반 브라우저에선 지원하지 않습니다(폴리필을 구현하면 사용할 수 있습니다).

* 프로젝트 전체에서 꼭 필요한 변수만 전역 객체에 저장하도록 하고, 전역 변수는 가능한 한 최소한으로 사용합시다.

* 모듈을 사용하고 있지 않다면, 브라우저에서 var로 선언한 전역 변수는 전역 객체의 프로퍼티가 됩니다.

* 이해하기 쉽고 요구사항 변경에 쉽게 대응할 수 있는 코드를 구현하려면, window.x처럼 전역 객체의 프로퍼티에 직접 접근합시다.

## 5 - 6 function-object
### 객체로서의 함수와 기명 함수 표현식
자바스크립트에서 함수는 값으로 취급됩니다. 이에 대해선 이미 배워서 알고 계실 겁니다.<br>

모든 값은 자료형을 가지고 있는데, 그렇다면 함수의 자료형은 무엇일까요?함수는 객체입니다.<br>

함수는 호출이 가능한(callable) '행동 객체'라고 이해하면 쉽습니다. 우리는 함수를 호출 할 수 있을 뿐만 아니라 객체처럼 함수에 프로퍼티를 추가·제거하거나 참조를 통해 전달할 수도 있습니다.

### 'name' 프로퍼티
함수 객체엔 몇 가지 쓸만한 프로퍼티가 있습니다.

'name' 프로퍼티를 사용하면 함수 이름을 가져올 수 있죠.
```js run
function sayHi() {
  alert("Hi");
}

alert(sayHi.name); // sayHi
```

### 'length' 프로퍼티
내장 프로퍼티 length는 함수 매개변수의 개수를 반환합니다. 예시를 살펴봅시다.
```js run
function f1(a) {}
function f2(a, b) {}
function many(a, b, ...more) {}

alert(f1.length); // 1
alert(f2.length); // 2
alert(many.length); // 2
```

### 커스텀 프로퍼티
함수에 자체적으로 만든 프로퍼티를 추가할 수도 있습니다.
```js run
function sayHi() {
  alert("Hi");
  
  *!*
  // 함수를 몇 번 호출했는지 세봅시다.
  sayHi.counter++;
  */!*
}
sayHi.counter = 0; // 초깃값

sayHi(); // Hi
sayHi(); // Hi

alert( `호출 횟수: ${sayHi.counter}회` ); // 호출 횟수: 2회
```
하지만 위에서 선언한 counter은 변수가 아니기떄문에 내부에서 counter 호출이 불가능하다.

## 6 - 7 new-function
### 문법
new Function 문법을 사용하면 함수를 만들 수 있습니다.
```js run
let sum = new Function('a', 'b', 'return a + b');

alert( sum(1, 2) ); // 3
```

### 클로저
그런데 new Function을 이용해 함수를 만들면 함수의 [[Environment]] 프로퍼티가 현재 렉시컬 환경이 아닌 전역 렉시컬 환경을 참조하게 됩니다.

따라서 new Function을 이용해 만든 함수는 외부 변수에 접근할 수 없고, 오직 전역 변수에만 접근할 수 있습니다.
```js run
function getFunc() {
  let value = "test";

*!*
  let func = new Function('alert(value)');
*/!*

  return func;
}

getFunc()(); // ReferenceError: value is not defined
```
일반적인 함수로 생성했다면 위에선 value="test"로 할당됐을것이다.

## 6 - 8 settimeout-setinterval
일정 시간이 지난 후에 원하는 함수를 예약 실행(호출)할 수 있게 하는 것을 '호출 스케줄링(scheduling a call)'이라고 합니다.

호출 스케줄링을 구현하는 방법은 두 가지가 있습니다.

* setTimeout을 이용해 일정 시간이 지난 후에 함수를 실행하는 방법
* setInterval을 이용해 일정 시간 간격을 두고 함수를 실행하는 방법

### setTimeout
```js run
function sayHi(who, phrase) {
  alert( who + ' 님, ' + phrase );
}

*!*
setTimeout(sayHi, 1000, "홍길동", "안녕하세요."); // 홍길동 님, 안녕하세요.
*/!*
```
몇ms인지 정한뒤에는 넘겨줄 인자를 위처럼 제공할 수 있다.
```js run
setTimeout(() => alert('안녕하세요.'), 1000); //익명함수를 전달하는것도 가능
```

#### clearTimeout으로 스케줄링 취소하기
```js run
let timerId = setTimeout(...);
clearTimeout(timerId);
```

### setInterval
인수 역시 동일합니다. 다만, setTimeout이 함수를 단 한 번만 실행하는 것과 달리 setInterval은 함수를 주기적으로 실행하게 만듭니다.
```js run
let timerId = setInterval(() => alert('째깍'), 2000);//2초마다 "째깍"

setTimeout(() => { clearInterval(timerId); alert('정지'); }, 5000);위의 setTimeout과 마찬가지로 clearInterval로 지워줄 수 있다.
```

## 6 - 10 bind
### 사라진 'this'
앞서 다양한 예제를 통해 this 정보가 사라지는 문제를 경험해보았습니다. 객체 메서드가 객체 내부가 아닌 다른 곳에 전달되어 호출되면 this가 사라집니다.

setTimeout을 사용한 아래 예시에서 this가 어떻게 사라지는지 살펴봅시다.
```js run
let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

*!*
setTimeout(user.sayHi, 1000); // Hello, undefined!
*/!*
```
#### 방법 1 래퍼
```js run
let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

*!*
setTimeout(function() {
  user.sayHi(); // Hello, John!
}, 1000);
*/!*
```

#### 방법 2 bind
모든 함수는 this를 수정하게 해주는 내장 메서드 bind를 제공합니다.
```js run
let user = {
  firstName: "John"
};

function func() {
  alert(this.firstName);
}

*!*
let funcUser = func.bind(user);
funcUser(); // John  
*/!* // this를 bind해주지 않으면 func함수에서는 undefined가 출력되야하지만 "john"이 출력된다.
```
이제 객체 메서드에 bind를 적용해 봅시다.
```js run
let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

*!*
let sayHi = user.sayHi.bind(user); // (*)
*/!*

// 이제 객체 없이도 객체 메서드를 호출할 수 있습니다.
sayHi(); // Hello, John!
```

`bind`는 컨텍스트를 `this`로 고정하는 것 뿐만 아니라 함수의 인수도 고정해줍니다.
```js run
function mul(a, b) {
  return a * b;
}

*!*
let double = mul.bind(null, 2);
*/!*

alert( double(3) ); // = mul(2, 3) = 6
alert( double(4) ); // = mul(2, 4) = 8
alert( double(5) ); // = mul(2, 5) = 10
```
