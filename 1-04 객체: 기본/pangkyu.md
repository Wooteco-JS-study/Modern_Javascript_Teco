### ch1 : 오브젝트

##### 객체

- 자바스크립트에는 8가지 자료형이 있다. 이 중 7개는 오직 하나의 데이터만 담을 수 있어 원시형(primitive type)이라 부른다.
- 객체형은 원시형과 다르게 다양한 데이터를 담을 수 있다. 키로 구분된 데이터 집합이나 복잡한 개체를 저장할 수 있다.
- 객체는 중괄호 <code>{...}</code>를 이용해 만들 수 있다. 중괄호안에는 키:값 쌍으로 구성된 프로퍼티를 여러 개 넣을 수 있다. <code>키</code>에는 문자형, <code>값</code>에는 모든 자료형이 허용된다. 프로퍼티 키는 프로퍼티 이름이라고도 부른다.

```js
// 빈 객체를 만드는 방법
//1.  객체 생성자 문법
let user = new Object();
//2 객체 리터럴 문법
let user = {};
```

```js
let user = {
  name: "John", // 키 : name , 값 'John'
  age: 30, // 키 : age, 값 : 30
};
```

- 점 표기법으로 프로퍼티의 값을 읽는 것도 가능하다.

```js
// 프로퍼티 값 얻기
console.log(user.name);
console.log(user.age);
```

- 프로퍼티 값에는 모든 자료형이 올 수 있다.

```js
user.isAdmin = true;
```

- <code>delete</code>연산자를 사용하면 프로퍼티를 삭제할 수 있다.

```js
delete user.age;
```

- 여러 단어를 조합하여 프로퍼티 이름을 만든 경우에는 프로퍼티 이름을 따옴표로 묶어야 한다.

```js
let user = {
  "likes birds": true,
};
```

- 마지막 프로퍼티 끝은 쉼표로 끝날 수 있다.

```js
let user = {
  name: "John",
  age: 30,
};
```

##### 대괄호 표기법

- 여러 단어를 조합하여 프로퍼티 키를 만든 경우에는 점 표기법으로 프로퍼티 값을 읽을 수 없다.

```js
user.likes birds = true; // 문법 에러 발생
```

- 키가 유효한 변수 식별자가 아닌 경우에는 점 표기법 대신 대괄호 표기법으로 동작시킬 수 있다.
  - 유효한 변수 식별자 : 공백이 없고, 숫자로 시작하지 않으며, <code>$</code>, <code>\_</code>를 제외한 특수 문자가 없어야 한다.

```js
let user = {};

// set
user["likes birds"] = true;

// get
alert(user["likes birds"]);

// delete
delete user["likes birds"];
```

- 대괄호 표기법을 사용하면 변수를 키로 사용한 것과 같이 문자열 뿐만 아니라 모든 표현식의 평가 결과를 프로퍼티 키로 사용할 수 있다.

```js
let key = "likes birds";
// user['likes birds'] = true; 와 같음
user[key] = true;
```

- 변수 <code>key</code>는 런타임에 평가되기 때문에 사용자 입력값 변경 등에 따라 값이 변경될 수 있다.

```js
let user = {
  name: "John",
  age: 30,
};
let key = prompt("사용자의 어떤 정보를 얻고 싶은가요? ", "name");
// 변수로 접근
alert(user[key]); // John(프롬프트에서 name을 입력한경우 )
```

##### 계산된 프로퍼티

- 객체를 만들 때 객체 리터럴 안의 프로퍼티 키가 대괄호로 둘러싸여 있는 경우, 이를 계산된 프로퍼티(computed property)라고 부른다.

```js
let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");

let bag = {
*!*
  [fruit]: 5, // 변수 fruit에서 프로퍼티 이름을 동적으로 받아 옵니다.
*/!*
};

alert( bag.apple ); // fruit에 "apple"이 할당되었다면, 5가 출력됩니다.
```

- 대괄호 표기법은 프로퍼티 이름과 값의 제약을 없애주기 때문에 점 표기법보다 강력하다. 그런데 작성하기 번거롭다는 단점이 있다.
- 프로퍼티 이름이 확정된 상황이고 단순한 이름이라면 처음에는 점 표기법을 사용하다가 뭔가 복잡한 상황이 발생했을 때 대괄호 표기법으로 바꾸는 경우가 많다.

##### 단축 프로퍼티

```js
function makeUser(name, age) {
  return {
    name: name,
    age: age,
    // 등등
  };
}
let user = makeUser("John", 30);
alert(user.name); // John
```

- 이름과 값이 변수의 이름과 동일한데, 이 경우에는 프로퍼티 값 단축구문을 사용하면 코드를 짧게 줄일 수있다.

```js
function makeUser(name, age) {
  return {
    name,
    age,
    // 등등
  };
}
let user = makeUser("John", 30);
alert(user.name); // John
```

- 한 객체에서 일반 프로퍼티와 단축 프로퍼티를 함께 사용하는 것도 가능하다.

##### 프로퍼티 이름의 제약사항

- 변수 이름(키)에는 예약어를 사용하면 안되지만, 객체 프로퍼티에는 이런 제약이 없다.

```js
let obj = {
  for: 1,
  let: 2,
  return: 3,
};
console.log(obj.for + obj.let + obj.return); // 6
```

- 문자형이나 심볼형에 속하지 않은 값은 문자열로 자동 형변환된다.

