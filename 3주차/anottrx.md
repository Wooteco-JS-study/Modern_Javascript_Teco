# Fetch API와 Axios

## 목차

1. [3.1 fetch](#1)
2. [3.6 Fetch API](#2)
3. [Axios](#3)
4. [Fetch API와 Axios](#4)

<br />

<div id="1"></div>

## [3.1 fetch](https://ko.javascript.info/fetch)

- **`fetch()` 메서드 : 서버에 네트워크 요청을 보내고 새로운 정보를 받아온다** (대부분의 모던 브라우저에서 지원)

```js
let promise = fetch(url, [options]);
```

- **url : 접근하고자 하는 URL**
- **options : 선택 매개변수 (method나 headers 등 지정 가능)**
  - options가 없다면 GET 메서드로 요청 진행
- `fetch()`를 호출하면 브라우저는 네트워크를 보내고, 프라미스가 반환된다
- 응답

  **1. 서버에서 응답 헤더를 받자마자, fetch 호출 시 반환받은 promise가 내장 클래스 Response의 인스턴스와 함께 이행(resolve) 상태가 된다**

  - 본문(body)이 도착하기 전에 응답 헤더만 보고 요청의 성공 여부를 알 수 있다
  - 네트워크 문제나 존재하지 않는 사이트 등 HTTP 요청을 보낼 수 없을 경우 프라미스는 거부 상태가 된다
  - HTTP 응답 상태

    - status : HTTP 상태 코드
    - ok : 불린 값. HTTP 상태 코드가 200과 299 사이라면 true

    ```js
    let response = await fetch(url);

    if (response.ok) {
      // HTTP 상태 코드가 200~299일 경우 응답 본문을 받는다
      let json = await response.json();
    } else {
      alert("HTTP-Error: " + response.status);
    }
    ```

  **2. 추가 메서드를 호출해 응답 본문을 받는다**

  - `response.text()` – 응답을 읽고 텍스트를 반환
  - `response.json()` – 응답을 JSON 형태로 파싱
  - `response.formData()` – 응답을 FormData 객체 형태로 반환
  - `response.blob()` – 응답을 Blob(타입이 있는 바이너리 데이터) 형태로 반환

  ```js
  let url =
    "https://api.github.com/repos/javascript-tutorial/ko.javascript.info/commits";
  let response = await fetch(url);
  let commits = await response.json(); // 응답 본문을 읽고 JSON 형태로 파싱함
  alert(commits[0].author.login);
  ```

  ```js
  // await 없이 프라미스만 사용
  fetch(
    "https://api.github.com/repos/javascript-tutorial/en.javascript.info/commits"
  )
    .then((response) => response.json())
    .then((commits) => alert(commits[0].author.login));
  ```

  ```js
  let response = await fetch(
    "https://api.github.com/repos/javascript-tutorial/en.javascript.info/commits"
  );
  let text = await response.text(); // 응답 본문을 텍스트 형태로 읽는다
  alert(text.slice(0, 80) + "...");
  ```

  ```js
  let response = await fetch("/article/fetch/logo-fetch.svg");
  let blob = await response.blob(); // 응답을 Blob 객체 형태로 다운로드

  let img = document.createElement("img"); // 다운로드받은 Blob을 담을 <img>를 만든다
  img.style = "position:fixed;top:10px;left:10px;width:100px";
  document.body.append(img);

  img.src = URL.createObjectURL(blob); // 이미지를 화면에 보여준다

  setTimeout(() => {
    // 3초 후 이미지를 숨긴다
    img.remove();
    URL.revokeObjectURL(img.src);
  }, 3000);
  ```

  ```js
  // 메서드는 하나만 사용할 수 있다
  let text = await response.text(); // 응답 본문
  let parsed = await response.json(); // 실패
  ```

### 응답 헤더

- `response.headers`에 맵과 유사한 형태로 저장

```js
let response = await fetch(
  "https://api.github.com/repos/javascript-tutorial/en.javascript.info/commits"
);

// 헤더 일부 추출
alert(response.headers.get("Content-Type")); // application/json; charset=utf-8

// 헤더 전체 순회
for (let [key, value] of response.headers) {
  alert(`${key} = ${value}`);
}
```

### 요청 헤더

```js
let response = fetch(protectedUrl, {
  headers: {
    Authentication: "secret",
  },
});
```

### POST 요청

- GET 이외에 다른 요청을 보내려면 추가 옵션이 필요
  - **method : HTTP 메서드 (POST 등)**
  - **body : 요청 본문**
    - 문자열, FormData 객체, Blob이나 BufferSource 등
- POST 요청할 때 요청 본문이 문자라면 기본으로 `Content-Type 헤더`가 `text/plain;charset=UTF-8`
  - JSON을 전송하기 위해서는 `Content-Type 헤더`에 `application/json` 설정

```js
let user = {
  name: "John",
  surname: "Smith",
};

let response = await fetch("/article/fetch/post/user", {
  method: "POST",
  headers: {
    "Content-Type": "application/json;charset=utf-8",
  },
  body: JSON.stringify(user),
});

let result = await response.json();
alert(result.message);
```

### 이미지 전송하기

- Blob, BufferSource 객체를 활용하여 fetch로 바이너리 데이터 전송 가능

```js
function submit() {
  canvasElem.toBlob(function (blob) {
    fetch("/article/fetch/post/image", {
      method: "POST",
      body: blob,
    })
      .then((response) => response.json())
      .then((result) => alert(JSON.stringify(result, null, 2)));
  }, "image/png");
}
```

<br />

<div id="2"></div>

## [3.6 Fetch API](https://ko.javascript.info/fetch-api)

```js
let promise = fetch(url, {
  method: "GET", // POST, PUT, DELETE, etc.
  headers: {
    // request body에 따라 보통 자동으로 설정된다
    "Content-Type": "text/plain;charset=UTF-8"
  },
  body: undefined // string, FormData, Blob, BufferSource, URLSearchParams
  referrer: "about:client", // Referer header가 없다면 "". 또는 "https://javascript.info/anotherpage"처럼 현재 출처
  referrerPolicy: "no-referrer-when-downgrade", // no-referrer, origin, same-origin 등
  // Requset의 3가지 타입 : 동일 출처, 다른 출처, HTTPS에서 HTTP 요청
  mode: "cors", // cors가 디폴트. same-origin, no-cors
  credentials: "same-origin", // same-origin이 디폴트. omit, include
  cache: "default", // no-store, reload, no-cache, force-cache, only-if-cached
  redirect: "follow", // follow가 디폴트. manual, error
  integrity: "", // a hash, like "sha256-abcdef1234567890"
  keepalive: false, // true
  signal: undefined, // AbortController to abort request
  window: window // null
});
```

<br />

<div id="3"></div>

## Axios

- 설치 후 import 필요

```bash
yarn add axios
```

```js
import axios from "axios";
```

- 예시

```js
axios(url); // GET

axios.get(url, {});

axios({
  method: "get",
  url: url,
  headers: {
    "Content-Type": "application/json;charset=UTF-8",
  },
  data: {},
});
```

<br />

<div id="3"></div>

## Fetch API와 Axios

### 데이터 처리

- Fetch는 메서드에서 처리된 promise를 반환하므로, JSON 포맷을 위해 .json() 메서드를 한 번 더 호출해야 한다
  ```js
  fetch(url)
    .then((response) => response.json())
    .then(console.log); // 두번의 then() 호출
  ```
- Axios의 응답 데이터는 기본적으로 JSON 타입이다
  ```js
  axios.get(url).then((response) => console.log(response.data));
  ```

### 자동 문자열 변환 (데이터 전송을 위해 JSON 문자열로 직렬화)

- Axios는 자동으로 데이터를 무자열로 변환해준다

  - Axios의 `Content-Type` 기본형은 `application/json`

  ```js
  const todo = {
    title: "A new todo",
    completed: false,
  };

  axios
    .post(url, {
      headers: {
        "Content-Type": "application/json",
      },
      data: todo,
    })
    .then(console.log);
  ```

- Fetch API는 JSON.stringify()로 객체를 문자열로 변환한 뒤 body에 할당해야 하며, `Content-Type`을 `application/json`로 설정해야 한다

```js
const todo = {
  title: "A new todo",
  completed: false,
};

fetch(url, {
  method: "post",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(todo),
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```

### 에러 처리

- Axios의 promise는 상태코드가 200번대를 벗어나면 거부한다

```js
axios
  .get(url)
  .then((response) => console.log(response.data))
  .catch((err) => {
    if (err.response) {
      // 요청이 이루어졌고 서버가 응답했을 경우
      const { status, config } = err.response;

      if (status === 404) {
        console.log(`${config.url} not found`);
      }
      if (status === 500) {
        console.log("Server error");
      }
    } else if (err.request) {
      // 요청이 이루어졌으나 서버에서 응답이 없었을 경우
      console.log("Error", err.message);
    } else {
      // 그 외 다른 에러
      console.log("Error", err.message);
    }
  });
```

- Fetch는 네트워크 장애가 발생한 경우만 promise를 거부하므로, 수동으로 HTTP 에러 처리를 해주어야 한다

```js
fetch(url)
  .then((response) => {
    if (!response.ok) {
      throw new Error(
        `This is an HTTP error: The status is ${response.status}`
      );
    }
    return response.json();
  })
  .then(console.log)
  .catch((err) => {
    console.log(err.message);
  });
```

### 응답 시간

- Axios는 timeout으로 요청 시간을 설정할 수 있다

```js
axios
  .get(url, {
    timeout: 4000, // 기본 설정은 '0' (타임아웃 없음)
  })
  .then((response) => console.log(response.data))
  .catch((err) => {
    console.log(err.message);
  });
```

- Fetch는 AbortController 인터페이스를 사용한다

```js
const controller = new AbortController();
const signal = controller.signal;
// controller로 생성한 signal 객체를 fetch()에 넘김으로써 응답 시간을 설정할 수 있다
setTimeout(() => controller.abort(), 4000);

fetch(url, {
  signal: signal,
})
  .then((response) => response.json())
  .then(console.log)
  .catch((err) => {
    console.error(err.message);
  });
```

- 출처 : [[번역] 입문자를 위한 Axios vs Fetch](https://velog.io/@eunbinn/Axios-vs-Fetch)

<br />
<br />
