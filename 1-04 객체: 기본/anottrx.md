<br />
<h1 align="center">1-04 객체: 기본</h1>
<br />

## 1. 객체

- 객체 : 중괄호 `{…}`로 작성.
  - 중괄호 안에는 `키(key): 값(value)` 쌍으로 구성된 프로퍼티(property) 여러 개 작성 가능
  - 키엔 문자형, 값엔 모든 자료형이 허용 (프로퍼티 키 = 프로퍼티 이름)
- 리터럴과 프로퍼티
  ```js
  let user = { // 객체
    name: "John", // 키: "name",  값: "John" (첫번째 프로퍼티)
    age: 30, // 키: "age", 값: 30 (두번째 프로퍼티)
    "likes birds": true // 복수의 단어는 따옴표 필요
  };

  user.isAdmin = true; // 추가
  delete user.age; // 삭제
  user.name = "Pete"; // 수정
  ```
- 마지막 프로퍼티의 끝에 붙는 쉼표 : ‘trailing(길게 늘어지는)’ 혹은 ‘hanging(매달리는)’ 쉼표
- 대괄호 표기법(square bracket notation)
  - 점은 키가 유효한 변수 식별자인 경우만 사용 가능
    - 유효한 변수 식별자 : 공백이 없고 숫자로 시작하지 않으며 $와 _를 제외한 특수 문자가 없는 경우
  ```js
  let user = {};
  let key = "likes birds";
  user[key] = true; // set

  alert(user["likes birds"]); // get (true)
  delete user["likes birds"]; // delete

  alert( user[key] ); // true
  alert( user.key ); // undefined
  ```
- 계산된 프로퍼티(computed property) 
  ```js
  let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");
  let bag = {
    [fruit]: 5, // 변수 fruit에서 프로퍼티 이름을 동적으로 받는다
  };
  alert( bag.apple ); // fruit에 "apple"이 할당되었다면, 5가 출력
  ```
- 대괄호 표기법은 작성하기 번거롭다는 단점 때문에, 프로퍼티 이름이 확정된 상황이고, 단순한 이름이라면 처음엔 점 표기법을 사용하다가 복잡해질 때 대괄호 표기법으로 바꾸는 편이다
- 단축 프로퍼티 : 프로퍼티 값 단축 구문(property value shorthand) 을 사용
  ```js
  let user = {
    name,  // name: name 과 같음
    age: 30
  };
  ```
- 프로퍼티 이름의 제약사항
  - 변수 이름에 예약어를 사용하면 안되지만, 객체 프로퍼티는 제약이 없다
  ```js
  let obj = {
    for: 1,
    let: 2,
    return: 3
  };
  alert( obj.for + obj.let + obj.return );  // 6
  ```
  - __proto__는 특별 대우
  ```js
  let obj = {};
  obj.__proto__ = 5; // 숫자를 할당
  alert(obj.__proto__); // [object Object] - 숫자를 할당했지만 값은 객체가 되어 의도한대로 되지 않는다
  ```
- ‘in’ 연산자로 프로퍼티 존재 여부 확인하기
  - 존재하지 않는 프로퍼티에 접근하면 에러가 아니라 undefined 반환
  ```js
  let user = { name: "John", age: 30 };
  alert( "age" in user ); // true
  alert( "blabla" in user ); // false
  ```
  ```js
  let obj = {
    test: undefined
  };
  alert( obj.test ); // undefined인데 값이 undefined인지 키가 없어서 undefined인지 알 수 없다
  ```
- ‘for…in’ 반복문
  ```js
  let user = {
    name: "John",
    age: 30,
    isAdmin: true
  };

  for (let key in user) {
    alert( key );  // name, age, isAdmin
    alert( user[key] ); // John, 30, true
  }
  ```
- 객체 정렬 방식 : 정수 프로퍼티(integer property)는 자동으로 정렬되고, 그 외의 프로퍼티는 객체에 추가한 순서 그대로 정렬
  ```js
  let codes = {
    "49": "독일",
    "41": "스위스",
    "44": "영국",
    // ..,
    "1": "미국"
  };
  for (let code in codes) {
    alert(code); // 1, 41, 44, 49
  }
  ```