```js
let obj = {
  0: "test", // "0" : "test"와 동일하다.
};
// 숫자 0은 문자열 "0"으로 변환되기 때문에 밑의 코드는 같은 프로퍼티에 접근한다.
alert(obj["0"]); // test
alert(obj[0]); // test
```

- 객체 프로퍼티 키에 쓸 수 있는 문자열에 제약이 없지만, <code>** proto**</code>는 제외

```js
let obj = {};
obj.__proto__ = 5; // 숫자를 할당
alert(obj.__proto__); // [object object] - 숫자를 할당했지만 값은 객체가 되어버렸다.
```

##### 'in'연산자로 프로퍼티 존재 여부 확인하기

- 자바스크립트의 중요한 특징 중 하나 : 존재하지 않는 프로퍼티에 접근하려 해도 에러가 발생하지 않고 <code>undefined</code>를 반환한다.

```js
// 이런 특징을 응용하면 프로퍼티 존재 여부를 쉽게 확인할 수 있다.
let user = {};
alert(user.noSuchProperty === undefined); // true는 존재하지 않음을 의미
```

```js
// 위와같은 방법을 사용할 수 있지만,
// 연산자 in을 사용하면 프로퍼티 존재여부 확인 가능하다.
"key" in object;

let user = { name: "John", age: 30 };
alert("age" in user); // user.age가 존재하므로 true 출력
alert("blabla" in user); // 존재하지 않으므로 false 출력
```

- <code>in</code> 왼쪽에는 반드시 프로퍼티 이름이 와야한다. 프로퍼티 이름은 보통 따옴표로 감싼 문자열이다.
- 따옴표를 생략하면 엉뚱한 변수가 조사대상이 된다.

```js
let user = { age: 30 };
let key = "age";
alert(key in user); // true, 변수 key에 저장된 값 'age'를 사용해 프로퍼티 존재여부를 확인한다.
```

- 대부분의 경우, 일치 연산자를 사용하여 프로퍼티 존재 여부를 알아내는 방법이 잘 동작하나, 가끔 실패하는 경우가 있다.

```js
let obj = {
  test: undefined,
};
alert(obj.test); // 값이 undefined이므로, 얼럿 창에는 undefined가 출력된다. 그러나 프로퍼티 test는 존재한다.
alert("test" in obj); // in을 사용하면 프로퍼티 유무를 제대로 확인할 수 있다. (true)
```

##### for in 반복문

- <code>for .. in </code>반복문을 사용하면 객체의 모든 키를 순회할 수있다.

```js
for (key in object) {
  // 각 프로퍼티 키를 이용하여 본문을 실행한다.
}
```

```js
let user = {
  name: "John",
  age: 30,
  isAdmin: true,
};

for (let key in user) {
  // 키
  alert(key); // name, age, isAdmin
  // 키에 해당하는 값
  alert(user[key]); // John, 30, true
}
```

- 반복 변수명은 자유롭게 정할 수 있다.
- <code>for in</code>반복문에서도 <code>for(;;)</code>문 처럼 반복 변수를 선언<code>let key</code>했다

##### 객체 정렬 방식

- 객체는 특별한 방식으로 정렬된다. 정수 프로퍼티는 자동으로 정렬되고, 그 외 프로퍼티는 객체에 추가한 순서 그대로 정렬된다.

```js
let codes = {
  49: "독일",
  41: "스위스",
  44: "영국",
  1: "미국",
};
for (let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```

- 정수 프로퍼티 : 변형 없이 정수에서 왔다갔다 할 수 있는 문자열

```js
// 키가 정수가 아닌 경우에는 작성된 순서대로 프로퍼티가 나열도니다.
let user = {
  name: "John",
  surname: "Smith",
};
user.age = 25;
for (let prop in user) {
  alert(prop); // name, surname, age
}
```

- 자바스크립트에는 일반 객체 이외에도 다양한 종류가 있다.
  - Array : 정렬된 데이터 컬렉션을 저장할 때 쓰임
  - Date : 날짜와 시간 정보를 저장할 때 쓰임
  - Error : 에러 정보를 저장할 때 쓰임
  - etc
### ch2 : object-copy

> 객체와 원시 타입의 근본적 차이 중 하나는 객체는 참조에 의해(by reference)저장되고 복사된다. 이에 반면에 원시값(문자열,숫자,불린 값)은 값 그대로 저장/할당되고 복사된다.

```js
let user = { name: "John" };
let admin = user; // 참조값을 복사한다.
```

- 변수는 2개이지만 각 변수에는 동일 객체에 대한 참조 값이 저장된다.
- 객체에 접근하거나 조작할때는 여러 변수를 사용할 수 있다.

```js
let user = { name: "John" };
let admin = user;
admin.name = "Pete";
alert(user.name); // 'Pete'
```

##### 참조에 의한 비교

- 객체 비교 시 <code>==</code>와 <code>===</code>는 동일하게 동작한다.
- **비교 시 피연산자인 두 객체가 동일한 객체인 경우 참을 반환**

```js
// 두 변수가 같은 객체를 참조할 때
let a = {};
let b = a; // 참조에 의한 복사

alert(a == b); // true, 두 변수는 같은 객체를 참조합니다.
alert(a === b); // true

// 다를 때
let a = {};
let b = {}; // 독립된 두 객체

alert(a == b); // false
```

