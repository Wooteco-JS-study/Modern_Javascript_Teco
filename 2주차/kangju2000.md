# 프라미스와 async, await

## 동기 처리
함수를 호출하면 함수 코드가 평가되어 함수 실행 컨텍스트가 생성된다. 이때 실행 컨텍스트 스택(콜 스택)에 푸시되고 함수 코드가 실행된다. 실행이 종료되면 함수 실행 컨텍스트는 실행 컨텍스트 스택에서 팝되어 제거된다.

자바스크립트 엔진은 단 하나의 실행 컨텍스트 스택을 가지고,  한 번에 하나의 태스크만 실행할 수 있는 **싱글 스레드** 방식으로 동작한다. 만약 시간이 걸리는 태스크를 실행하는 경우 **블로킹**이 발생한다.

## 비동기 처리
비동기 처리를 위해 콜백 패턴을 사용한다. 하지만 **콜백 헬** 을 발생시켜 가독성을 나쁘게 하고, 비동기 처리 중 발생한 에러의 예외 처리가 곤란하며, 여러 개의 비동기 처리를 한 번에처리하는 데도 한계가 있다.

```js
loadScript('1.js', function(error, script) {

  if (error) {
    handleError(error);
  } else {
    // ...
    loadScript('2.js', function(error, script) {
      if (error) {
        handleError(error);
      } else {
        // ...
        loadScript('3.js', function(error, script) {
          if (error) {
            handleError(error);
          } else {
          // ...
          }
        });

      }
    })
  }
});
```

### 태스크 큐(task queue/evnet queue/callback queue)
비동기 함수의 콜백 함수 또는 이벤트 핸들러가 일시적으로 보관되는 영역이다.

### 이벤트 루프(event loop)
콜 스택에 현재 실행 중인 실행 컨텍스트가 있는지, 그리고 태스크 큐에 대기 중인 함수가 있는지 반복해서 확인한다.
만약 콜 스택이 비어 있고 태스크 큐에 대기 중인 함수가 있다면 이벤트 루프는 순차적(FIFO)으로 태스크 큐에 대기 중인 함수를 콜 스택으로 이동시킨다.