- 자바스크립트의 객체
  - 일반 객체 (순수 객체(plain object))
  - Array : 정렬된 데이터 컬렉션을 저장할 때 쓰임
  - Date : 날짜와 시간 정보를 저장할 때 쓰임
  - Error : 에러 정보를 저장할 때 쓰임

### 과제
```js
let schedule = {};
alert( isEmpty(schedule) ); // true
schedule["8:30"] = "get up";
alert( isEmpty(schedule) ); // false

function isEmpty(obj) {
  for (let key in obj) { // 객체가 비었는지 확인
    return false;
  }
  return true;
}
```
```js
// 함수 호출 전
let menu = {
  width: 200,
  height: 300,
  title: "My menu"
};

multiplyNumeric(menu);

// 함수 호출 후
menu = {
  width: 400,
  height: 600,
  title: "My menu"
};

function multiplyNumeric(obj) {
  for (let key in obj) {
    if (typeof obj[key] == 'number') {
      obj[key] *= 2;
    }
  }
}
```

<br />

## 2. 참조에 의한 객체 복사

- 객체와 원시 타입의 차이 중 하나는 객체는 참조에 의해(by reference) 저장되고 복사된다는 것
- 변수엔 객체가 그대로 저장되는 것이 아니라, 객체가 저장되어있는 '메모리 주소’인 객체에 대한 '참조 값’이 저장
- 객체가 할당된 변수를 복사할 땐 객체의 참조 값이 복사되고 객체는 복사되지 않는다
  ```js
  let user = { name: 'John' };
  let admin = user;
  admin.name = 'Pete'; // 'admin' 참조 값에 의해 변경
  alert(user.name); // Pete. 'user' 참조 값을 이용해 변경사항을 확인함
  ```
- 비교 시 피연산자인 두 객체가 동일한 객체인 경우에 참을 반환
- 참조에 의한 비교 : 피연산자인 두 객체가 동일한 객체인 경우에 참을 반환
  ```js
  let a = {};
  let b = a; // 참조에 의한 복사

  alert( a == b ); // true
  alert( a === b ); // true

  let c = {}; // 독립된 두 객체
  alert( a == c ); // false
  ```
- 객체 복사, 병합과 Object.assign
  ```js
  let user = {
    name: "John",
    age: 30
  };

  let clone = {}; // 새로운 빈 객체
  for (let key in user) { // 복사
    clone[key] = user[key];
  }
  clone.name = "Pete";
  alert( user.name ); // John

  // permissions1과 permissions2의 프로퍼티를 user로 복사합니다.
  let permissions1 = { canView: true };
  let permissions2 = { canEdit: true };
  Object.assign(user, permissions1, permissions2);
  // user = { name: "John", canView: true, canEdit: true }
  ```
  ```js
  let user = { name: "John" };
  Object.assign(user, { name: "Pete" });
  alert(user.name); // user = { name: "Pete" }
  ```
  ```js
  let user = {
    name: "John",
    age: 30
  };
  // 반복문 없이 객체 복사
  let clone = Object.assign({}, user);
  ```
- 중첩 객체 복사
  ```js
  let user = {
    name: "John",
    sizes: {
      height: 182,
      width: 50
    }
  };

  let clone = Object.assign({}, user);
  alert( user.sizes === clone.sizes ); // true
  // user와 clone는 sizes를 공유
  user.sizes.width++; // 프로퍼티 변경
  alert(clone.sizes.width); // 51, 다른 객체에서도 변경
  ```
  - 깊은 복사(deep cloning) 필요
    -  lodash의 메서드 _.cloneDeep(obj) 활용

<br />

## 3. 가비지 컬렉션

- 가비지 컬렉션 기준
  - 도달 가능성(reachability) 이라는 개념을 사용해 메모리 관리를 수행
  - 명백한 이유 없이 삭제되지 않는 예시들 → 루트(root)
    - 현재 함수의 지역 변수와 매개변수
    - 중첩 함수의 체인에 있는 함수에서 사용되는 변수와 매개변수
    - 전역 변수
  - 루트가 참조하는 값이나 체이닝으로 루트에서 참조할 수 있는 값은 도달 가능한 값이 된다