- 대소 비교나 같은 원시값과의 비교에서는 객체가 원시형으로 변환된다.

##### 객체 복사, 병합과 Object.assign

- 기존 객체와 똑같으면서 독립적인 객체를 만들고 싶을때?
  - 새로운 객체를 만든 다음 기존 객체의 프로퍼티들을 순회하여 원시 수준까지 프로퍼티를 복사하면 된다.

```js
let user = {
  name: "John",
  age: 30,
};
let clone = {};
for (let key in user) {
  clone[key] = user[key];
}
clone.name = "Pete";
alert(user.name); // 가존 객체에는 여전히 John이 남아있다.
alert(clone.name); // 'Pete'
```

- <code>Object.assign</code>를 사용해도 된다.

```js
Object.assign(dest, [src1, src2, src3...])
/*
dest : 목표로 하는 객체
src1 ~ src N : 복사하고자 하는 객체
마지막으로 dest를 반환

*/

let user = {name : 'John'};
let permissions1 = {canView : true};
let permissions2 = {canEdit : true};

Object.assign(user, permissions1, permission2);
// user에는 { name : 'John', canView : true, canEdit : true} 가 들어간다.
// 목표객체에 동일한 이름ㅇ르 가진 프로퍼티가 있는경우에는 기존 값이 덮어씌워진다.
```

- Object.assign을 사용하면 반복문 없이도 간단하게 객체 복사가 가능하다

```js
let user = {
  name: "John",
  age: 30,
};

let clone = Object.assign({}, user);
// user에 모든 프로퍼티가 빈 배열에 복사되고 변수에 할당된다.
```

##### 중첩 객체복사

- 프로퍼티는 다른 객체에 대한 참조 값일 수 있다.

```js
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50,
  },
};
alert(user.sizes.height); // 182
```

- <code>clone.sizes = user.sizes</code>로 프로퍼티를 복사하는 것만으로는 객체를 복제할 수 없다. <code>user.sizes</code>는 객체이기 때문에 참조값이 복사된다. <code>clone.sizes = user.sizes</code>로 프로퍼티를 복사하면 <code>clone</code>과 <code>user</code>는 같은 sizes를 공유한다.
- 이 문제를 해결하기 위해서는 <code>user[key]</code>의 각 값을 검사하면서 그 값이 객체인 경우 객체의 구조도 복사하는 반복문을 사용해야한다. ==> 깊은 복사(deep cloning)
- **자바스크립트 라이브러리 <code>lodash</code>의 메서드인 <code>\_.cloneDeep(obj)</code>를 사용하면 깊은 복사를 처리할 수 있다.**


### ch3 : 가비지 컬렉션

> 자바스크립트는 눈에 보이지 않는 곳에서 메모리 관리를 수행

##### 기준

- 자바스크립트는 도달 가능성(reachability) 개념으로 메모리 관리를 수행한다
  - 도달가능성 : 어떻게든 접근하거나 사용할 수 있는 값을 의미. 도달 가능한 값은 메모리에서 삭제되지 않는다.
  - 예시 : 현재 함수의 지역 변수와 매개변수, 중첩 함수의 체인에 있는 함수에서 사용되는 변수/매개변수, 전역 변수 등을 루트(root)라고 부른다.
  - 루트가 참조하는 값이나 체이닝으로 루트에서 참조할 수 있는 값은 도달 가능한 값이 된다.
- 자바스크립트 엔진에서는 가바지 컬렉터가 끊임없이 동작한다. 가비지 컬렉터는 모든 객체를 모니터링하고, 도달할 수 없는 객체는 삭제한다.

##### 예시

```js
let user = {
  name: "John",
};
```

- 전역변수 user는 <code>{name : 'John'}</code>를 참조한다.
- <code>user</code>의 값을 다른 값으로 덮어쓰면 참조가 사라진다.

```js
user = null;
```

- 이제 John은 도달할 수 없는 상태다. John에 접근할 방법도, 참조하는 것도 모두 사라졌다.
- 가비지 컬렉터는 John에 저장된 데이터를 삭제하고, John을 메모리에서 삭제한다.

##### 참조 두 개

```js
let user = {
  name: "John",
};
//user에서 admin으로 복사
let admin = user;

// user의 값을 다른 값으로 덮어쓰기
user = null;
```

- <code>admin</code>으로 여전히 John에 접근할 수 있기 때문에 John은 메모리에서 삭제되지 않는다
- <code>admin</code>도 다른 값으로 덮어쓰면 John은 메모리에서 삭제될 수 있다.

##### 연결된 객체

```js
function marry(man, woman) {
  woman.husband = man;
  man.wife = woman;

  return {
    father: man,
    mother: woman,
  };
}
let family = marry(
  {
    name: "John",
  },
  {
    name: "Ann",
  }
);
```

- <code>marry</code>는 매개변수로 받은 두 객체를 서로 참조하고, 두 객체를 포함한 새로운 객체를 반환한다.

```js
// 참조 두 개를 지우기
delete family.father;
delete family.mother.husband;
```

- 하나만 지웠다면 모든 객체가 여전히 도달 가능한 상태지만, 모두 지워서 John으로 들어오는 참조가 사라졌다.
  - John은 도달 가능한 상태에서 벗어나짐
  - John은 메모리에서 제거되며, John에 저장된 데이터(프로퍼티)도 메모리에서 사라진다.
