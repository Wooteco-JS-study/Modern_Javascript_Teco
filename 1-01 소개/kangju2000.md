# 1.01 getting-started
## 1. 소개
> 자바스크립트 = '웹페이지에 생동감을 불어넣기 위해' 만들어진 프로그래밍 언어
> 스크립트 = 자바스크립트로 작성한 프로그램

자바스크립트는 브라우저뿐만 아니라 서버에서도 실행할 수 있다.
이 외에도 **자바스크립트 엔진**이라 불리는 특별한 프로그램이 들어있는 모든 디바이스에서도 동작한다.

브라우저에는 '**자바스크립트 가상 머신**'이라 불리는 엔진이 내장되어 있다.
- V8 - Chrome, Opera
- SpiderMonkey - Firefox
- Trident / Chakra - IE
- ChakraCore - Microsoft Edge
- SquirrelFish - Safari
> 엔진 동작 기본 원리
>> 1. 엔진(브라우저라면 내장 엔진)이 스크립트를 읽음(파싱).
>> 2. 읽어 들인 스크립트를 기계어로 전환(컴파일).
>> 3. 기계어로 전환된 코드가 실행됨. 기계어로 전환되었기 때문에 실행 속도가 빠름.
>
> 엔진은 각 단계마다 최적화 진행

### 브라우저에서 할 수 있는 일
-   페이지에 새로운 HTML을 추가하거나 기존 HTML, 혹은 스타일 수정하기
-   마우스 클릭이나 포인터의 움직임, 키보드 키 눌림 등과 같은 사용자 행동에 반응하기
-   네트워크를 통해 원격 서버에 요청을 보내거나, 파일 다운로드, 업로드하기([AJAX](https://en.wikipedia.org/wiki/Ajax_(programming))나  [COMET](https://en.wikipedia.org/wiki/Comet_(programming))과 같은 기술 사용)
-   쿠키를 가져오거나 설정하기. 사용자에게 질문을 건네거나 메시지 보여주기
-   클라이언트 측에 데이터 저장하기(로컬 스토리지)

### 브라우저에서 할 수 없는 일
브라우저는 **보안을 위해** 자바스크립트 기능에 **제약**을 걸어놓았다. 악성 웹페이지가 개인 정보에 접근하거나 사용자의 데이터를 손상시키는 것을 막기 위해 만들어졌다.
- 웹페이지 내 스크립트는 디스크에 저장된 임의의 파일을 읽거나 쓰고, 복사하거나 실행할 때
	- 사용자가 브라우저 창에 파일을 '끌어다 두거나' `<input>` 태그를 통해 파일을 선택할 때와 같이 특정 상황에서만 파일 접근을 허용
	- 카메라나 마이크 같은 디바이스와 상호 작용하려면 사용자의 명시적인 허가가 있어야 함
- 브라우저 내 탭과 창은 대개 서로의 정보를 알 수 없음
	- 자바스크립트를 사용해 한 창에서 다른 창을 열 때는 예외가 적용됨
	- 하지만 이 경우에도 도메인이나 프로토콜, 포트가 다르다면 페이지에 접근할 수 없음
	- = 동일 출처 정책(Same Origin Policy)

### 자바스크립트만의 강점
- HTML/CSS와 완전히 통합할 수 있음
- 간단한 일은 간단하게 처리할 수 있게 해줌
- 모든 주요 브라우저에서 지원하고, 기본 언어로 사용됨

## 2. 매뉴얼과 명세서
[ECMA-262 명세서(specification)](https://www.ecma-international.org/publications/standards/Ecma-262.htm)는 자바스크립트와 관련된 가장 심도 있고 상세한 정보를 담고 있는 공식 문서이다.

### 매뉴얼
- [MDN JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)
- Google 검색 엔진에 접속해 'MDN [원하는 용어]'를 입력

### 호환성 표
- [http://caniuse.com](http://caniuse.com/)
	- 브라우저가 특정 기능을 지원하는지 (표 형태로) 확인 가능
- [https://kangax.github.io/compat-table](https://kangax.github.io/compat-table)
	- 자바스크립트 기능 목록, 특정 엔진이 지원하는지 여부를 표를 통해 보여줌

## 3. 코드 에디터
### 통합 개발 환경(Integrated Development Environment, IDE)
'개발 환경'을 쾌적하게 해주는 통합 환경을 제공한다.
- 추천 에디터
	-   [Visual Studio Code](https://code.visualstudio.com/)  (크로스 플랫폼, 무료)
	-   [WebStorm](http://www.jetbrains.com/webstorm/)  (크로스 플랫폼, 유료)

### 경량 에디터
- 속도가 빠르고 단순함
- 파일을 열고 바로 수정하고자 할 때 주로 사용
- '경량 에디터'와 'IDE'의 차이점
	- IDE는 프로젝트 레벨에서 작동함
	- 경량 에디터는 다양한 플러그인을 지원함
- 추천 에디터
	-   [Atom](https://atom.io/)  (크로스 플랫폼, 무료)
	-   [Visual Studio Code](https://code.visualstudio.com/)  (크로스 플랫폼, 무료)
	-   [Sublime Text](http://www.sublimetext.com/)  (크로스 플랫폼, 셰어웨어)
	-   [Notepad++](https://notepad-plus-plus.org/)  (Windows, 무료)
	-   [Vim](http://www.vim.org/) or  [Emacs](https://www.gnu.org/software/emacs/)

## 4. 개발자 콘솔
브라우저엔 '개발자 도구'라는 것이 내장되어 있다.
### Chrome
- Windows: `key:F12` / Mac : `key:Cmd+Opt+J`
### Safari
- '개발자 메뉴(Develop menu)'를 명시적으로 활성화해주어야 함
- `key:Cmd+Opt+C`