- 자바스크립트 엔진 내에선 가비지 컬렉터(garbage collector)가 끊임없이 동작 → 가비지 컬렉터는 모든 객체를 모니터링하고, 도달할 수 없는 객체는 삭제
  ```js
  let user = { // user엔 객체 참조 값이 저장
    name: "John"
  };

  user = null; // John은 도달할 수 없는 상태
  // 가비지 컬렉터는 이제 John에 저장된 데이터를 삭제하고, John을 메모리에서 삭제
  ```
- mark-and-sweep 가비지 컬렉션 기본 알고리즘
  - 가비지 컬렉터는 루트(root) 정보를 수집하고 이를 mark(기억)
  - 루트가 참조하고 있는 모든 객체를 방문하고 이것들을 mark
  - mark 된 모든 객체에 방문하고 그 객체들이 참조하는 객체도 mark. 한번 방문한 객체는 전부 mark 하기 때문에 같은 객체를 다시 방문하는 일은 없다
  - 루트에서 도달 가능한 모든 객체를 방문할 때까지 위 과정을 반복
  - mark 되지 않은 모든 객체를 메모리에서 삭제
- 최적화 기법
  - generational collection(세대별 수집) : 객체를 '새로운 객체’와 '오래된 객체’로 나눈다. 객체 상당수는 생성 이후 제 역할을 빠르게 수행해 금방 쓸모가 없어지는데, 이런 객체를 '새로운 객체’로 구분한다. 가비지 컬렉터는 이런 객체를 공격적으로 메모리에서 제거. 일정 시간 이상 동안 살아남은 객체는 '오래된 객체’로 분류하고, 가비지 컬렉터가 덜 감시
  - incremental collection(점진적 수집) : 방문해야 할 객체가 많다면 모든 객체를 한 번에 방문하고 mark 하는데 상당한 시간이 소모되고, 가비지 컬렉션에 많은 리소스가 사용되어 실행 속도도 느려질 것이다. 자바스크립트 엔진은 이런 현상을 개선하기 위해 가비지 컬렉션을 여러 부분으로 분리한 다음, 각 부분을 별도로 수행. 작업을 분리하고, 변경 사항을 추적하는 데 추가 작업이 필요하긴 하지만, 긴 지연을 짧은 지연 여러 개로 분산시킬 수 있다
  - idle-time collection(유휴 시간 수집) : 가비지 컬렉터는 실행에 주는 영향을 최소화하기 위해 CPU가 유휴 상태일 때에만 가비지 컬렉션을 실행

