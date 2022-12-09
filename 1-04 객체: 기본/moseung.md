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
