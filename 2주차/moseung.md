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




