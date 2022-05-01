---
title: "[Elice SW 2기] mini-log #006 : JavaScript의 이해 1"
date : "2022-04-11T23:46:37.121Z"
description: Elice, SW, WEB, Frontend, Bootcamp, 이고잉, HTML, CSS, JavaScript
---

## JavaScript
HTML보다 JavaScript가 동적인 언어이다. JavaScript는 웹 페이지에 생동감을 부여하기 위한 프로그래밍 언어로, 기본적으로 안전한 프로그래밍 언어이다.

예를 들어, 페이지에 새로운 HTML을 추가하거나, 기존의 HTML, CSS를 수정하거나 Mouse, Keyboard 등 사용자의 행동에 따라 반응하는 등의 일을 JavaScript를 통해 할 수 있다.

### JavaScript 실행 방법
- **브라우저의 Console 창(Interactive Mode, 대화형 도구)**<br />
  해당 웹 페이지를 대상으로 JavaScript가 실행된다. 브라우저의 개발자 도구를 통해 사용할 수 있으며, JavaScript 명령어를 입력하거나, 에러 메시지를 확인할 수 있다.
  
  이러한 Console Programming은 한 번에 하나의 프로그램을 실행하여 흐름을 예측할 수 있어 순차적인 프로그래밍에 적합하다.
  ```javascript
  alert("Hello");
  prompt("ID");
  confirm("Please click OK.");

  document.querySelector('body');
  document.querySelector('body').style.backgroundColor = "red";

  speechSynthesis.speak(new SpeechSynthesisUtterance('꼭이요!'));
  ```
> 문서로 기록: 문서에 기록하는 이유는 자동화시키기 위함이다.

- **`<script>` 태그**<br />
  위치는 상관없이, HTML 문서 내에서 `<script>`를 활용해 JavaScript 프로그램을 활용할 수 있다. 외부 script 파일을 `src` 속성을 사용해 HTML 문서에 삽입할 수도 있는데, 이러한 방법이 더 선호된다.
  
  추가적으로, `src` 속성을 통해 외부 스크립트를 불러오는 경우 해당 `<script>` 태그 내부의 코드는 무시된다. 즉, 두 방식을 혼용하지 말고, 각각의 `<script>` 태그로 분리해야 한다.
  ```html
  <html>
    <body>
      <h1>Script Tag</h1>
      <script>
        document.write(1+1);
      </script>
    </body>
  </html>
  ```

- **Event Programming**<br />
  이벤트의 발생에 의해 프로그램의 흐름이 결정되는 프로그래밍 패러다임으로, 사용자와 상호작용하면서 실행하는 방식이다.
  ```html
  <input type="button" value="hi" onClick="
    speechSynthesis.speak(new SpeechSynthesisUtterance('HI'));
    alert('HI');
  " >
  ```

### JavaScript DateType
JavaScript의 변수는 자료형에 관계없이 모든 데이터 타입을 가질 수 있다. 즉, 동적 타입 언어인 JavaScript는 데이터 타입은 존재하나 변수에 저장되는 값의 타입은 언제든지 바꿀 수 있다.

#### Number Type
Number Type은 정수 및 부동소수점 숫자를 나타낸다. 이러한 일반적인 숫자 외에 `∓Infinity`, `NaN`과 같은 특수 숫자 값도 포함된다.

##### `NaN`
`NaN`은 `Not a Number`의 약어로, 계산 중 에러가 발생했다는 것을 나타내준다. 즉, 부정확하거나 정의되지 않은 수학 연산을 사용할 때 발생한다.

##### 산술 연산자
덧셈 연산자 `+`, 뺄셈 연산자 `-`, 곱셈 연산자 `*`, 나눗셈 연산자 `/`, 나머지 연산자 `%`, 거듭제곱 연산자 `**`가 있다.

##### `Math` 객체
`Math` 객체는 JavaScript에서 제공하는 내장 객체로, 다양한 수학 관련 함수와 상수들이 포함되어 있다.
```javascript
Math.random();              // 임의의 수 작성

Math.max(a, b, c, ...);     // 인수 중 최대값 반환
Math.min(a, b, c, ...);     // 인수 중 최솟값 반환

Math.pow(n, power);         // n을 power번 거듭제곱 

Math.floor(n);              // 소수점 첫째 자리에서 내림
Math.ceil(n);               // 소수점 첫째 자리에서 올림
Math.round(n);              // 소수점 첫째 자리에서 반올림
Math.trunc(n);              // 소수부 무시(* IE 미지원 *)
```

#### String Type
JavaScript에서는 문자열을 따옴표로 묶는다.
- 큰따옴표 `" "`
- 작은따옴표 `' '`
- 역따옴표(Backtick): 역 따옴표로 변수나 표현식을 감싼 후 `${…}`으로 변수나 표현식을 넣을 수 있다.

```javascript
console.log('Hello, \
world! <br>');   // 작은 따옴표(줄바꿈 불가능: `\`를 통해 코드 상으로만 가능케 함)
console.log(`Hello, 
world! <br>`);   // 백틱(줄바꿈 가능)

Hello,       world! <br>
Hello, 
      world! <br>
```

##### 문자열과 이항 연산자 `+`
덧셈 연산자 `+`는 숫자의 덧셈을 반환하지만, 이항 결합 연산자로서 문자열을 피연산자로 받는 경우에는 두 문자열을 병합하게 된다.
```javascript
console.log("my" + "String");     // myString
console.log(1 + "2");             // 12
console.log("2" + 1);             // 21
```

#### Boolean DataType
Boolean DataType는 `true`, `false` 두 가지 값만을 갖는 자료형으로, 긍정이나 부정을 나타내는 값을 저장할 때 사용한다. 이러한 논리 자료형을 바탕으로 조건문과 반복문을 작성할 수 있다.

##### 비교 연산자
비교 연산자는 Boolean을 도출하는 연산자이다. 부등호(`>`, `<`, `<=`, `>=`), 동등(`==`, `===`), 부등(`!=`, `!==`) 등이 있다.

### JavaScript Variables
변수는 데이터를 저장할 때 쓰는 이름이 지정된 저장소이다. `let`, `var`를 활용하지 않아도 동작하지만, 적어주는 것이 좋다. 특히, `let`은 한 번 선언한 후에는 동일한 변수명으로는 선언하면 안된다.(`Uncaught SyntaxError: Identifier 'a' has already been declared`)

```javascript
let number;
let string = "Hello, world";
```

#### 변수를 쓰는 이유
주석으로 해당 값에 대해 설명하는 것 보다, 변수를 활용하는 것이 더 효율적이다. 변수는 데이터의 이름을 붙인 것이기 때문이다.
```javascript
console.log(10000 * 0.1); // 10000: price, 0.1: tax_rate
```

```javascript
let price = 10000;
let tax_rate = 0.1;
let tax_amount = price * tax_rate;

console.log(tax_amount);
```

### Flow Control
조건문(Conditional Statement)과 반복문(Loop Statement)을 활용해서 코드의 흐름을 제어할 수 있다.

#### 조건문(Conditional Statements)
조건에 따라 다른 동작을 해야할 때 조건문을 활용한다.
> if (condition) { 동작문 } else { 동작문 }

> (condition) ? 참인 경우 동작문 : 거짓일 경우 동작문

> 참고: `this`는 맥락에 따라서 의미가 변경(가리키는 대상이 변경되는)되는 내장된 변수이다.

#### 반복문(Loop Statements)
반복문을 통해 동일한 코드를 여러번 반복할 수 있다.
> for (begin; condition; step) { 동작문 }

> while (condition)  { 동작문 }

> do { 동작문 } while (condition);
