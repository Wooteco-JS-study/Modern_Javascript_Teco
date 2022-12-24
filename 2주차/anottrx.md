# 모듈과 커링

## 목차

1. [13.1 모듈 소개](#1)
2. [13.2 모듈 내보내고 가져오기](#2)
3. [13.3 동적으로 모듈 가져오기](#3)
4. [14.3 커링](#4)

<br />

<div id="1"></div>

## [모듈 소개](https://ko.javascript.info/modules-intro)

- 모듈(module) : 대개 클래스 하나 혹은 특정한 목적을 가진 복수의 함수로 구성된 라이브러리 하나로 구성
- 초기 자바스크립트는 크기가 작고 기능도 단순해서 모듈 관련 문법이 없었지만, 스크립트 크기가 커지면서 모듈을 불러오거나 모듈 단위로 구성할 수 있게 되었다
  - AMD → require.js
  - CommonJS → Node.js 서버를 위해 만들어진 모듈 시스템
  - UMD → AMD와 CommonJS와 같은 다양한 모듈 시스템을 사용하기 위해 만들어졌다
- 모듈 시스템은 2015년에 표준으로 등재되고, 이제 대부분 주요 브라우저와 Node.js는 모듈 시스템을 지원한다

### 모듈이란

- 모듈 : 파일 하나 (스크립트 하나)
  - export → 모듈 내보내기
  - import → 모듈 가져오기
- 모듈은 로컬 파일에서 동작하지 않고, HTTP 또는 HTTPS 프로토콜을 통해서만 동작

```html
<!doctype html>
<script type="module">
  // 해당 스크립트가 모듈이란 걸 브라우저에게 알려줘야 한다
  import {sayHi} from './say.js';
  document.body.innerHTML = sayHi('John');
</script>
```

### ESM과 CJS

- CommonJS (CJS)
  - CJS module loader는 동기적으로 작동
  - CJS는 기본적으로 `require/module.exports` 를 동적으로 진행되기 때문에, 빌드 타임에 정적 분석을 적용하기 어렵고, 런타임에서만 모듈 관계를 파악할 수 있다
  - CJS가 기본값이다
  ```js
  // add.js
  module.exports.add = (x, y) => x + y;

  // main.js
  const { add } = require('./add');
  add(1, 2);
  ```
- ECMAScript Modules (ESM)
  - ESM module loader는 비동기적으로 작동
  - ESM 모듈 내의 모든 자식 스크립트들은 병렬로 다운로드 되지만, 실행은 순차적으로 진행
  - ESM은 정적인 구조로 모듈끼리 의존하도록 강제하기 때문에, 빌드 단계에서 정적 분석을 통해 모듈 간의 의존 관계를 파악할 수 있고, Tree-shaking이 쉽다
  ```js
  // add.js
  export function add(x, y) {
    return x + y
  }

  // main.js
  import { add } from './add.js';
  add(1, 2);
  ```
- 출처: [CommonJS와 ESM에 모두 대응하는 라이브러리 개발하기: exports field](https://toss.tech/article/commonjs-esm-exports-field), [CommonJS와 ES Modules은 왜 함께 할 수 없는가?](https://yceffort.kr/2020/08/commonjs-esmodules)

### 모듈의 핵심 기능

- 모듈은 항상 엄격 모드(use strict)로 실행
- 모듈은 자신만의 스코프가 있으므로 모듈 내에 정의한 변수나 함수는 다른 스크립트에서 접근 불가능 → export, import를 통해서는 가능

  ```html
  <script type="module">
    let user = "John"; // user는 해당 모듈 안에서만 접근 가능
  </script>

  <script type="module">
    alert(user); // Error: user is not defined
  </script>
  ```

- 모듈이 여러 곳에서 사용되더라도 최초 호출 시 한 번만 실행되고, 실행된 모듈은 필요한 곳에 공유되므로 한 모듈에서 객체를 수정하면 다른 모듈에서도 변경사항 확인 가능

  ```js
  // 📁 admin.js
  export let admin = { };

  export function sayHi() {
    alert(`${admin.name}님, 안녕하세요!`);
  }
  ```
  ```js
  // 📁 init.js
  import {admin} from './admin.js';
  admin.name = "보라"; // 이곳에서 admin.name을 설정
  ```
  ```js
  // 📁 other.js
  import {admin, sayHi} from './admin.js';

  alert(admin.name); // 보라

  sayHi(); // 보라님, 안녕하세요!
  ```

- import.meta 객체는 현재 모듈에 대한 정보 제공

  ```html
  <script type="module">
    alert(import.meta.url); // script URL (인라인 스크립트가 위치해 있는 html 페이지의 URL)
  </script>
  ```

- 모듈 최상위 레벨의 this는 undefined

  ```html
  <script>
    alert(this); // window
  </script>

  <script type="module">
    alert(this); // undefined
  </script>
  ```

### 브라우저 특정 기능

> 브라우저 환경에서 `type="module"`이 붙은 스크립트의 특징

- 지연 실행
  - 외부 모듈 스크립트 `<script type="module" src="...">`를 다운로드할 때 브라우저의 HTML 처리를 중단하지 않는다. 외부 모듈 스크립트와 기타 리소스를 병렬적으로 불러온다
  - 모듈 스크립트는 HTML 문서가 완전히 준비될 때까지 대기하다가, HTML 문서가 만들어진 후 실행된다
  - 스크립트의 순서가 유지된다
  - defer처럼 작동한다
  ```html
  <script type="module">
    alert(typeof button); // 모듈 스크립트는 지연 실행되기 때문에 페이지가 모두 로드되고 난 다음에 alert 함수가 실행
    // 얼럿창에 object가 정상적으로 출력되고, 모듈 스크립트는 아래쪽의 button 요소를 볼 수 있다
  </script>

  하단의 일반 스크립트와 비교해 봅시다.

  <script>
    alert(typeof button); // 일반 스크립트는 페이지가 완전히 구성되기 전이라도 바로 실행
    // 버튼 요소가 페이지에 만들어지기 전에 접근하였기 때문에 undefined가 출력
  </script>

  <button id="button">Button</button>
  ```

- 인라인 스크립트의 비동기 처리
  - 일반 스크립트에서 async 속성은 외부 스크립트를 불러올 때만 유효. async 속성이 붙은 스크립트는 로딩이 끝나면 다른 스크립트나 HTML을 기다리지 않고 즉시 실행
  - 모듈 스크립트에서 async 속성을 인라인 스크립트에 적용 가능
  - 광고나 문서 레벨 이벤트 리스너, 카운터 등 어디에도 종속되지 않는 기능 구현시 사용

  ```html
  <!-- 필요한 모듈(analytics.js)의 로드가 끝나면 문서나 다른 <script>가 로드되길 기다리지 않고 바로 실행-->
  <script async type="module">
    import {counter} from './analytics.js';

    counter.count();
  </script>
  ```

- async와 defer ([참고 이미지](https://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html))
  - async : HTML 파싱(DOM 렌더)과 스크립트 다운을 병렬적으로 진행하고, 스크립트가 모두 로딩되면 DOM 렌더를 멈추가 스크립트 파일 해석을 시작한다. async 스크립트는 실행 순서를 보장하지 않는다
  - defer : DOM 렌더와 스크립트 로딩을 병렬적으로 진행하지만, DOM이 모두 로드된 다음에야 실행한다. defer는 실행 순서를 보장한다
  - 출처: [스크립트의 실행 시점을 조절하는 Async와 Defer 속성](https://wormwlrm.github.io/2021/03/01/Async-Defer-Attributes-of-Script-Tag.html)

- 외부 스크립트
  - src 속성값이 동일한 외부 스크립트는 한 번만 실행
  - 다른 오리진에서 모듈 스크립트를 불러오려면 CORS 헤더 필요
  ```html
  <!-- another-site.com이 Access-Control-Allow-Origin을 지원해야만 외부 모듈을 불러올 수 있다. 그렇지 않으면 스크립트는 실행되지 않는다 -->
  <script type="module" src="http://another-site.com/their.js"></script>
  ```

- 경로가 없는 모듈은 금지
  ```js
  import {sayHi} from 'sayHi'; // Error! ('./sayHi.js'처럼 경로 지정 필요)
  ```

- 호환을 위한 nomodule
  - 구식 브라우저는 `type="module"`을 해석하지 못하기 때문에 모듈 타입의 스크립트를 만나면 무시하고 넘어가므로, nomodule 속성을 이용해 대비 가능
  ```html
  <script type="module">
    alert("모던 브라우저를 사용하고 계시군요.");
  </script>

  <script nomodule>
    alert("type=module을 해석할 수 있는 브라우저는 nomodule 타입의 스크립트는 넘어가므로 이 alert 문은 실행되지 않는다")
    alert("오래된 브라우저를 사용하고 있다면 type=module이 붙은 스크립트는 무시되고, 대신 이 alert 문이 실행된다");
  </script>
  ```

### 빌드 툴

- 브라우저 환경에서는 모듈을 단독으로 사용하기보다는 `웹택(Webpack)` 등 특별한 툴을 이용해 모듈을 한 데 묶어(번들링) 프로덕션 서버에 올린다
- 번들러를 사용하면 모듈 분해를 통제할 수 있고, 경로가 없는 모듈, CSS, HTML 포맷의 모듈을 사용할 수 있게 해준다
- 빌드 툴의 역할
  - 모듈 간의 의존 관계 파악
  - 모듈 전체를 모아 하나의 큰 파일 생성 (여러 개로 만들기도 가능)
  - 이 과정에서 변형이나 최적화도 함께 실행
    - 도달되지 않은 코드는 삭제
    - 내보내진 모듈 중 쓰임처가 없는 모듈은 삭제(`가지치기(tree-shaking)`)
    - `console`, `debugger` 등 개발 관련 코드 삭제
    - 최신 자바스크립트 문법이 사용될 경우 `바벨(Babel)`을 이용해 동일한 기능을 하는 낮은 버전의 스크립트로 변환
    - 공백 제거, 변수 이름 줄이기 등 산출물의 크기 감소
- 번들링 과정이 끝나면 기존 스크립트에서 `import`, `export`가 사라지므로 `type="module"`이 사라지므로, 일반 스크립트처럼 취급할 수 있다

<br />

<div id="2"></div>

## [모듈 내보내고 가져오기](https://ko.javascript.info/import-export)

### export

```js
// 배열, 상수, 클래스 등 모두 내보내기 가능
export class User {
  constructor(name) {
    this.name = name;
  }
}

function sayHi(user) {
  alert(`Hello, ${user}!`);
}
export {sayHi}; 
```

### import

```js
import {sayHi} from './say.js';
sayHi('John'); // Hello, John!
```
`import * as <obj>`처럼 객체 형태로도 가져올 수 있다
```js
import * as say from './say.js';
say.sayHi('John');
```
그러나 구체적으로 명시하는 것이 더 좋다
- 웹팩과 같은 모던 빌드 툴은 실제 사용되는 함수만 최종 번들링 결과물에 포함한다. 불필요한 코드가 줄어들수록 빌드 결과물의 크기도 줄어든다
- 어떤 것을 가져올지 명시하면 더 간결하다
- 어디서 어떤 것이 사용되는지 명확하기 때문에 리팩터링이나 유지보수에 좋다

### as

```js
import {sayHi as hi} from './say.js';
hi('John'); // Hello, John!
```
```js
// 📁 say.js
export {sayHi as hi};
```
```js
// 📁 main.js
import * as say from './say.js';
say.hi('John'); // Hello, John!
```

### export default

- 모듈의 두 종류
  1. 복수의 함수가 있는 라이브러리 형태의 모듈
  2. 개체 하나만 선언되어있는 모듈 → 해당 모듈엔 개체가 하나만 있다
- export default는 개체 이름이 없어도 가능

```js
// 📁 user.js
export default class User { 
  constructor(name) {
    this.name = name;
  }
}
```
```js
// 📁 main.js
import User from './user.js'; // {User}가 아닌 User
new User('John');
```

- named export와 default export

  | named export | default export |
  | --- | --- |
  | export class User {...} | export default class User {...} |
  | import {User} from ... | import User from ... |

- ‘default’ name
  - 함수 선언부와 떨어진 곳에서 default 키워드를 사용해 내보내기 가능
  ```js
  function sayHi(user) {
    alert(`Hello, ${user}!`);
  }
  export {sayHi as default};
  ```

- default export의 이름에 관한 규칙
  - named export는 내보내기 할 때 쓴 이름과 가져오기 할 때 쓸 이름이 동일해야 한다
    ```js
    import {User} from './user.js'; // MyUser 불가능
    ```
  - default export는 가져오기 할 때 마음대로 이름 짓기 가능
    ```js
    import MyUser from './user.js'; // 동작
    ```
  → 혼란스러울 수 있으므로 default export한 것을 가져올 때는 파일 이름과 동일하게 하기도 한다
    ```js
    import LoginForm from './loginForm.js';
    ```

### 모듈 다시 내보내기

- `export ... from ...`으로 가져온 개체를 즉시 `다시 내보내기(re-export)` 가능
- auth의 login, logout만 외부에 공개하려고 할 때, 해당 기능을 사용하는 외부 개발자가 auth 패키지를 뒤져 내부 구조를 건드리게 하면 안된다. 이를 막기 위해 공개할 것만 auth/index.js에 넣고 나머지는 숨긴다
```js
// 📁 auth/index.js

// login과 logout을 가지고 온 후 바로 내보낸다
import {login, logout} from './helpers.js';
export {login, logout};
// export {login, logout} from './helpers.js';

// User를 가져온 후 바로 내보낸다
import User from './user.js';
export {User};
// export {default as User} from './user.js';
```

- default export 다시 내보내기
  - `export * from './user.js'`를 사용해 모든 걸 한 번에 다시 내보내면 `default export`는 무시되고, `named export`만 다시 내보내진다
    ```js
    export * from './user.js'; // named export를 다시 내보내기
    export {default} from './user.js'; // default export를 다시 내보내기
    ```

- import/export문은 스크립트 맨 위나 아래 모두 위치 가능
  ```js
  sayHi();
  import {sayHi} from './say.js'; // 문제 없음
  ```

- import/export문은 블록 안에서는 동작하지 않는다
  ```js
  if (something) {
    import {sayHi} from "./say.js"; // 에러: import 문은 최상위 레벨에 위치
  }
  ```

<br />

<div id="3"></div>

## [동적으로 모듈 가져오기](https://ko.javascript.info/modules-dynamic-imports)

### import() 표현식

- import()는 함수 호출이 아니고, super()처럼 괄호를 사용하는 특별한 문법이다. 따라서 import를 변수에 복사하거나, call/apply 사용하는 것은 불가능하다

```js
// 📁 say.js
export function hi() {
  alert(`안녕하세요.`);
}

export default function() {
  alert("export default한 모듈을 불러왔습니다!");
}
```
```js
let {hi} = await import('./say.js');
hi();
```
```js
let say = await import('./say.js');
say.hi();
say.default();
```

<br />

<div id="4"></div>

## [커링](https://ko.javascript.info/currying-partials)

- `f(a, b, c)`처럼 단일 호출로 처리하는 함수를 `f(a)(b)(c)`처럼 다중 callable 프로세스 형태로 변환하는 기술 (함수 호출이 아니고 변환)
- 자바스크립트에서 커링되어진 함수는 호출되기도 하고, 인수가 충분하지 않을 때는 partial을 반환
- 고정된 개수의 인수를 가질 때에만 가능 (`f(...args)`처럼 나머지 매개변수를 사용하는 함수는 불가능)
- 인자 순서가 중요하므로 변동될 가능성이 낮은 인자를 앞에다 둔다

```js
function curry(f) { // 커링 변환을 하는 curry(f) 함수
  return function(a) { // curry(func)의 반환값은 function(a)형태의 래퍼
    return function(b) {
      return f(a, b);
    };
  };
}

// usage
function sum(a, b) {
  return a + b;
}

const curriedSum = curry(sum);

alert( curriedSum(1)(2) ); // 3
// curriedSum(1)이 호출되면, 인수는 렉시컬 환경에 저장되고 새로운 래퍼 function(b)가 반환
// 반환된 function(b) 래퍼 함수가 2를 인수로 호출된다
// 그리고 반환값이 원래 sum으로 넘겨져서 호출된다
```

```js
const curriedSum2 = (a) => (b) => a + b;
```

- `lodash`의 [_.curry](https://lodash.com/docs/4.17.15#curry)처럼 래퍼를 반환할 때 함수가 보통 또는 partial적으로 호출하는 것을 허용하는 커링도 있다

```js
function sum(a, b) {
  return a + b;
}

let carriedSum = _.curry(sum); // lodash 라이브러리의 _.curry 사용

alert( carriedSum(1, 2) ); // 3, 보통 때 처럼 호출가능
alert( carriedSum(1)(2) ); // 3, partially 호출되었음
```

### 커링을 사용하는 곳

- 커링은 partial을 쉽게 적용할 수 있도록 한다
- 커링을 적용하면 인수 3개의 범용 함수를 인수 1개 또는 2개인 형태로 호출할 수 있다

```js
function log(date, importance, message) {
  alert(`[${date.getHours()}:${date.getMinutes()}] [${importance}] ${message}`);
}

log = _.curry(log);

log(new Date(), "DEBUG", "some debug");
log(new Date())("DEBUG")("some debug");

// logNow 는 log 의 첫 번째 인수가 고정된 partial이 된다
let logNow = log(new Date());
logNow("INFO", "message");

let debugNow = logNow("DEBUG");
debugNow("message"); // [HH:mm] DEBUG 메세지
```

```js
const list = [
  {
    id: 1,
    name: 'Steve',
    email: 'steve@example.com',
  },
  {
    id: 2,
    name: 'John',
    email: 'john@example.com',
  },
  {
    id: 3,
    name: 'Pamela',
    email: 'pam@example.com',
  },
  {
    id: 4,
    name: 'Liz',
    email: 'liz@example.com',
  },
];

const get = (property) => (object) => object[property];
const getName = get('name');
const getNames = list => list.map(getName);

console.log(getNames(list)); // [ 'Steve', 'John', 'Pamela', 'Liz' ]

const filtering = name => item => item.name == name;
const filterByName = (list, name) => list.filter(filtering(name));

console.log(filterByName(list, 'John')); // [{ id: 2, name: 'John', email: 'john@example.com' }]
```

### 고급 커리 구현

> 다중-인수를 허용하는 커리        
> 추가 참조 자료: [JavaScript에서 커링 currying 함수 작성하기](https://edykim.com/ko/post/writing-a-curling-currying-function-in-javascript/)

```js
function curry(func) {
  return function curried(...args) {

    if (args.length >= func.length) { // func 호출에 전달
      return func.apply(this, args);

    } else { // partial (아직 func 호출되지 않음) → pass 래퍼
      return function(...args2) {
        return curried.apply(this, args.concat(args2));
      }
    }
  };
}
```

**`curriedSum(1)(2)(3)` 호출되는 과정**
  1. 첫 번째 `curried(1)` 을 호출할때 `1`을 렉시컬 환경에 기억하고 `curried(1)` 이 `pass` 래퍼를 반환한다.
  2. `pass`래퍼가 `(2)`와 함께 호출된다. 이전의 인수인 (`1`)을 가져서 `(2)`와 연결하고`curried (1, 2)`를 함께 호출한다. 인수의 개수는 아직 3보다 작기때문에 `curry`는 `pass`를 반환한다.
  3. `pass` 래퍼가 다시 `(3)`과 함께 호출된다. 다음 호출인 `pass(3)`가 이전의 인수들인 (`1`, `2`)를 가져오고 `3`을 추가하고 `curried(1, 2, 3)` 호출한다 → `3`인수는 마지막이므로 원래의 함수에 전달된다

- 출처: [커링](https://ko.javascript.info/currying-partials), [[번역] 초보자를 위한 함수형 자바스크립트 Currying 가이드](https://sujinlee.me/currying-in-functional-javascript/), [JavaScript currying](https://zetcode.com/javascript/currying/), [A practical example of how to use Currying in Javascript](https://dev.to/darkmavis1980/a-practical-example-on-how-to-use-currying-in-javascript-1ae9), [[JavaScript] - 커링에 대해 알아보자](https://velog.io/@hustle-dev/Javascript-%EC%BB%A4%EB%A7%81%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)

<br />
<br />
