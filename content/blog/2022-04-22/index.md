---
title: "[Elice SW 2기] mini-log #015 : JavaScript 심화 - 변수와 Hoisting"
date : "2022-04-22T23:46:37.121Z"
description: Elice, SW, WEB, Frontend, Bootcamp, 이고잉, HTML, CSS, JavaScript, OOP, Event, ES6, var, let, const, hoisting, Lexical Environment, 내장 객체
---
## JavaScript 실행의 이해

### 01. JavaScript 변수 정의 과정

#### JavaScript Engine

JavaScript Engine은 JavaScript 코드를 읽어 실행하는 프로그램으로, 작성된 JavaScript 코드가 JavaScript Engine을 통해 [파싱](https://oneroomtable.tistory.com/entry/%ED%8C%8C%EC%8B%B1%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C-%EB%B2%88%EC%97%AD)([parsing](https://developer.mozilla.org/en-US/docs/Glossary/Parse))되고 실행된다. 즉, 작성된 코드는 JavaScript Engine에 의해 AST 형식으로 파싱되고, Compiler가 읽어 머신 코드로 변경해준 후 컴퓨터 CPU에 의해 실행된다.

#### Node.js

Node.js는 브라우저 외부 환경에서 JavaScript 코드를 실행하도록 하는 프로그램이다.

#### JavaScript 코드의 실행 순서

1. JavaScript Engine은 코드의 실행 이전 Execution Context를 생성한다.
2. 생성 단계에서 JavaScript Engine은 변수 선언을 읽는다.(`a`, `b` 등이 Variable Object에 등록된다.)
   - JavaScript Engine은 생성 단계에서 함수 선언문, 함수 표현식, 변수 등을 읽어 Execution Context에 저장한다.
   - 변수의 경우, Execution Context의 Lexical Environment를 구성한다.
   - 함수 선언문 외에 변수는 값이 저장되지 않는다. 즉, 함수는 객체 전체가 저장되나, 변수는 값이 저장되지 않고, 할당 공간만 생성된다.
   - 이러한 경우, `var` 변수는 undefined, `let`, `const`는 `uninitialized` 값으로 초기화된다.

3. 실행 단계에서 JavaScript Engine은 변수의 값을 할당한다.(`10`, `20` 등 값이 Variable Object에 이미 등록된 `a`, `b` 등에 할당된다.)
   - JavaScript Engine은 변수에 값을 할당하는 구문을 만나면 Execution Context에 값을 저장한다.
   - 그 외 코드를 한 줄씩 읽어 나가며 실행한다.

#### Lexical Environment

함수가 사용되는 변수들을 둘러싼 환경을 의미한다. 따라서 특정 변수의 값은 함수의 Lexical Environment 안에서 찾을 수 있다. 즉, Execution Context 내부에 정의된 Variable Object로 이해할 수 있다. 이때, Lexical Environment는 Scope Chain을 포함해, 외부에서 선언된 변수의 값을 참조할 수 있다.

### 02. Hoisting

JavaScript Engine이 코드를 읽으면, 생성 단계에서 Execution Context를 생성하고, 함수 선언문은 실행 단계에서 전체가 저장된다. 이와 달리 `var` 변수는 저장 시 `undefined`로, `let`, `const` 변수는 초기화되지 않는다. 초기화되지 않은 변수에 접근하면 에러가 발생한다.

Hoisting은 변수가 선언된 시점보다 앞서서 사용될 때 발생한다. `var` 변수가 생성 단계에서 undefined로 초기화되기 때문에 발생한다. 함수는 생성 단계에서 함수 전체에 저장되기 때문에 뒤에서 선언되더라도 호출이 가능하다.

```javascript
console.log(callMe());

var x = 10;

console.log(callMe());

function callMe() {
  return x;
}
```

이와 달리 let, const 변수는 생성 단계에서 초기화되지 않는다. 따라서 선언 이전에 접근하면 Reference Error가 발생한다. 즉, `let`, `const`는 Hoisting이 발생하지 않는다.(이 경계 구간, 즉 사용될 때부터 선언되기 전까지의 구간을 TDZ, Temporal Dead Zone이라 한다.)

```javascript
console.log(callMe());

let x = 10;

console.log(callMe());

function callMe() {
  return x;
}
```

#### var와 let의 Scope

```javascript
function varFor () {
  for (var i = 0; i < 3; ++i) { setTimeout(() => console.log("i: ", i), 0); }
}

function letFor () {
  for (let i = 0; i < 3; ++i) { setTimeout(() => console.log("i: ", i), 0); }
}

varFor(); // 3 3 3
letFor(); // 0 1 2
```

`var` 변수로 선언된 `i`는 `setTimeout()` 함수가 반복문을 돌며 3번 실행되고, `for`문이 종료된 시점에도 소멸하지 않는 반면, `let`으로 선언된 `i`의 경우에는 하나의 반복문 Block마다 소멸하고 그때의 화살표 함수 closure에 저장된다.

즉, `var` 변수는 function varFor에 존재하는 변수이고, `let` 변수는 for Loop에 존재하는 변수이기 때문에 차이를 보이는 것이다.

### 03. JavaScript 내장 객체

#### globalThis

globalThis는 전역 객체를 지칭하는 변수로, 환경에 따라 다른 전역 객체(브라우저에서는 `window`, Node에서는 `global`)를 통일하여 하나의 변수로 환경에 맞는 전역 객체를 가리킬 수 있게 한다.

#### window

DOM Document를 포함하는 창을 나타내는 개체로, 전역 Scope에서 선언된 변수는 모두 window 객체의 property가 된다. 현재 창의 정보를 얻거나, 창을 조작할 수 있다.

```javascript
const targetURL = "https://www.naver.com";

const windowSize = `height=${window.innerHeight}, width=${window.innerWidth}`;      // 현재 창과 동일한 크기 설정
// const windowSize = `height=${globalThis.innerHeight}, width=${globalThis.innerWidth}`;      // 여기서 globalThis = window를 의미함

globalThis.open(    // 새로운 창을 여는 함수
  targetURL,
  "Target",
  windowSize
);
```

#### Document

브라우저에 로드된 웹 페이지 즉, HTML 문서 자체를 표현하는 객체로, 문서의 title, URL 등의 정보를 얻거나, element의 생성, 검색 등의 기능을 제공한다. Document 객체를 통해 JavaScript만으로 요소를 구성할 수 있다.

```javascript
function printDocumentInfo() {
  console.Log("문서 URL: ", document.URL);
  console.Log("문서 title: ", document.title);
  console. Log("모든 Node:", document.querySelectorAll("*"));
}

function createTodolist(todos) {
  return todos
    .map((todo) => {
      const li = document.createElement("Li")
      li.appendChild(document.createTextNode(todo))
      return li
    })
    .reduce((ul, li) => {
      ul.appendChild(li)
      return ul
    }, document.createElement("ul"))
}
```

#### Number

Number 객체는 JavaScript의 원시 타입 number를 감싸는 객체로, 유의미한 상수값, 숫자를 변환하는 Method 등을 제공한다. NaN은 Not a Number를 나타내는 객체로, `isNaN()`(전역 함수)로 입력 값이 숫자로 변환될 때 `NaN`인지를 검사할 수 있다.

```javascript
function changeToUsd(krw) {
  const rate = 1046;
  return (krw / rate).toFixed(2);
}

const krw = 1000000;
console.Log(changeToUsd(krw));

function formatNumber(n) {
  if (isNaN(n)) return '0';
  return Number (n).toFixed (2);
}
formatNumber('12.345') // 12.35
```

`Number.toFixed()`: 숫자의 소수점 자릿수를 제어한다. 다만, 문자열로 반환하는 점에 유의해야 한다.
`isNaN()`을 통해 유저의 입력 값을 포맷팅할 수 있다.

#### Math

기본적인 수학 연산 Method를 포함해 상수를 다루는 객체로, BigInt 타입과 호환되지 않고 반드시 Number 타입만을 인자로 다룬다.

```javascript
function getMaxDiff(nums) {
  return Math.max(...nums) - Math.min(...nums);
}
getMaxDiff([-1, -4, -7, 11]);

function getRandomNumberInRange (min, max) {
  return Math.floor(Math.random()*(max - min + 1)) + min;
}

Array.from({ length: 10 }).map(() => getRandomNumberInRange(50, 100))
```

#### Date

특정 시점의 날짜를 표시하기 위한 객체로, 날짜와 관련된 작업을 위한 여러 Method를 포함한다.(연도, 월, 일, 시, 분, 초, 밀리초, 요일 등을 가져올 수 있다.)

```javascript
function isWeekend(today) {
  let day = today.getDay();
  return day === 0 || day === 6;
}

console.Log(isWeekend (new Date("2021/9/12")));

function addDays (date, days) {
  date.setDate(date.getDate() + days)
  return date.toDateString()
}

addDays(new Date("2021/9/22"), 100) // Fri Dec 31 2021

function timeDiff(date1, date2) {
  return date2.getTime() - date1.getTime();
}

let dayTime = 60 * 24 * 60 * 1000
function fromNow(date) {
  let diff = timeDiff(date, new Date())
  return `${Math.floor(diff / dayTime)} days ago...`;
}

fromNow(new Date("2021/9/1"))
```

#### String

JavaScript 문자열 원시 타입에 대한 객체로, 문자열을 조작하기 위한 여러 Method를 포함한다.

```javascript
function toUserlist(users) {
  return users
    .filter((user) => !user.includes("Admin"))
    .map((user) => user.trim().toUpperCase())
    .map((user) => `<li>${user}</li>')`)
    .join("");
}

console.log (toUserlist(["Daniel", "Tom", "Johnny", "Admin"]));

"Daniel, Kim, SW".split(',');               // [ 'Daniel', 'Kim', 'SW']
"Daniel, Kim, SW".replace(',', ' ');        // "Daniel Kim SW"
"Daniel, Kim, SW".includes("Kim");          // true
"        Daniel, Kim, SW      ".trim();     // "Daniel,Kim,SW"
"Daniel, Kim, SW".index0f("Kim");           // 7
```

#### JSON

JSON 객체와 관련된 Method를 포함한 객체를 의미한다.

```javascript
JSON.stringify({ name: "Daniel", age : 12});        // '{"name":"Daniel","age":12}'
JSON.parse('{"name":"Daniel","age":12}');           // { name: 'Daniel', age: 12 }
```