### 요약
- 가비지 컬렉션은 엔진이 자동으로 수행하므로 개발자는 이를 억지로 실행하거나 막을 수 없다
- 객체는 도달 가능한 상태일 때 메모리에 남는다
- 참조된다고 해서 도달 가능한 것은 아니다. 서로 연결된 객체들도 도달 불가능할 수 있다
- [V8 공식 블로그](https://v8.dev/)의 메모리 관리 방법 변화
- 가비지 컬렉션을 심도 있게 학습하려면 V8 내부구조를 공부하거나 V8 엔지니어로 일했던 [Vyacheslav Egorov의 블로그](https://mrale.ph/)

<br />

## 4. 메서드와 this

```js
let user = {
  name: "John",
  age: 30
};

user.sayBye = function() { // 메서드
  alert("안녕히 가세요!");
};

function sayHi() { // 함수 선언
  alert("안녕하세요!");
};
user.sayHi = sayHi; // 선언된 함수를 메서드로 등록
```

- 메서드 내부에서 this 키워드를 사용하면 객체에 접근할 수 있다
  ```js
  let user = {
    name: "John",
    age: 30,

    sayHi() {
      alert(this.name); // 'this'는 '현재 객체'
    }
  };

  user.sayHi(); // John
  ```
- 자유로운 this
  ```js
  let user = { name: "John" };
  let admin = { name: "Admin" };

  function sayHi() {
    alert( this.name );
  }

  // 별개의 객체에서 동일한 함수를 사용함
  user.f = sayHi;
  admin.f = sayHi;

  // 'this'는 '점(.) 앞의' 객체를 참조하기 때문에 this 값이 달라짐
  user.f(); // John  (this == user)
  admin.f(); // Admin  (this == admin)

  admin['f'](); // Admin (점과 대괄호는 동일하게 동작함)
  ```
- 객체 없이 호출하기
  ```js
  function sayHi() {
    alert(this);
  }
  sayHi(); // 엄격 모드에서는 undefined
  // 엄격 모드가 아닐 경우 this는 전역 객체를 참조. 브라우저 환경에서는 window 전역 객체를 참조
  ```
- this가 없는 화살표 함수
  ```js
  let user = {
    firstName: "보라",
    sayHi() {
      let arrow = () => alert(this.firstName);
      arrow();
    }
  };
  user.sayHi(); // 보라
  ```
- this 값은 런타임에 결정된다
  - 함수를 선언할 때 this를 사용할 수 있다. 다만 함수가 호출되기 전까지 this엔 값이 할당되지는 않는다
  - 함수를 복사해 객체 간 전달할 수 있다
  - 함수를 객체 프로퍼티에 저장해 object.method()같이 ‘메서드’ 형태로 호출하면 this는 object를 참조
- 화살표 함수는 자신만의 this를 가지지 않는다. 화살표 함수 안에서 this를 사용하면, 외부에서 this 값을 가져온다

### 과제
```js
function makeUser() {
  return {
    name: "John",
    ref: this,
    ref2() {
      return this;
    }
  };
};

let user = makeUser();

alert( user.ref.name ); // Error: Cannot read property 'name' of undefined
alert( user.ref2().name ); // John
```
```js
let calculator = {
  sum() {
    return this.a + this.b;
  },
  mul() {
    return this.a * this.b;
  },
  read() {
    this.a = +prompt('첫 번째 값:', 0);
    this.b = +prompt('두 번째 값:', 0);
  }
};

calculator.read();
alert( calculator.sum() );
alert( calculator.mul() );
```
```js
let ladder = {
  step: 0,
  up() {
    this.step++;
    return this;
  },
  down() {
    this.step--;
    return this;
  },
  showStep() {
    alert( this.step );
    return this;
  }
}
ladder.up().up().down().showStep(); // 1
```

<br />

## 5. new 연산자와 생성자 함수

> 'new' 연산자와 생성자 함수를 사용하면 유사한 객체 여러 개를 쉽게 생성 가능

- 생성자 함수(constructor function)
  - 함수 이름의 첫 글자는 대문자로 시작
  - 반드시 'new' 연산자를 붙여 실행
  ```js
  function User(name) {
    // this = {};  (빈 객체가 암시적으로 만들어짐)
    this.name = name;
    this.isAdmin = false;
    // return this;  (this가 암시적으로 반환됨)
  }

  let user = new User("보라");
  alert(user.name); // 보라
  ```
  - 모든 함수는 생성자 함수가 될 수 있다
  - 익명 함수는 저장되지 않고, 한 번만 호출할 목적으로 만들어지기 때문에 재사용 불가능 → 코드 캡슐화
- new.target과 생성자 함수 (자주 사용하지 않는다)
  - new가 있으면 새로운 객체를 만드는 것을 누구나 알 수 있기 때문에 정말 필요할 때만 new 생략할 것
  ```js
  function User() {
    alert(new.target);
  }

  // 'new' 없이 호출함
  User(); // undefined

  // 'new'를 붙여 호출함
  new User(); // function User { ... }  
  ```
  ```js
  function User(name) {
    if (!new.target) { // new 없이 호출해도
      return new User(name); // new를 붙여준다
    }
    this.name = name;
  }

  let bora = User("보라"); // 'new User'를 쓴 것처럼 바꿔준다
  alert(bora.name); // 보라  
  ```
- 생성자와 return문
  - 객체를 return 한다면 this 대신 객체가 반환
  - 원시형을 return 한다면 return문이 무시
  ```js
  function BigUser() {
    this.name = "원숭이";

    return { name: "고릴라" };  // this가 아닌 새로운 객체를 반환함
  }
  alert( new BigUser().name );  // 고릴라  

  function SmallUser() {
    this.name = "원숭이";
    return; // this를 반환함
  }
  alert( new SmallUser().name );  // 원숭이
  ```  
  - return문이 있는 생성자 함수는 별로 없다
- 인수가 없는 생성자 함수는 괄호를 생략해 호출 가능 → 좋은 스타일은 아님
  ```js
  let user = new User; // 괄호가 없지만 아래와 동일
  let user = new User();
  ```
- 생성자 내 메서드 더하기도 가능

### 요약

- 생성자 함수(짧게 줄여서 생성자)는 일반 함수다. 다만, 일반 함수와 구분하기 위해 함수 이름 첫 글자를 대문자로 쓴다
- 생성자 함수는 반드시 new 연산자와 함께 호출해야 한다. new와 함께 호출하면 내부에서 this가 암시적으로 만들어지고, 마지막엔 this가 반환된다
- 생성자 함수는 유사한 객체를 여러 개 만들 때 유용

### 과제

```js
let obj = {};
function A() { return obj; }
function B() { return obj; }
alert( new A() == new B() ); // true
```
```js
function Calculator() {
  this.read = function() {
    this.a = +prompt('a?', 0);
    this.b = +prompt('b?', 0);
  };
  this.sum = function() {
    return this.a + this.b;
  };
  this.mul = function() {
    return this.a * this.b;
  };
}

let calculator = new Calculator();
calculator.read();
alert( "Sum=" + calculator.sum() );
alert( "Mul=" + calculator.mul() );
```
```js
function Accumulator(startingValue) {
  this.value = startingValue;
  this.read = function() {
    this.value += +prompt('value?', 0);
  };
}

let accumulator = new Accumulator(1);
accumulator.read(); // 사용자가 입력한 값을 더해줌
alert(accumulator.value); 
```

<br />

## 6. 옵셔널 체이닝 '?.'

> 스펙에 추가된 지 얼마 안 된 문법으로, 구식 브라우저는 폴리필이 필요      
> 옵셔널 체이닝(optional chaining) `?.`을 사용하면 프로퍼티가 없는 중첩 객체를 에러 없이 안전하게 접근 가능

- 옵셔널 체이닝이 필요한 이유
  ```js
  // 옵셔널 체이닝이 없을 때는 아래처럼 작성했는데, 코드가 길어졌다
  let user = {}; // 주소 정보가 없는 사용자
  alert( user && user.address && user.address.street ); // undefined, 에러가 발생하지 않습니다.
  ```
- 옵셔널 체이닝의 등장
  - `?.`은 `?.` 앞의 평가 대상이 undefined나 null이면 평가를 멈추고 undefined를 반환
  ```js
  let user = null;
  alert( user?.address ); // undefined
  alert( user?.address.street ); // undefined
  ```
- 옵셔널 체이닝을 남용하지 않아야 한다
- ?.앞의 변수는 꼭 선언되어 있어야 한다
  ```js
  // ReferenceError: user is not defined
  user?.address;
  ```
- 단락 평가(short-circuit) : 평가대상에 값이 없으면 즉시 평가를 멈춘다
- `?.()`와 `?.[]`
  - `?.`는 연산자가 아니고, 함수나 대괄호와 함께 동작하는 특별한 문법 구조체(syntax construct)
  - `?.()` : 존재 여부가 확실치 않은 함수를 호출할 때 사용
    ```js
    let user1 = {
      admin() {
        alert("관리자 계정입니다.");
      }
    }

    let user2 = {};
    user1.admin?.(); // 관리자 계정입니다.
    user2.admin?.();
    ```
  - `?.[]`를 사용하면 객체 존재 여부가 확실치 않은 경우에도 안전하게 프로퍼티 읽기 가능
  ```js
  let user1 = {
    firstName: "Violet"
  };

  let user2 = null; // user2는 권한이 없는 사용자라고 가정

  let key = "firstName";
  alert( user1?.[key] ); // Violet
  alert( user2?.[key] ); // undefined
  alert( user1?.[key]?.something?.not?.existing); // undefined
  ```
- ?.은 읽기나 삭제하기에는 사용할 수 있지만 쓰기는 불가능
  ```js
  delete user?.name; // user가 존재하면 user.name을 삭제
  user?.name = "Violet"; // SyntaxError: Invalid left-hand side in assignment
  // 에러가 발생하는 이유는 undefined = "Violet"이 되기 때문입니다.
  ```

<br />

## 7. 심볼형

<br />

## 8. 객체를 원시형으로 변환하기

<br />
<br />