![](https://t1.daumcdn.net/cfile/tistory/99A7234F5C321A7F2B)


함수가 호출되면 실행 컨텍스트가 생성되어 콜 스택에 푸시되어 실행된다. 이 때 콜백 함수를 호출 스케줄링하고 종료되어 콜 스택에서 팝된다. 이때 타이머가 만료되면 콜백 함수를 태스크 큐에 푸시하는데, 이는 브라우저의 역할이다.
콜 스택이 비어있고 태스크 큐에 대기중인 함수가 있다면 **이벤트 루프**가 순차적으로 태스크 큐에 대기 중인 함수를 콜 스택으로 이동시킨다.

### 왜 예외 처리가 곤란할까?
비동기 함수인 `setTimeout` 함수에서 1초 후에 콜백 함수가 실행되도록 타이머를 설정하고 이후 콜백 함수가 에러를 발생시킨다고 하자. 하지만 catch 코드 블록에서 캐치되지 않는다.

```js
try {
	setTimeout(() => { throw new Error('Error!'); }. 1000);
} catch (e) {
	console.error('캐치한 에러', e);
}
```
![](https://miro.medium.com/max/700/1*0FSent9cSo2b5ggUdtKPWQ.png)

에러는 호출자 방향으로 전파된다. 콜 스택의 아래방향으로 전파된다. 하지만 setTimeout 함수의 콜백함수를 호출한 것은 setTimeout 함수가 아니기 때문에 캐치되지 않는다.
콜 스택에 푸시된 콜백 함수의 실행 컨텍스트는 콜 스택의 가장 하부에 존재하게 되기 때문에, 에러를 전파할 호출자가 존재하지 않는다.

에러 핸들링 방법은 콜백 함수 내부에 try...catch를 구현하면 된다.


### 비동기 처리 예제
```js
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"), 500);
const baz = () => console.log("Third");

bar();
foo();
baz();
```

![img](https://www.devh.kr/assets/images/post/javascript-visualized-event-loop/gif14.1.gif)



## Promise
ES6에서 비동기 처리를 위한 또 다른 패턴으로 Promise를 도입했다. 
![](https://github.com/javascript-tutorial/ko.javascript.info/raw/master/1-js/11-async/02-promise-basics/promise-resolve-reject.svg)

- pending 상태: 비동기 처리가 수행되지 않은 상태
- fulfilled 상태: 비동기 처리가 수행된 상태(성공)
- rejected 상태: 비동기 처리가 수행된 상태(실패)

fulfilled와 rejected 상태를 합쳐서 settled 상태라고 한다. 성공 여부 상관없이 비동기 처리가 수행된 상태를 말한다.

## Promise 후속 처리 메서드
### Promise.prototype.then
두 개의 콜백 함수를 인수로 전달받는다.
- 첫 번째 콜백 함수는 fulfilled 상태가 되면 호출된다.
- 두 번째 콜백 함수는 rejected 상태가 되면 호출된다.

### Promise.prototype.catch
한 개의 콜백 함수를 인수로 전달받는다.
- 콜백 함수는 rejected 상태인 경우만 호출된다.

### Promise.prototype.finally
한 개의 콜백 함수를 인수로 전달받는다.
- 성공, 실패 상관없이 무조건 한 번 호출된다.

```js
function checkMail() {
  return new Promise((resolve, reject) => {
    if (Math.random() > 0.5) {
      resolve('Mail has arrived');
    } else {
      reject(new Error('Failed to arrive'));
    }
  });
}

checkMail()
  .then((mail) => {
    console.log(mail);
  })
  .catch((err) => {
    console.error(err);
  })
  .finally(() => {
    console.log('Experiment completed');
  });
```

## Promise Chaining
```js
new Promise(function(resolve, reject) {
  setTimeout(() => resolve(1), 1000); 
}).then(function(result) {
  alert(result); // 1
  return result * 2;
}).then(function(result) { 
  alert(result); // 2
  return result * 2;
}).then(function(result) {
  alert(result); // 4
  return result * 2;
});
```
![](https://github.com/javascript-tutorial/ko.javascript.info/raw/master/1-js/11-async/03-promise-chaining/promise-then-chain.svg)

## Promise의 정적 메서드
### Promise.resolve / Promise.reject
- `Promise.resolve(value)`는 결괏값이 `value`인 이행 상태 Promise를 생성한다.
- `Promise.reject(error)`는 결괏값이 `error`인 거부 상태 Promise를 생성한다.

### Promise.all
모든 Promise가 이행될 때까지 기다렸다가 그 결괏값을 담은 배열을 반환한다. 주어진 프라미스 중 하나라도 실패하면 `Promise.all`는 거부되고, 나머지 Promise의 결과는 무시된다.
```js
Promise.all([
  new Promise(resolve => setTimeout(() => resolve(1), 3000)), // 1
  new Promise(resolve => setTimeout(() => resolve(2), 2000)), // 2
  new Promise(resolve => setTimeout(() => resolve(3), 1000))  // 3
]).then(alert); // 프라미스 전체가 처리되면 1, 2, 3이 반환됩니다. 각 프라미스는 배열을 구성하는 요소가 됩니다.
```
### Promise.race
가장 먼저 fulfilled 상태가 된 Promise의 처리 결과(혹은 에러)를 반환한다.
```js
Promise.race([
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error("에러 발생!")), 2000)),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 3000))
]).then(alert); // 1
```

### Promise.allSettled
ES11에 도입된 메서드이다. 
전달받은 Promise가 모두 settled 상태가 되면 처리 결과를 배열로 반환한다.
-   응답이 성공할 경우 –  `{status:"fulfilled", value:result}`
-   에러가 발생한 경우 –  `{status:"rejected", reason:error}`

## Promise 에러 핸들링
-   `.catch`  는 프라미스에서 발생한 모든 에러를 다룬다.  `reject()`가 호출되거나 에러가 던져지면  `.catch`에서 이를 처리한다.
- `.catch`를 추가하지 않았을 때 에러 발생하면 자바스크립트 엔진은 Promise rejected를 추적하다가 전역 에러를 생성한다.
	- 브라우저 환경에선 이런 에러를 `unhandledrejection` 이벤트로 처리할 수 있다.

```js
window.addEventListener('unhandledrejection', function(event) {
  // unhandledrejection 이벤트엔 두 개의 특수 프로퍼티가 있습니다.
  alert(event.promise); // [object Promise] - 에러를 생성하는 프라미스
  alert(event.reason); // Error: 에러 발생! - 처리하지 못한 에러 객체
});

new Promise(function() {
  throw new Error("에러 발생!");
}); // 에러를 처리할 수 있는 .catch 핸들러가 없음
```

## 마이크로태스크 큐
태스크 큐와는 별개의 큐이다. Promise의 후속 처리 메서드의 콜백 함수가 일시 저장된다.
- 태스크 큐보다 우선순위가 높다.
- 이벤트 루프는 콜 스택이 비면 먼저 마이크로태스크 큐에서 대기하고 있는 함수를 가져와 실행한다. 그 다음 마이크로태스크 큐가 비면 태스크 큐에 대기하고 있는 함수를 가져와 실행한다.

## async와 await
ES8에 도입되었다.
- Promise를 기반으로 동작한다.
- Promise의 후속 처리 메서드 없이 마치 동기 처리처럼 Promise가 처리 결과를 반환하도록 구현할 수 있다.

### async 함수
- function 앞에 `async`를 붙이면 해당 함수는 항상 Promise를 반환한다. 
- Promise가 아닌 값을 반환하더라도 resolve하는 promise로 값을 감싸 반환한다.
- 클래스의 constructor 메서드는 async 메서드가 될 수 없다.
	- constructor 메서드는 인스턴스를 반환해야하지만, async 함수는 언제나 프로미스를 반환해야한다.

### await 키워드
- settled 상태가 되면 resolve한 처리 결과를 반환한다.
- thenable 객체 사용할 수 있다.
	- thenable : then 메서드를 가진 객체

```js
class Thenable {
  constructor(num) {
    this.num = num;
  }
  then(resolve, reject) {
    alert(resolve);
    // 1000밀리초 후에 이행됨(result는 this.num*2)
    setTimeout(() => resolve(this.num * 2), 1000); // (*)
  }
};

async function f() {
  // 1초 후, 변수 result는 2가 됨
  let result = await new Thenable(1);
  alert(result);
}

f();
```