- 외부로 나가는 참조는 도달 가능한 상태에 영향을 주지 않는다.

```js
// family가 아무것도 참조하지 않을 경우
family = null;
```

- John과 Ann이 서로를 참조하고 있고, 두 객체 모두 외부에서 들어오는 참조를 가지지만, <code>family</code>객체와 루트의 연결이 사라지면 루트 객체를 참조하는 것이 아무것도 없다. 따라서 객체 전부가 메모리에서 제거된다.

##### 내부 알고리즘

- 'mark-and-sweep'은 가비지 컬렉션의 기본 알고리즘이다.
- 가비지 컬렉션의 단계
  - 가비지 컬렉터는 루트(root)정보를 수집하고 이를 mark(기억)한다.
  - 루트가 참조하고 있는 모든 객체를 방문하고 이것들을 mark한다
  - mark된 모든 객체에 방문하고 그 객체들이 참조하는 객체도 mark한다. 한번 방문한 객체는 전부 mark 하기 때문에 같은 객체를 다시 방문하는 일은 없다.
  - 루트에서 도달 가능한 모든 객체를 방문할 때 까지 위 과정을 반복한다.
  - mark되지 않은 모든 객체를 메모리에서 삭제한다.
- 루트에서 페인트를 붓는다고 생각하면 과정을 이해하기 쉬움(페인트가 묻지 않는 객체는 메모리에서 삭제)

- 최적화 기법
  - generational collection(세대별 수집)
    - 객체를 '새로운 객체'와 '오래된 객체'로 나눈다.
    - 객체 상당수는 생성 이후 자기 역할을 수행한 뒤, 쓸모가 없어지는데 이를 '새로운 객체'로 구분한다
    - 가바지 컬렉터는 새로운 객체를 공격적으로 메모리에서 제거한다.
    - 일정 시간 이상 동안 살아남은 객체는 '오래된 객체'로 분류하고, 가비지 컬렉터가 덜 감시한다.
  - incremental collection(점진적 수집)
    - 방문해야 할 객체가 많으면 모든 객체를 한 번에 방문하고 mark 하는데 오랜 시간이 걸린다.
    - 가비지 컬렉션에 많은 리소스가 사용되어 실행 속도도 느려진다.
    - 이런 현상을 개선하기 위해 가비지 컬렉션을 여러 부분으로 분리하여 각 부분을 별도로 수행한다.
    - 작업을 분리하고, 변경 사항을 추적하는 데 추가 작업이 필요하지만, 긴 지연을 짧은 지연 여러 개로 분산시킬 수 있다는 장점이 있다.
  - idle-time collection(유휴 시간 수집)
    - 가비지 컬렉터는 실행에 주는 영향을 최소화하기 위해 CPU가 유휴 상태일 때만 가비지 컬렉션을 실행한다.
- 이 외에도 다양한 최적화 기법과 가비지 컬렉션 알고리즘이 있다.

### ch4 : object methods

##### 메서드와 this

- 객체는 사용자(user), 주문(order) 등과 같이 실제 존재하는 개체를 표한하고자 할 때 생성한다.
- 자바스크립트에서는 객체의 프로퍼티에 함수를 할당해 객체에게 행동할 수 있는 능력을 준다.

```js
let user = {
  name: "John",
  age: 30,
};
```

##### 메서드 만들기

```js
let user = {
  name: "John",
  age: 30,
};
user.sayHi = function () {
  alert("하이");
};
user.sayHi(); // 하이
```

- 객체 프로퍼티에 할당된 함수를 메서드라고 부른다.
- 객체를 사용하여 개체를 표현하는 방식을 객체 지향 프로그래밍(object-oriented programming, OOP)이라고 부른다.

```js
// 함수 선언
function sayHi() {
  alert("하이");
}
// 선언된 함수를 메서드로 등록
user.sayHi = sayHi;
user.sayHi(); // 하이
```

##### 메서드 단축 구문

```js
// 아래 두 객체는 동일하게 동작
user = {
  sayHi: function () {
    alert("hi");
  },
};

// 단축구문
user = {
  sayHi() {
    alert("hi");
  },
};
```

- function을 생략해도 메서드 정의할 수 있다.

##### 메서드와 this

- 메서드는 객체에 저장된 정보에 접근할 수 있어야 제 역할을 할 수 있다.
- 대부분의 메서드가 객체 프로퍼티의 ㄱ밧을 활용한다.
- 메서드 내부에서 <code>this</code> 키워드를 사용하면 객체에 접근할 수 있다.

```js
let user = {
  name: "John",
  age: 30,
  sayHi() {
    alert(this.name); // this는 현재객체를 나타냄
  },
};
user.sayHi(); // John
```

- <code>this</code>를 사용하지 않고 외부 변술르 참조해도 객체접근이 가능하다.

```js
let user = {
  name: "John",
  age: 30,
  sayHi() {
    alert(user.name);
  },
};
// 하지만 외부 변수를 사용하여 참조할 경우에 예상치 못한 에러가 발생할 수 있다.
// user를 복사하여 다른 변수에 할당하고 user를 다른 값으로 덮어쓰면 sayHi()는 다른 값을 참조한다.
```

##### 자유로운 this

