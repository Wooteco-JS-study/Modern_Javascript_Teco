
# 6 - 1강 data storage
## 1 - 1 cookie
쿠키는 브라우저에 저장되는 작은 크기의 문자열로, RFC 6265 명세에서 정의한 HTTP 프로토콜의 일부입니다.<br>
쿠키는 주로 웹 서버에 의해 만들어집니다. 서버가 HTTP 응답 헤더(header)의 Set-Cookie에 내용을 넣어 전달하면, 브라우저는 이 내용을 자체적으로 브라우저에 저장합니다. 이게 바로 쿠키입니다. 브라우저는 사용자가 쿠키를 생성하도록 한 동일 서버(사이트)에 접속할 때마다 쿠키의 내용을 `Cookie` 요청 헤더에 넣어서 함께 전달합니다.<br>
쿠키는 클라이언트 식별과 같은 인증에 가장 많이 쓰입니다.

* 사용자가 로그인하면 서버는 HTTP 응답 헤더의 Set-Cookie에 담긴 "세션 식별자(session identifier)" 정보를 사용해 쿠키를 설정합니다.
* 사용자가 동일 도메인에 접속하려고 하면 브라우저는 HTTP Cookie 헤더에 인증 정보가 담긴 고윳값(세션 식별자)을 함께 실어 서버에 요청을 보냅니다.
* 서버는 브라우저가 보낸 요청 헤더의 세션 식별자를 읽어 사용자를 식별합니다.

### 쿠키읽기
document.cookie는 name=value 쌍으로 구성되어있고, 각 쌍은 ;로 구분합니다. 이때, 쌍 하나는 하나의 독립된 쿠키를 나타냅니다.

### path
URL path(경로)의 접두사로, 이 경로나 이 경로의 하위 경로에 있는 페이지만 쿠키에 접근할 수 있습니다. 절대 경로이어야 하고, (미 지정시) 기본값은 현재 경로입니다.<br>
특별한 경우가 아니라면, `path` 옵션을 `path=/`같이 루트로 설정해 웹사이트의 모든 페이지에서 쿠키에 접근할 수 있도록 합시다.

### domain
쿠키에 접근 가능한 domain(도메인)을 지정합니다. 다만, 몇 가지 제약이 있어서 아무 도메인이나 지정할 수 없습니다.<br>
domain 옵션에 아무 값도 넣지 않았다면, 쿠키를 설정한 도메인에서만 쿠키에 접근할 수 있습니다. `site.com`에서 설정한 쿠키는 other.com에서 얻을 수 없죠.<br>

이 외에 까다로운 제약사항이 하나 더 있습니다. 서브 도메인(subdomain)인 `forum.site.com`에서도 쿠키 정보를 얻을 수 없다는 점입니다

### expires와 max-age
expires(유효 일자)나 max-age(만료 기간) 옵션이 지정되어있지 않으면, 브라우저가 닫힐 때 쿠키도 함께 삭제됩니다. 이런 쿠키를 "세션 쿠키(session cookie)"라고 부릅니다.<br>
`expires` 나 `max-age` 옵션을 설정하면 브라우저를 닫아도 쿠키가 삭제되지 않습니다.
```js run
// 1시간 뒤에 쿠키가 삭제됩니다.
document.cookie = "user=John; max-age=3600";

// 만료 기간을 0으로 지정하여 쿠키를 바로 삭제함
document.cookie = "user=John; max-age=0";
```

### secure
이 옵션을 설정하면 HTTPS로 통신하는 경우에만 쿠키가 전송됩니다.

### setCookie(name, value, options)
현재 경로(path=/)를 기본으로, 주어진 name과 value를 가진 쿠키를 설정합니다(다른 기본값을 추가할 수 있습니다).

### deleteCookie(name)
만료 기간을 음수로 설정하면 쿠키를 삭제할 수 있습니다.

