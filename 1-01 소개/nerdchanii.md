# Javascript란 ?

- [Javascript란 ?](#javascript란-)
  - [정의](#정의)
  - [javascript의 명세](#javascript의-명세)
  - [javascript Engine](#javascript-engine)
    - [engine종류](#engine종류)
  - [브라우저에서 할 수 있는 일](#브라우저에서-할-수-있는-일)
  - [브라우저에서 할 수 없는 일](#브라우저에서-할-수-없는-일)
  - [javascript의 강점](#javascript의-강점)
  - [javascript의 슈퍼셋언어들](#javascript의-슈퍼셋언어들)
    - [javascript로 컴파일이 가능한 언어들](#javascript로-컴파일이-가능한-언어들)
  - [etc](#etc)
  - [summary](#summary)

## 정의

- 웹페이지에 생동감을 불어넣기 위해 만들어진 프로그래밍 언어
- js로 작성된 코드 -> 스크립트라고 부름
- 컴파일 없이 실행할 수 있는 인터프리터 언어

## javascript의 명세

- **Ecmascript** 라는 고유한 명세를 갖게 됨
- [ECMA-262 명세](https://www.ecma-international.org/about-ecma/areas-of-work/): 자바스크립트에대한 가장 심도있고 상세한 공식문서
- 가장 최근 명세: [https://tc39.es/ecma262/](https://tc39.es/ecma262/)
- 등록되기 직전(스테이지 3)에 있는 기능들 [proposal](https://github.com/tc39/proposals)

## javascript Engine

- javascript의 실행환경
- javascript는 javascript Engine이 있는 어느곳에서나 동작가능

### engine종류  

- V8(chrome, opera, node)
- SpiderMonkey(Firefox)  
- CharkraCore(Edge)
- SquirrelFish(Safari)

> 엔진의 동작과정
> 파싱 -> 컴파일 -> 실행

## 브라우저에서 할 수 있는 일

- 모던 자바스크립트는 '안전한' 프로그래밍 언어
- 메모리나 CPU등 저수준 영역의 조작을 허용하지 않음
- javascript의 능력은 실행환경에 상당한 영향을 받는다.
  - nodejs환경에서는 파일을 읽고/쓰고, 네트워크 요청을 할 수 있는 함수를 지원
  - 브라우저환경에선 웹페이지 조작, 클라이언트와 서버의 상호작용에 관한 모든 일을 지원
  - 브라우저에서 javascript로 할 수 있는 일
    - HTML에 HTML 수정, style 수정
    - 마우스 / 키보드 등 사용자의 행동에 반응
    - 네트워크 요청(다운로드 / 업로드)
    - 클라이언트 측에 데이터 저장(로컬스토리지)

## 브라우저에서 할 수 없는 일

- 디스크에 저장된 임의의 파일을 읽거나 쓰고, 복사하거나 실행하는 것
- 파일을 다룰 순 있지만, 접근은 제한되어있다.(input태그 사용)
- 카메라 / 마이크와 같은 디바이스와 상호작용하려면 사용자의 명시적인 허가를 필요
- 브라우저 내 탭과 창은 서로의 정볼르 알 수 없다. 예외) javascript로 다른 창을 열 때(도메인, 프로토콜, 포트 등 CORS의 제약을 받음)

## javascript의 강점

- HTML/CSS와 완전한 통합 가능
- 간단한 일을 간단하게 처리할 수 있음
- 모든 브라우저에서 지원 / 기본 언어로 사용

## javascript의 슈퍼셋언어들

- 특정한 요구사항들 때문에, javascript에 기능이 추가된 언어를 형성시켜서 추가된 기능의 이점을 얻고, 트랜스파일을 통해 javascript로 변환시켜 javascript Engine이 실행할 수 있도록 하는 언어

### javascript로 컴파일이 가능한 언어들

- CoffeScript - javascript를 위한 syntactic sugar, 짧은 문법, 명료하고 이해하기 쉬운 코드 작성을 도와줌. Ruby개발자들의 사랑을 받음
- Typescript - 개발을 단순화하고 복잡한 시스템을 지원하기 위해 자료형의 명시화에 집중해서 만든 언어. MS에서 만듦. 최근 웹개발에서 엄청난 사랑을 받는 중
- Flow - 자료형을 강제하지만, TypeScript와는 다른 방식을 사용. Meta에서 개발
- Dart - 모바일 앱과 같이 브라우저가 아닌 환경에서 동작하는 고유의 엔진을 가진 독자적 언어 Google이 개발하였음

## etc

추후 개발시 알아두면 좋을 자료들과 사이트

- [can-i-use](https://caniuse.com/)
- [mdn](https://developer.mozilla.org/ko/)
- [ecma명세](https://www.ecma-international.org/)
- [ecma-github](https://github.com/tc39/ecma262)
- [ecma-stage-3](https://github.com/tc39/proposals)

## summary

- javascript의 출발은 브라우저에서 약간의 인터렉션을 위해 고안된 언어
  - 하지만, 현재는 다양한 환경에서 쓰임
- javascript === 엄청난 사랑을 받는 중
- 다양한 언어를 javascript로 트랜스파일 가능