- 자바스크립트의 <code>this</code>는 모든 함수에서 사용할 수 있다.
- <code>this</code>값은 런타임에 결정된다.(컨텍스트에 따라 달라짐)

```js
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert(this.name);
}
// 별개의 객체에서 동일한 함수를 사용
user.f = sayHi;
admin.f = sayHi;

// this는 점 앞의 객체를 참조하기 때문에 this값이 다름
user.f(); // John
admin.f(); // Admin
admin["f"](); // Admin (점과 대괄호는 동일하게 동작)
```

- [this 문법정리](https://velog.io/@pangkyu/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-this)


### ch6 : contructor-new

##### new 연산자와 생성자 함수

- 객체 리터럴 <code>{...}</code>을 사용하면 객체를 쉽게 만들 수 있다.
- 그러다보면 유사한 객체를 여러 개 만들어야 할 때가 생기는데 => <code>new</code>연산자와 생성자 함수를 사용하면 유사한 객체 여러 개를 쉽게 만들 수 있다.

##### 생성자함수

- constructor function은 두 개의 관례를 따른다.
  1. 함수 이름의 첫 글자는 대문자로 시작한다
  2. 반드시 <code>new</code>연산자를 붙여 실행한다.

```js
function User(name) {
  this.name = name;
  this.isAdmin = false;
}
let user = new User("보라");
alert(user.name); // 보라
alert(user.isAdmin); // false
/*
1. 빈 객체를 만들어 this에 할당한다. 
2. 함수 본문을 실행한다. this에 새로운 프로퍼티를 추가하여 this를 수정한다. 
3. this를 반환한다. 
*/
```

- 객체 리터럴 문법으로 일일이 객체를 만든느 방법보다 훨씬 간단하고 읽기 쉽게 객체를 만들 수 있다.
- 생성자의 의의 : 재사용할 수 있는 객체 생성 코드를 구현

##### new.target과 생성자 함수

- <code>new.target</code>프로퍼티를 사용하여 함수가 <code>new</code>와 함께 호출되었는지 아닌지 알 수 있다.
- 일반적인 방법으로 함수 호출했다면 <code>new.target</code>은 <code>undefined</code>를 반환한다.
- 반면, <code>new</code>와 함께 호출한 경우에는 <code>new.target</code>은 함수 자체를 반환해준다.

```js
function User() {
  alert(new.target);
}
User(); // undefined
new User(); // function User{...}
```

- 함수 본문에서 <code>new.target</code>을 사용하면 해당 함수가 <code>new</code>와 함께 호출되었는지(in constructor mode) 아닌지(in regular mode)를 확인할 수 있다.

```js
function User(name) {
  if (!new.target) {
    // new 없이 호출해도
    return new User(name); // new를 붙여줍니다
  }
  this.name = name;
}
let bora = User("보라"); // new User를 쓴 것처럼 바꿔준다.
alert(bora.name); // 보라
```

- <code>new</code>를 생략해서 객체를 만드는 것은 정말 필요한 경우에만 사용하고 남발하지 않는 것이 좋다.

##### 생성자와 리턴문

- 생성자 함수에는 보통 <code>return</code>문이 없다. 반환해야 할 것은 모두 <code>this</code>에 저장되고, <code>this</code>는 자동으로 반환되기 때문에 반환문을 명시적으로 써 줄 필요가 없다.
- 만약 리턴문이 있다면?
  - 객체를 <code>return</code>한다면 this 대신 객체가 반환된다.
  - 원시형을 <code>return</code>한다면 return문이 무시된다.
- return뒤에 객체가 오면 생성자 함수는 해당 객체를 반환해주고, 이 외의 경우는 <code>this</code>가 반환된다.

```js
function BigUser() {
  this.name = "원숭이";
  return { name: "고릴라" }; // <- this가 아닌 새로운 객체를 반환
}
alert(new BigUser().name); // 고릴라
```

```js
function SmallUser() {
  this.name = "원숭이";
  return; // <- this를 반환
}
alert(new SmallUser().name); // 원숭이
```

##### 생성자 내 메서드

- 생성자 함수를 사용하면 매개변수를 이용해 객체 내부를 자유롭게 구성할 수 있다.
- 메서드를 더해주는 것도 가능하다.

```js
function User(name) {
  this.name = name;
  this.sayHi = function () {
    alert("제 이름은" + this.name + "입니다.");
  };
}
let bora = new User("이보라");
bora.sayHi();
```

### ch7 : 옵셔널 체이닝

> 옵셔널 체이닝 <code>?.</code>을 이용하면 프로퍼티가 없는 중첩 객체를 에러 없이 안전하게 접근할 수 있다.

##### 옵셔널 체이닝이 필요한 이유

```js
// 사용자 중 몇 명이 주소정보를 가지고 있지 않을 때, 주소정보에 접근하면 에러가 발생할 수 있다.
let user = {}; // 주소 정보가 없는 사용자
alert(user.address.street); //  TypeError: Cannot read property 'street' of undefined
```

```js
// 자바스크립트를 사용하여 페이지에 존재하지 않는 요소에 접근하여 정보를 가져오려할 때 문제가 발생
let html = document.querySelector(".my-element").innerHTML; // 쿼리셀렉터 호출 결과가 null인 경우 에러가 발생한다
```

- 명세서에 <code>?.</code>이 추가되기 전에는 문제해결을 위해 <code>&&</code>연산자를 사용했다.
- AND연산자를 사용하면 코드가 길어진다는 단점이 있다.

```js
let user = {};
alert(user && user.address && user.address.street); // undefined, 에러가 발생하지 않음
```

##### 옵셔널 체이닝의 등장

- <code>?.</code>은 <code>?.</code>'앞'의 평가대상이 undefined나 null이면 평가를 멈추고 <code>undefined</code>를 반환한다.

```js
let user = {}; // 주소 정보가 없는 사용자
alert(user?.address?.street); // undefined, 에러가 발생하지 않음
```

```js
let user = null;
alert(user?.address); // undefined
alert(user?.address.street); // undefined
/*
user가 null이나 undefined가 아니고 실제 값이 존재하는 경우에는 반드시 user.address 프로퍼티는 있어야 한다. 그렇지 않으면 user?.address.street의 두 번째 점 연산자에서 에러 발생한다. 
*/
```

- 옵셔널 체이닝은 선언이 완료된 변수를 대상으로만 동작한다.
- <code>?.</code>는 왼쪽 평가대상에 값이 없으면 즉시 평가를 멈춘다. (단락 평가)

```js
// ?.()와 ?.[]
// ?.은 함수나 대괄호와 함께 동작하는 특별한 문법 구조체이다.
let user1 = {
  admin() {
    alert("관리자 계정이다.");
  },
};
let user2 = {};
user1.admin?.(); // 관리자 계정이다
user2.admin?.();
```

- <code>.</code>대신 대괄호를 사용해 객체 프로퍼티에 접근하는 경우에는 <code>?.[]</code>를 사용할 수도 있다.

```js
let user1 = {
  firstName: "Violet",
};
let user2 = null;
let key = "firstName";

alert(user1?.[key]); // Violet
alert(user2?.[key]); // undefined
alert(user1?.[key]?.something?.not?.existing); // undefined
```

- <code>?.</code>은 delete와 조합하여 사용할 수 있다.

```js
delete user?.name; // user가 존재하면 user.name을 삭제한다.
```

- <code>?.</code>은 읽기/삭제는 할 수 있지만 쓰기에는 사용할 수 없다.
- <code>?.</code>은 할당 연산자 왼쪽에서 사용할 수 없다.

```js
user?.name = 'Violet'; // SyntaxError: Invalid left-hand side in assignment
// 에러가 발생하는 이유 : undefined = 'Violet'이 되기 때문
```

```md
1. `obj?.prop` -- `obj`가 존재하면 `obj.prop`을 반환하고, 그렇지 않으면 `undefined`를 반환함
2. `obj?.[prop]` -- `obj`가 존재하면 `obj[prop]`을 반환하고, 그렇지 않으면 `undefined`를 반환함
3. `obj?.method()` -- `obj`가 존재하면 `obj.method()`를 호출하고, 그렇지 않으면 `undefined`를 반환함
```


### ch8 : 심볼형

> 자바스크립트는 객체 프로퍼티 키로 오직 문자형과 심볼형만 허용한다.

- 심볼의 주요 유스케이스
  - 객체의 숨김 프로퍼티 : 외부 스크립트에서 우리가 숨긴 것을 볼 수 없다. 외부 스크립트나 라이브러리에 속한 객체에 새로운 프로퍼티를 추가하고 싶다면 심볼을 만들고 이를 프로퍼티 키로 사용하면 된다.
  - Symbol.\* 로 접근할 수 있다.

##### 심볼

- 심볼은 유일한 식별자(unique identifier)를 만들고 싶을 때 사용한다.

```js
let id = Symbol();

// 심볼 이름이라 불리는 설명을 붙일 수도 있다.
let id = Symbol("id");
```

- 심볼은 유일성이 보장되는 자료형이다. 설명이 동일한 심볼을 여러 개 만들어도 각 심볼 값은 다르다.
- 심볼에 붙이는 설명은 어떤 것에도 영향을 주지 않는 이름표 역할만을 한다.

```js
let id1 = Symbol("id");
let id2 = Symbol("id");
alert(id1 == id2); // false
```

- 심볼형 값은 다른 자료형으로 암시적 형 변환(자동형변환)되지 않는다.

```js
let id = Symbol("id");
alert(id); //  TypeError: Cannot convert a Symbol value to a string
```

- 심볼을 반드시 출력해야하는 상황이면 <code>.toString()</code>메소드를 사용한다.

```js
let id = Symbol("id");
alert(id.toString()); // Symbol(id)가 얼럿 창에 출력됨
```

- <code>symbol.description</code> 프로퍼티를 이용하면 설명만 보여주는 것도 가능하다.

```js
let id = Symbol("id");
alert(id.description); // id
```

##### 숨김 프로퍼티

- 심볼을 이용하면 숨김(hidden)프로퍼티를 만들 수 있다. 숨김 프로퍼티는 외부 코드에서 접근이 불가능하고 값도 덮어쓸 수 없는 프로퍼티이다.

```js
let user = {
  // 서드파티 코드에서 가져온 객체
  name: "John",
};
let id = Symbol("id");
user[id] = 1;
alert(user[id]); // 심볼을 키로 사용해 데이터에 접근할 수 있다.

/*
문자열 id를 키로 써도 되는데 Symbol('id')을 사용한 이유 ? 
user는 서드파티 코드에서 갖고 온 객체이므로 함부로 새로운 프로퍼티를 추가할 수 없다. 
그런데 심볼은 서드파티 코드에서 접근할 수 없기 때문에, 심볼을 사용하면 서드파티 코드가 모르게 user에 식별자를 부여할 수 있다.
*/
```

- 심볼은 유일성이 보장되므로 우리가 만든 식별자와 제3의 스크립트에서 만든 식별자가 이름이 같더라도 충돌하지 않는다.
- 심볼 대신 문자열 <code>'id'</code>를 사용해 식별자를 만들었다면 충돌이 발생할 가능성이 있다.

```js
let user = { name: "John" };
// 문자열 id를 사용하여 식별자를 만들었다.
user.id = "스크립트 id 값";
// 만약 제 3의 스크립트가 우리 스크립트와 동일하게 문자열 'id'를 이용하여 식별자를 만들었다면?
user.id = "제 3 스크립트 id 값 ";
// 의도치 않게 값이 덮어 쓰여서 우리가 만든 식별자가 무의미해 진다.
```

##### Symbols in a literal

- 객체 리터럴 <code>{...}</code>을 사용해 객체를 만든 경우, 대괄호를 사용하여 심볼형 키를 만들어야 한다.

```js
let id = Symbol("id");
let user = {
  name: "John",
  [id]: 123, // 'id' : 123은 안된다.
};
```

##### 심볼은 for in에서 배제된다

- 키가 심볼인 프로퍼티는 <code>for in</code>반복문에서 배제된다.

```js
let id = Symbol("id");
let user = {
  name: "John",
  age: 30,
  [id]: 123,
};
for (let key in user) alert(key); // name과 age만 출력되고, 심볼은 출력되지 않는다.
alert(" 직접 접근한 값 : " + user[id]); // 심볼로 직접 접근하면 잘 작동한다.
```

- <code>Object.keys(user)</code>에서도 키가 심볼인 프로퍼티는 배제된다. '심볼형 프로퍼티 숨기기'라 불리는 원칙 덕분에 외부 스크립트나 라이브러리는 심볼형 키를 가진 프로퍼티에 접근하지 못한다.
- <code>Object.assign</code>은 키가 심볼인 프로퍼티를 배제하지 않고 객체 내 모든 프로퍼티를 복사한다.
- 객체를 복사하거나 병합할 때, <code>id</code>같은 심볼을 포함한 프로퍼티 전부를 사용하도록 하기 위해 설게되었음

```js
let id = Symbol("id");
let user = {
  [id]: 123,
};
let clone = Object.assign({}, user);
alert(clone[id]); // 123
```

##### 전역 심볼

- 심볼은 이름이 같더라도 모두 별개로 취급된다.
- 이름이 같은 심볼이 같은 개체를 가리키길 원하는 경우도 가끔 있다.
- 전역 심볼 레지스트리 안에 심볼을 만들고 해당 심볼에 접근하면 이름이 같은 경우 항상 동일한 심볼을 반환한다.
- 레지스트리 안에 있는 심볼을 읽거나, 새로운 심볼을 생성하려면 <code>Symbol.for(key)</code>를 사용해야 한다.
- 이 메소드를 호출하면 이름이 <code>key</code>인 심볼을 반환한다. 조건에 맞는 심볼이 레지스트리 안에 없으면 새로운 심볼 <code>Symbol(key)</code>을 만들고 레지스트리 안에 저장한다.

```js
// 전역 레지스트리에서 심볼을 읽는다.
let id = Symbol.for("id"); // 심볼이 존재하지 않으면 새로운 심볼을 만든다.

// 동일한 이름을 이용해 심볼을 다시 읽는다.
let idAgain = Symbol.for("id");

// 두 심볼은 같다.
alert(id === idAgain); // true
```

##### Symbol.keyFor

- <code>Symbol.keyFor(sym)</code>를 사용하면 이름을 얻을 수 있다.
- 전역 심볼 레지스트리를 뒤져서 해당 심볼의 이름을 얻어낸다.
- 검색 범위가 전역 심볼 레지스트리이기 때문에 전역 심볼이 아닌 심볼에는 사용할 수 없다.
- 전역 심볼이 아닌 인자가 넘어오면 <code>Symbol.keyFor</code>는 <code>undefined</code>를 반환한다.

```js
// 이름을 이용하여 심볼을 찾는다.
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// 심볼을 이용하여 이름을 얻는다.
alert(Symbol.keyFor(sym)); //name
alert(Symbol.keyFor(sym2)); //id
```

- 일반 심볼에서 이름을 얻고싶으면 <code>description</code>프로퍼티를 사용한다.

```js
let globalSymbol = Symbol.for("name");
let localSymbol = Symbol("name");

alert(Symbol.keyFor(globalSymbol)); // name, 전역 심볼
alert(Symbol.keyFor(localSymbol)); // undefined, 전역 심볼이 아님

alert(localSymbol.description); // name
```

##### 시스템 심볼

- 시스템 심볼은 자바스크립트 내부에서 사용되는 심볼이다. 시스템 심볼을 활용하면 객체를 미세 조정할 수 있다.
  - Symbol.hasInstance
  - Symbol.isConcatSpreadable
  - Symbol.iterator
  - Symbol.toPrimitive
  - 등등

### ch9 : 객체를 원시형으로 변환하기

- <code>obj.toString()</code>만 사용해도 '모든 변환'을 다 다룰 수 있기 때문에 실무에서 충분한 경우가 많다. 로깅이나 디버깅 목적으로도 자주 사용된다.
- 객체-원시형 형변환은 hint를 기준으로 3종류로 구분할 수 있다.
  - string : alert같이 문자열을 필요로 하는 연산
  - number : 수학연산
  - default : 드물게 발생

##### ToPrimitive

- 특수 객체 메서드를 사용하면 숫자형이나 문자형으로의 형 변환을 원하는 대로 조절할 수 있다.

- <code>string</code> : <code>alert</code> 함수같이 문자열을 기대하는 연산을 수행할 때는(객체-문자형 변환), hint가 <code>string</code>이 된다.

```js
// 객체를 출력하려고 함
alert(obj);

// 객체를 프로퍼티 키로 사용하고 있음
anotherObj[obj] = 123;
```

- <code>number</code> : 수학연산을 적용하려 할 때 (객체-숫자형 변환), hint는 number가 된다.

```js
// 명시적 형 변환
let num = Number(obj);

// (이항 덧셈 연산을 제외한)수학연산
let n = +obj; // 단항 덧셈 연산
let delta = date1 - date2;

// 대소 비교하기
let greater = user1 > user2;
```

- <code>default</code> : 연산자가 기대하는 자료형이 확실치 않을 때, hint는 default가 된다.

```js
// 이항 덧셈 연산은 hint로 default를 사용한다.
let total = obj1 + obj2;

// obj == number 연산은 hint로 default를 사용한다.
if( user == 1 ) { ... };
```

```js
let user = {
  name: "John",
  money: 1000,
  [Symbol.toPrimitive](hint) {
    alert(`hint : ${hint}`);
    return hint == "string" ? `{name : "${this.name}'}` : this.money;
  },
};
alert(user); // hint: string -> {name: "John"}
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500
```

- <code>user</code>는 hint에 따라 (자기 자신을 설명해주는)문자열로 변환되가도 하고 (갖고 있는 돈의 액수를 나타내는)숫자로 변환되기도 한다.
- <code>user[Symbol.toPrimitive]</code>를 사용하면 메서드 하나로 모든 종류의 형 변환을 다룰 수 있다.

##### toString과 valueOf

- 이 메소드를 사용하면 구식이나 형 변환을 직접 구현할 수 있다.
- 객체에 <code>Symbol.toPrimitive</code>가 없으면 아래 규칙에 따라 toString이나 valueOf를 호출한다.
  - hint가 'string'인 경우 : <code>toString -> valueOf</code> 순 (toString이 있으면 toString을 호출, toString이 없다면 valueOf를 호출함)
  - 그 외 : <code>valueOf -> toString </code> 순

```js
let user = { name: "John" };
alert(user); // [object Object]
alert(user.valueOf() === user); // true
```

- 아래 user는 toString과 valueOf를 조합하여 만들었다. Symbol.toPrimitive를 사용한 위쪽 예시와 동일하게 동작한다.

```js
let user = {
  name: "John",
  money: 1000,

  // hint가 "string"인 경우
  toString() {
    return `{name: "${this.name}"}`;
  },

  // hint가 "number"나 "default"인 경우
  valueOf() {
    return this.money;
  },
};

