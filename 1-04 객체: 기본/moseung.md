# 4강 Object

## 4 - 1 object-basics
### 객체
info:types 챕터에서 배웠듯이 자바스크립트엔 여덟 가지 자료형이 있습니다. 이 중 일곱 개는 오직 하나의 데이터(문자열, 숫자 등)만 담을 수 있어 '원시형(primitive type)'이라 부릅니다.<br>
빈 객체(빈 서랍장)를 만드는 방법은 두 가지가 있습니다.
* let user = new Object(); // '객체 생성자' 문법
* let user = {};  // '객체 리터럴' 문법

### 대괄호 표기법
```js run
const a = {
        "he is good" : "go",
        real:"real",

      }
      a["he is good"]
```
위처럼 ""로 key값을 표시했을때는 .으로는 읽을수 없어서 대괄호표기법으로 표시한다. a["real"]도 가능하다.
#### 계산된 프로퍼티
```js run
const fruit = "apple";
      const b = {
        [fruit] : "야미",
        gogo:"가보자"
      }
      b["apple"]; //"야미"
```
대괄포 표기법을 응용해서 위처럼 키값도 설정 가능하다.

#### 단축 프로퍼티
```js run
function makeUser(name, age) {
*!*
  return {
    name, // name: name 과 같음
    age,  // age: age 와 같음
    // ...
  };
*/!*
}
```
이것도 최신문법이고 key와 value가 동일하다면 위처럼 단축해서 표현 가능하다.

### 'in' 연산자로 프로퍼티 존재 여부 확인하기
in연산자로 객체 내에 프로퍼티가 존재하는지 확인 가능하다.
```js run
let user = { name: "John", age: 30 };

alert( "age" in user ); // user.age가 존재하므로 true가 출력됩니다.
alert( "blabla" in user ); // user.blabla는 존재하지 않기 때문에 false가 출력됩니다.
```

### 'for..in' 반복문
for..in 반복문을 사용하면 객체의 모든 키를 순회할 수 있습니다. for..in은 앞서 학습했던 for(;;) 반복문과는 완전히 다릅니다.
```js run
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
  // 키
  alert( key );  // name, age, isAdmin
  // 키에 해당하는 값
  alert( user[key] ); // John, 30, true
}
```

#### 객체 정렬 방식
정수 프로퍼티(integer property)는 자동으로 정렬되고, 그 외의 프로퍼티는 객체에 추가한 순서 그대로 정렬됩니다. 자세한 내용은 예제를 통해 살펴봅시다.

## 4 - 2 object-copy
### 참조에 의한 객체 복사
객체와 원시 타입의 근본적인 차이 중 하나는 객체는 '참조에 의해(by reference)' 저장되고 복사된다는 것입니다.<br>
변수엔 객체가 그대로 저장되는 것이 아니라, 객체가 저장되어있는 '메모리 주소'인 객체에 대한 '참조 값'이 저장됩니다.
```js run
let a = {};
let b = {}; // 독립된 두 객체

alert( a == b ); // false a와 b는 다른 주소를 참조하고 있기떄문에 다르다.
```

### 객체 복사, 병합과 Object.assign
```js run
const user = {
name:"모승",
age:26
}
for (let key in user) {
  clone[key] = user[key];
}
-----
Object.assign(user)
```

### 중첩 객체 복사
객체내에 중첩으로 객체가 있을경우에 문제가 생긴다.이 문제를 해결하려면 user[key]의 각 값을 검사하면서, 그 값이 객체인 경우 객체의 구조도 복사해주는 반복문을 사용해야 합니다. 이런 방식을 '깊은 복사(deep cloning)'라고 합니다.

## 4 - 3 garbage-collection
자바스크립트는 눈에 보이지 않는 곳에서 메모리 관리를 수행합니다. 이를 garbage-collection이라 합니다.
### garbage-collection 기준
'도달 가능한(reachable)' 값은 쉽게 말해 어떻게든 접근하거나 사용할 수 있는 값을 의미합니다. 도달 가능한 값은 메모리에서 삭제되지 않습니다.
### 내부 알고리즘
* 가비지 컬렉터는 루트(root) 정보를 수집하고 이를 'mark(기억)' 합니다.
* 루트가 참조하고 있는 모든 객체를 방문하고 이것들을 'mark' 합니다.
* mark 된 모든 객체에 방문하고 그 객체들이 참조하는 객체도 mark 합니다. 한번 방문한 객체는 전부 mark 하기 때문에 같은 객체를 다시 방문하는 일은 없습니다.
* 루트에서 도달 가능한 모든 객체를 방문할 때까지 위 과정을 반복합니다.
* mark 되지 않은 모든 객체를 메모리에서 삭제합니다.

## 4 - 4 object-methods
### 메서드 만들기
```js run
const abab = {
        print: function () {
          console.log("hi");
        },
      };//이게 기본값이고 :와 function을 지워도 똑같이 작동한다.
```

### 메서드와 this
객체내에서 this를 호출하면 현재 객체를 의미한다.<br>
화살표 함수는 일반 함수와는 달리 '고유한' `this`를 가지지 않습니다. 화살표 함수에서 `this`를 참조하면, 화살표 함수가 아닌 '평범한' 외부 함수에서 `this` 값을 가져옵니다. 아래 예시에서 함수 `arrow()`의 `this`는 외부 함수 `user.sayHi()`의 `this`가 됩니다. <br>
이번 우테코에서 비동기에 콜백함수를 넘겨주고 넘겨줄때 this를 호출당시의 this를 바인딩해줌으로써 해결했는데 애로우 함수를 사용하면 이를 해결가능하다.
```js run
 play = () => {
    InputView.readUserMoney((userMoney) => {
      this.makeLotto(userMoney);
      this.printUserLottos();
      this.printUserLottoList();
      this.getWinningNumber();
    });
  };
```
그리고 자바스크립트의 this는 다른 프로그래밍 언어의 this와 동작 방식이 다릅니다. this 값은 런타임에 결정됩니다. 컨텍스트에 따라 달라진다.

## 4 - 5 constructor-new
### new연산자와 생성자 함수
생성자 함수(constructor function)와 일반 함수에 기술적인 차이는 없습니다. 다만 생성자 함수는 아래 두 관례를 따릅니다.그래서 class를 만들때 앞글자를 대문자로 딴다.
* 함수 이름의 첫 글자는 대문자로 시작합니다.
* 반드시 'new' 연산자를 붙여 실행합니다.
생성자 함수에는 값을 return하는 방향으로 잘 작성안한다.

## 4 - 6 optional-chaining
optional chaining인?.은 ?.'앞'의 평가 대상이 undefined나 null이면 평가를 멈추고 undefined를 반환합니다.
```js run
const abab = {
        print: function () {
          console.log("hi");
        },
      };
      console.log(abab?.akak);// undefined 옵셔널 체이닝이 없으면 error를 띄운다.
```

## 4 - 7 symbol
심볼은 유일한 식별자를 만들고 싶을떄 선언한다.
```js run
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```

## 4 - 8 object-toPrimitive
```js run
const abab = {
        print: function () {
          console.log("hi");
        },
      };
      console.log(abab.toString());
      console.log(abab.valueOf());
```
위 두개의 메소드로 형변환 가능하고 결과값은 아래 사진과 같다.
![image](https://user-images.githubusercontent.com/103626175/206748199-45b7410a-d698-4e61-8a91-8a8df675d0d0.png)

