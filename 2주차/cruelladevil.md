# 프로토타입

> 8장 - "프로토타입과 프로토타입 상속"에 관한 내용입니다.

## 목차

1. [프로토타입이란?](#프로토타입이란)
1. [프로토타입 상속](#프로토타입-상속)
1. [프로토타입 체이닝의 제약사항](#프로토타입-체이닝의-제약사항)
1. [for..in 반복문](#forin-반복문)
1. [생성자 함수](#생성자-함수)
1. [클래스와 프로토타입은 뭐가 다를까?](#클래스와-프로토타입은-뭐가-다를까)

## 프로토타입이란?

프로토타입(prototype)은 원형이라는 뜻이다.  
자바스크립트의 모든 객체는 자신의 부모 역할을 하는 객체와 연결되어 있다.  
이 부모 객체를 프로토타입 객체 또는 프로토타입이라고 한다.

## 프로토타입 상속

객체에서 프로퍼티(property)를 읽으려고 하는데 해당 프로퍼티가 없으면,  
자바스크립트는 자동으로 프로토타입에서 프로퍼티를 찾는다.  
프로그래밍에선 이런 동작 방식을 '프로토타입 상속'이라고 부른다.

```js
const arr = [4, 3, 5, 2, 1];

arr.sort(); // [1, 2, 3, 4, 5]
```

arr 배열 객체는 sort 라는 메서드를 가지고 있지 않다.  
그렇기 때문에 자신의 프로토타입에서 sort 메서드를 찾아 실행한다.

### \[\[Prototype\]\]

자바스크립트의 객체는 명세서에서 명명한 `[[Prototype]]`이라는 인터널 슬롯[^1]을 갖는다.  
\[\[Prototype\]\]은 `null`이나 `객체`에 대한 참조를 갖는데,  
객체를 참조하는 경우 참조 대상을 '프로토타입'이라 부른다.

### \_\_proto\_\_

\_\_proto\_\_는 \[\[Prototype\]\]을 대신하는 getter 및 setter 이다.  
하위 호환성 떄문에 여전히 \_\_proto\_\_를 사용할 순 있지만,  
근래에는 `Object.getPrototypeOf`나 `Object.setPrototypeOf`를 사용한다.

## 프로토타입 체이닝의 제약사항

1. 순환 참조(circular reference)는 허용되지 않는다.
2. `null`이나 `객체`만 참조할 수 있다. 다른 자료형은 무시된다.
3. 오직 하나만 상속받을 수 있다.

## for..in 반복문

`for..in` 반복문은 상속 프로퍼티도 순회대상에 포함시킨다.

```js
const animal = {
  canEat: true,
};

const rabbit = {
  canJump: true,
  __proto__: animal,
};

// Object.keys는 객체 자신의 키만 반환한다.
console.log(Object.keys(rabbit)); // canJump

// for..in 은 객체 자신의 키와 상속 프로퍼티의 키 모두를 순회한다.
for (const prop in rabbit) {
  console.log(prop); // canJump, canEat
}
```

`Object.prototype.hasOwnProperty(key)`를 사용하면 상속 프로퍼티를 순회 대상에서 제외할 수 있다.

```js
for (const prop in rabbit) {
  if (rabbit.hasOwnProperty(prop)) {
    console.log(`객체 자신의 프로퍼티: ${prop}`); // 객체 자신의 프로퍼티: canJump
  } else {
    console.log(`상속 프로퍼티: ${prop}`); // 상속 프로퍼티: canEat
  }
}
```

for..in 반복문은 enumerable[^2]한 속성들만 순회 대상에 포함시키기 때문에,  
length 같은 프로퍼티나 기타 내장 객체 메소드들은 나오지 않는다.

### Object.prototype.hasOwnProperty.call(this, prop)

**hasOwnProperty 메소드도 프로퍼티다.**  
hasOwnProperty라는 이름의 프로퍼티가 오버라이딩 된다면 의도한 대로 동작하지 않을 수 있다.

```js
const animal = {
  hasOwnProperty(prop) {
    console.log(`${prop}을 찾고 싶어도 찾을 수 없습니다.`);
  },

  canEat: true,
};

animal.hasOwnProperty('canEat'); // canEat을 찾고 싶어도 찾을 수 없습니다.

Object.prototype.hasOwnProperty.call(animal, 'canEat'); // true
Object.hasOwn(animal, 'canEat'); // true
```

**prototype이 null이라면?**

```js
const nullPrototype = Object.create(null);

nullPrototype.name = 'jungmin';

nullPrototype.hasOwnProperty('name');
// TypeError: nullPrototype.hasOwnProperty is not a function
// 프로토타입이 null이기 때문에 Object의 프로토타입 객체가 가진 hasOwnProperty 메서드에 접근할 수 없다.

Object.prototype.hasOwnProperty.call(nullPrototype, 'name'); // true
Object.hasOwn(nullPrototype, 'name'); // true
```

이러한 문제로 this를 묶어주고 call로 호출하였는데 이를 대체할 Object 생성자 함수에 hasOwn이라는 메서드가 생겼다.  
다만 비교적 최근에 생긴 스펙이므로 여전히 Object.prototype.hasOwnProperty.call이 많이 사용된다.

```js
const hasOwn = Object.prototype.hasOwnProperty;
hasOwn.call(this, prop);
```

## 생성자 함수

객체를 생성할 때 리터럴로 생성하더라도 생성자 함수로 생성한 것과 동일하다.  
생성자 함수의 prototype이 생성된 객체의 [[Prototype]]이 된다.

### prototype

`생성자함수`는 `prototype` 프로퍼티에 생성된 객체의 \[\[Prototype\]\]이 되는 객체를 가지고 있다.

### constructor

`프로토타입 객체`는 `constructor` 프로퍼티에 생성자 함수를 가지고 있다.

<img src = "https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ff75c238-d237-403d-b02c-58b8c4524bff/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-12-24_02.07.43.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221223%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221223T170828Z&X-Amz-Expires=86400&X-Amz-Signature=a75b9b2b534e63106d381757569782c58fb42a3e91192731483961eb08ecc21d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA%25202022-12-24%252002.07.43.png%22&x-id=GetObject" width="500px" />

## 클래스와 프로토타입은 뭐가 다를까?

> 원형 이론(prototype theory)에 대해 더 알아본다면,  
> 자바스크립트의 근간이 되는 prototype에 대해 조금 더 다가갈 수 있다.  
> 또한 this가 왜 문맥(context)에 따라 다른지도 설명 가능하며,  
> prototype 설계로 인한 장점과 단점에 대해 고민해 볼 수 있다.

### 고전 범주(Classification - 분류)

- 범주는 필요충분자질의 집합인 본질적 자질이다.
- 분명한 경계를 갖고 경계간 모호한 경우는 없다.
- 구성원의 자격은 동등하다. (범주 구성원 모두 동일한 속성 집합을 가진다고 보기 때문)

ex) 포유류 - 고래, 원숭이. 고래와 원숭이는 포유류에만 속하고 어류와 같은 다른 범주에 속할 수 없음.

### 원형 범주(Prototype - 원형)

- 범주 원소는 가족 닮음의 특성을 가진다.
  - 범주 구성원들의 공통 속성은 존재하지 않는다.
  - 몇몇 자질들만 중첩되고 교차된다. 공통이 아닌 유사.
- 범주 경계를 폐쇄적으로 보는 고전 범주화와 달리 원형 범주화는 개방적이며 경계가 모호하다. (퍼지 이론)
- 범주 원소는 계층성을 띈다.
  - 전형적이고 대표적인 것부터 비전형적인 것까지 연속체를 이룸.

ex) 무기 - 총, 연필. 총은 무기로써 전형적이고, 연필은 비전형적이지만 무기가 될 수는 있음.

### 프로토타입 참고 문헌

[자바스크립트는 왜 프로토타입을 선택했을까](https://medium.com/@limsungmook/자바스크립트는-왜-프로토타입을-선택했을까-997f985adb42)  
[wikipedia - prototype theory](https://en.wikipedia.org/wiki/Prototype_theory)  
[원형 이론 요약1](https://m.blog.naver.com/fnzh0814/115053452)  
[원형 이론 요약2](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=ms2948&logNo=220999019306)

[^1]: [인터널 슬롯](https://codingfarm.tistory.com/459) - 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 명세서에서 사용하는 의사 프로퍼티(pseudo property)다.
[^2]: enumerable - 프로퍼티 플래그이며 [property descriptor](https://ko.javascript.info/property-descriptors)를 확인해보면 좋다.