```js run
function deleteCookie(name) {
  setCookie(name, "", {
    'max-age': -1
  })
}
```

## 1 - 2 Local storage
웹 스토리지 객체(web storage object)인 localStorage와 sessionStorage는 브라우저 내에 키-값 쌍을 저장할 수 있게 해줍니다.<br>

그런데 "쿠키를 사용하면 브라우저에 데이터를 저장할 수 있는데, 왜 또 다른 객체를 사용해 데이터를 저장하는 걸까요?"라는 의문이 들 수 있습니다. 쿠키 이외에도 다른 방식을 사용하는 이유는 다음과 같습니다.<br>

* 쿠키와 다르게 웹 스토리지 객체는 네트워크 요청 시 서버로 전송되지 않습니다. 이런 특징 때문에 쿠키보다 더 많은 자료를 보관할 수 있습니다. 대부분의 브라우저가 최소 2MB 혹은 그 이상의 웹 스토리지 객체를 저장할 수 있도록 해줍니다. 또한 개발자는 브라우저 내 웹 스토리지 구성 방식을 설정할 수 있습니다.
* 쿠키와 또 다른 점은 서버가 HTTP 헤더를 통해 스토리지 객체를 조작할 수 없다는 것입니다. 웹 스토리지 객체 조작은 모두 자바스크립트 내에서 수행됩니다.
* 웹 스토리지 객체는 도메인·프로토콜·포트로 정의되는 오리진(origin)에 묶여있습니다. 따라서 프로토콜과 서브 도메인이 다르면 데이터에 접근할 수 없습니다.

두 스토리지 객체는 동일한 메서드와 프로퍼티를 제공합니다.

* setItem(key, value) -- 키-값 쌍을 보관합니다.
* getItem(key) -- 키에 해당하는 값을 받아옵니다.
* removeItem(key) -- 키와 해당 값을 삭제합니다.
* clear() -- 모든 것을 삭제합니다.
* key(index) -- 인덱스(index)에 해당하는 키를 받아옵니다.
* length -- 저장된 항목의 개수를 얻습니다.

### localStorage
localStorage의 주요 기능은 다음과 같습니다.

* 오리진이 같은 경우 데이터는 모든 탭과 창에서 공유됩니다.
* 브라우저나 OS가 재시작하더라도 데이터가 파기되지 않습니다.

### 일반 객체처럼 사용하기
```js run
// 키 설정하기
localStorage.test = 2;

// 키 얻기
alert( localStorage.test ); // 2

// 키 삭제하기
delete localStorage.test;
```

### 키 순회하기
대신 배열처럼 다루면 전체 키-값을 얻을 수 있습니다.

```js run
for(let i=0; i<localStorage.length; i++) {
  let key = localStorage.key(i);
  alert(`${key}: ${localStorage.getItem(key)}`);
}
```

### 문자열만 사용가능
localStorage의 키와 값은 반드시 문자열이어야 합니다.<br>

숫자나 객체 등 다른 자료형을 사용하게 되면 문자열로 자동 변환됩니다.

```js run
localStorage.user = {name: "John"};
alert(localStorage.user); // [object Object]
```
JSON을 사용하면 객체를 쓸 수 있긴 합니다.

```js run
localStorage.user = JSON.stringify({name: "John"});

// 잠시 후 
let user = JSON.parse( localStorage.user );
alert( user.name ); // John
```

### sessionStorage
* sessionStorage는 현재 떠 있는 탭 내에서만 유지됩니다.
* 같은 페이지라도 다른 탭에 있으면 다른 곳에 저장되기 때문입니다.
* 그런데 하나의 탭에 여러 개의 iframe이 있는 경우엔 동일한 오리진에서 왔다고 취급되기 때문에 sessionStorage가 공유됩니다.
* 페이지를 새로 고침할 때 sessionStorage에 저장된 데이터는 사라지지 않습니다. 하지만 탭을 닫고 새로 열 때는 사라집니다.