alert(user); // toString -> {name: "John"}
alert(+user); // valueOf -> 1000
alert(user + 500); // valueOf -> 1500
```

- 모든 형 변환을 한 곳에서 처리해야 하는 경우
- toString만 구현하면 된다.
- 객체에 Symbol.toPrimitive와 valueOf가 없으면 toString이 모든 형 변환을 처리한다.

```js
let user = {
  name: "John",

  toString() {
    return this.name;
  },
};

alert(user); // toString -> John
alert(user + 500); // toString -> John500
```

##### 반환 타입

- 위에서 소개한 3개의 메서드는 hint에 명시된 자료형으로의 형 변환을 보장해 주지 않는다.
- 확신할 수 있는 단 한 가지는 객체가 아닌 원시값을 반환해 준다는 것 뿐이다.
- 반면, Symbol.toPrimitive는 무조건 원시자료를 반환해야 한다. 아닐 시 에러가 발생한다.

##### 추가 형 변환

- 객체가 피연산자일 때는 다음과 같은 단계를 거쳐 형 변환이 일어난다.
  1. 객체는 원시형으로 변화된다.
  2. 변환 후 원시값이 원하는 형이 아닌 경우에는 또다시 형 변환이 일어난다.

```js
/*
1. obj * 2 에서는 객체가 원시형으로 변화되므로 toString에 의해 obj는 문자열 '2'가 된다. 
2. 곱셈 연산은 문자열을 숫자형으로 변화시키므로 '2' * 2는 2 * 2 가 된다. 
*/

let obj = {
  // 다른 메서드가 없으면 toString에서 모든 형 변환을 처리한다.
  toString() {
    return "2";
  },
};
alert(obj * 2); //4 객체가 문자열 '2'로 바뀌고 곱셉 연산 과정에서 숫자 2로 변경된다.
```

```js
// 이항 덧셈 연산에서는 같은 상황에서 문자열을 연결한다.
let obj = {
  toString() {
    return "2";
  },
};

alert(obj + 2); // 22("2" + 2), 문자열이 반환되기 때문에 문자열끼리의 병합이 일어났습니다.
```
