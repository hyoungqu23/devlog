---
title: "[Elice SW 2기] mini-log #014 : JavaScript 심화 - Call Stack과 Execution Context, Closure"
date : "2022-04-21T23:46:37.121Z"
description: Elice, SW, WEB, Frontend, Bootcamp, 이고잉, HTML, CSS, JavaScript, OOP, Event, ES6, Closure, this, Execution Context
---

## JavaScript 심화

### 00. JavaScript 함수가 실행되는 과정

JavaScript는 어떤 코드도 없는 경우에도, 실행 환경(Execution Context, 실행 컨텍스트)를 초기화하는데, 이때 다음 세 가지가 환경에 포함되어 초기화된다.

> this, Variable Object, Scope Chain

- **this**
  
  코드가 실행되는 시점의 환경이 가리키는 객체를 의미한다.
  
  어떤 코드도 없는 경우, 브라우저 상에서 최상위 Scope에 존재하는 객체인 window 객체를 의미한다.

- **Variable Object**
  
  변수 객체를 의미하고 Execution Context의 하나의 property로 실행에 필요한 정보를 담고 있다.
  
   변수 객체는 코드가 실행될 때 엔진에 의해 참조되며 코드에서는 접근할 수가 없다.

- **Scope Chain**

  Scope는 코드가 현재 실행되는 환경, 맥락(context), 즉 현재 코드에서 접근할 수 있는 변수, 함수 등을 의미한다.
  
  어떤 코드도 없는 경우, 최상위 Scope인 Global Scope에 위치하므로, 연결된 Scope Chain은 없다.

#### 함수가 존재하는 경우 코드가 실행되는 과정

```javascript
function myFunc() {
  let a = 10;
  let b = 20;

  function add(first, second) {
    return first + second;
  }

  return add(a, b)
}

myFunc();
```

##### Call Stack

- `myFunc()` 선언 이전에 어떤 코드도 존재하지 않는 것처럼 Execution Context, 즉 Global Context가 초기화되며, this, Variable Object, Scope Chain이 초기화된다.
- `myFunc()`을 선언하면, 새로운 Function Execution Context가 생성되고, 기존 Execution Context, 즉 Global Context는 아래에 그대로 존재하게 된다.
- `myFunc()`가 종료되면 새로이 생성된 Function Execution Context가 종료되어 제거된다.
- 모든 코드가 종료되는 경우에, 기존 Execution Context, 즉 Global Context도 제거된다.

##### Function Execution Context(`myFunc()`)

- **this**

  JavaScript를 Strict Mode로 실행하는 경우에, `this`가 `undefined` 값을 갖는다.

- **Variable Object**

  변수 `a`, `b`, 함수 `add()`가 저장된다.

- **Scope Chain**
  
  Global Scope, 즉 이전의 Execution Context가 연결되어 다른 변수를 찾아야하는 경우 연결된 Scope Chain 따라 검색하게 된다.

  이때 함수가 모두 종료되면, Global Scope로 돌아가게 된다.

##### Function Execution Context(`add()`)

- **this**

  이전의 Function Execution Context와 동일하게 `this`가 `undefined` 값을 갖는다.

- **Variable Object**

  변수 `first`, `second`가 저장된다.

- **Scope Chain**
  
  myFunc Scope와 Global Scope가 존재하고, 즉 이전의 Execution Context가 연결되어 다른 변수를 찾아야하는 경우 연결된 Scope Chain 따라 검색하게 된다.

> 즉, 함수가 실행되는 경우 해당 함수 Scope에 따라 Execution Context가 생성되고, 연결된 Scope Chain을 따라 Global Scope에 접근할 수 있다.

#### 객체가 존재하는 경우 코드가 실행되는 과정

```javascript
let obj = {
  name: Daniel,
  method: function(number) {
    return this.name.repeat(number);
  }
}

function myFunc() {
  let n = 10;
  return o.method(n);
}

myFunc();
```

##### Call Stack

- 가장 처음에는 어떤 코드도 존재하지 않는 것처럼 Execution Context, 즉 Global Context가 초기화되며, this, Variable Object, Scope Chain이 초기화된다.
- 이후 Global Context가 되어 this는 window를 가리키고, Variable Object에 변수 `o`와 `myFunc()` 함수가 존재한다. 다만, Scope Chain은 Global Context이기 때문에 비어있다.
- 다음으로 `myFunc()`가 실행되면서 Function Execution Context가 생성된다.
- `myFunc()`가 호출한 `o.method()`가 실행되면 Object Execution Context가 생성되며, 이때 this는 해당 객체 `o`를 의미한다. 즉, 어떤 객체에 속한 method의 경우 this는 해당 객체를 가리킨다. 다만, 환경에 따라 this가 가리키는 대상이 변경될 수 있다.
- 객체의 method가 종료되면, Object Execution Context가 제거되고, 이후 `myFunc` 함수가 종료되면, Function Execution Context도 종료된다.
- 마지막으로 모든 코드가 종료되는 경우에, 기존 Execution Context, 즉 Global Context도 제거된다.

##### Global Execution Context

- **this**

  this는 Global Execution Context에서 window를 가리킨다.

- **Variable Object**

  객체 `o`와 함수 `myFunc()`가 저장된다.

- **Scope Chain**
  
  이미 Global Scope이므로 존재하지 않는다.

##### Function Execution Context(`myFunc()`)

- **this**

  JavaScript를 Strict Mode로 실행하는 경우에, `this`가 `undefined` 값을 갖는다.

- **Variable Object**

  변수 `n`이 저장된다.

- **Scope Chain**
  
  Global Scope, 즉 이전의 Execution Context가 연결되어 다른 변수를 찾아야하는 경우 연결된 Scope Chain 따라 검색하게 된다. 이때 Function Execution Context에서는 Global Scope와 연결되어 있다.

##### Object Execution Context(`o`)

- **this**

  JavaScript에서 객체의 method 경우에는 `this`가 `o`, 즉 해당 객체를 가리킨다.

- **Variable Object**

  변수 `number`가 저장된다.

- **Scope Chain**
  
  Global Scope와 myFunc Scope가 차례로 존재한다. 이전의 Execution Context에 존재하는 다른 변수를 찾아야하는 경우 연결된 Scope Chain 따라 검색하게 된다.

### 01. Execution Context, 실행 컨텍스트

실행 컨텍스트(Execution Context)는 **Scope, hoisting, this, function, closure** 등의 동작 원리를 담고 있는 JavaScript의 핵심 원리로, 실행 맥락이라고도 불리며 JavaScript 코드가 실행되는 환경을 의미한다.

실행 컨텍스트(Execution Context)에는 JavaScript 엔진이 코드를 실행하기 위해 필요한 코드에 대한 정보들, 즉 **선언된 변수와 함수, 객체, Scope, this, arguments 등에 대한 레퍼런스**가 존재한다.

실행 컨텍스트(Execution Context)는 전역(Global)에서 시작해, 함수가 호출될 때 **Call Stack(Execution Context Stack)**에 쌓이게 된다.

- JavaScript가 실행될 때 **Global Execution Context, GEC**가 생성된다.
- 함수가 실행될 때 **Function Execution Context, FEC**가 생성된다.

### 02. this

this는 Execution Context가 생성될 때 함께 생성되어 코드가 실행되는 환경을 가리킨다.

#### 함수가 호출되는 상황

- 함수 호출

  ```javascript
  myFunc();
  ```

- 메서드 호출

  ```javascript
  o.method();
  ```

- 생성자 호출

  ```javascript
  function Person() {
    this.name = 'abc';
  }
  const p = new Person();
  ```

- 간접 호출: Function 객체의 method `call`, `apply` 등을 통해 간접 호출한다.

  ```javascript
  f.call();
  ```

  `bind` 함수는 특정 this 변수에 해당되는 객체를 method에 묶어주는 함수로, 간접 호출이 된다.
- 콜백 함수(특정 동작 이후 불려지는 함수, 보통 다른 함수의 인자로 보내지는 함수)의 호출

  ```javascript
  function callback() { console.log('callback') }
  function myFunc(name, cb) { console.log(`name : ${name}`); cb(name); };
  myFunc('Daniel', callback);
  ```

#### Dynamic Binding

함수는 다양한 환경에서 호출될 수 있고, 이러한 호출 환경에 따라 this는 동적으로 설정된다. 이를 Dynamic Binding이라고 한다. 이를 조작하기 위해 Function 객체의 method인 `bind`, `call`, `apply` 등을 활용할 수 있다.

```javascript
let o = {
  name: 'Daniel',
  f1: () => {
    console.log("f1 this :", this);
  },
  f2: function () {
    console.log("f2 this :", this);
  },
};

o.f1();   // global
o.f2();   // o

setTimeout(o.f1, 10);     // global
setTimeout(o.f2, 20);     // global
```

화살표 함수 호출 시 this는 함수가 생성된 환경(고정)을 가리키고, 일반 함수 호출 시 this는 함수가 호출된 환경(동적)을 가리킨다. 이때, `setTimeout()`의 콜백 함수로 호출하면 둘 모두 Global Execution Context를 가리킨다. 즉, `setTimeout()` 함수의 인자로 콜백 함수를 보내면 특정 시간 이후에 해당 함수는 실행된다. 특정 객체의 메서드라 하더라도, 실행될 때 함수가 실행되는 환경은 바뀌게 된다. 따라서 미리 바인딩 된 this가 없을 경우 this는 함수를 둘러싼 환경을 가리키도록 바뀐다.

#### binding

```javascript
const o = {
name: "Kim",
  changeMyName: function (name) { this.name = name },
};

const o2 = {
  name: "Song",
};

function callFuncWithArg(f, arg) {
  f(arg);
}

o.changeMyName.bind(o2)("Sam");
console.log("1번 - ", o2.name);               // Sam
callFuncWithArg(o.changeMyName, "Daniel");
console.log("2번 - ", o.name);                // Kim
o.changeMyName("Sam");
console.log("3번 - ", o.name);                // Sam
```

1번이 Sam인 이유는, bind 메서드로 기존 o의 execution context를 o2의 execution context로 변환했기 때문이다.
2번이 Kim인 이유는, o의 changeMyName 메서드의 execution context가 callFuncWithArg에서 그대로 유지되기 때문이다. o의 changeMyName 메서드는, callFuncWithArg의 인자로 넘겨질 때 execution context가 dynamic binding 됩니다. 따라서 o.changeMyName은 global을 execution context로 갖게 되고, o.name은 바뀌지 않습니다.
3번이 Sam인 이유는, o.changeMyName 메서드의 execution context가 o로 유지되기 때문이다.

#### 화살표 함수와 일반 함수의 this

화살표 함수의 this는 호출된 함수를 둘러싼 Execution Context (즉, 화살표 함수가 선언될 때의 this)를 가리키고, 일반 함수의 this는 새롭게 생성된 Execution Context 즉, Call Stack에서 가장 높은 위치에 있는 Context를 가리킨다.

이때 화살표 함수의 this는 bind 등을 통해 변경할 수 없다.

```javascript
const o = {
  method() {
    console.log("context: ", this);     // o
    let f1 = function () {
      console.log("f1 this: ", this);
    }
    let f2 = () => {
      console.log("f2 this: ", this);
    }
    f1();     // global   ??
    f2();     // o
  },
};
o.method();
```

### 03. Closure

#### 함수와 일급 객체(first-class object)

일급 객체란 다른 변수처럼 대상을 다룰 수 있는 것을 의미한다. 함수는 Function 이라는 전역적으로 존재하는 일급 객체로, JavaScript에서 개발자가 만든 function은 해당 객체를 상속받은 인스턴스가 된다.
> 함수를 다른 함수의 인자로 넘기면, 다른 함수 내부에서 그 함수를 호출할 수 있다. 함수를 인자로 받아 자유롭게 활용할 수 있고, 인자로 받은 함수는 또한 다른 함수를 인자로 받을 수 있다.

> 함수 안에 함수를 선언했을 때 그 함수를 외부에서 쓰고 싶다면, 그 함수를 리턴하여 사용할 수 있다.

> 함수의 실행이 끝나도 내부 변수를 유지할 수 있다. 함수 안에서 closure가 만들어지면, 내부 변수가 메모리에 남아 closure에 활용된다.

```javascript
// 일급 객체로서의 함수

function add(a, b) {
  return a + b;
}

// 함수를 다른 함수의 인자로 넘긴다.
[1, 2, 3].reduce(add, 0);

(() => {
  console.log('익명 화살표 함수 생성');
})()

function outer(a) {
  function inner(b) {
    return a + b;
  } // 중첩 함수 생성
  return inner(10);
}

const Person = (name) => {  // 함수를 변수로 생성
  const printName = () => console.log(name);
  return { printName }
} // 함수를 return하면서 closure 생성

const person = Person('Daniel');
person.printName();

function printName(name) {
  console.log('name :', name);
}

// 함수의 비교
console.log(printName === person.printName);
```

#### Closure

JavaScript의 Closure는 함수의 일급 객체 성질을 이용한다. 함수가 생성될 때, 함수 내부에서 사용되는 변수들이 외부에 존재하는 경우 그 변수들은 함수의 Scope에 저장된다. 이때 함수와 함수가 사용하는 변수가 저장된 공간을 Closure라고 한다.

함수를 생성해서 반환하는 팩토리 함수 내부에서 생성된 변수는 팩토리 함수의 실행이 종료되어도 메모리에 남아 있게 되는 것을 확인할 수 있다.

```javascript
function createCard() {
  let title = "";
  let content = "";

  function changeTitle(text) {title = text}
  function changeContent(text) {content = text}

  function print() {
    console.log("TITLE - ", title);
    console.log("CONTENT - ", content);
  }
  return { changeTitle, changeContent, print };
}

// 각각 별개의 closure로 다른 메모리 공간에 저장된다.
const card1 = createCard();     

card1.changeTitle("생일카드");
card1.changeContent("생일 축하해");
card1.print();

const card2 = createCard();

card2.changeTitle("감사카드");
card2.changeContent("고마워");
card2.print();
```

```javascript
let rate = 1.05;

function app() {
  let base = 10;
  return function (price) {
  return price * rate + base;
};

const getPrice = app();
getPrice(120)           // 136
```

이 경우 `rate`는 함수 외부 Scope에, `base`는 함수 내부 Scope에 존재한다. 함수가 참조하는 변수는 실행 시점의 Execution Context에 의해 Scope가 결정된다. 이렇게 결정된 Scope에 따라 변수가 영향을 받는데, `rate`는 `app` 함수 호출과 무관하게 값이 수정되는 것이 반영되지만, `base`의 경우 함수 호출 시 매번 생성되는 별도의 메모리 공간에 할당되는 변수이기 때문에 값이 수정되어도 영향을 미치지 못한다. 즉, `rate`와 같은 외부 변수는 클래스의 `static` 변수와 유사하다.

### 04. Rest, Spread Operator

#### Rest Operator

함수의 인자, 배열, 객체 중 나머지 값을 묶어 사용하도록 한다.

함수 인자 rest는 인자들을 **배열**로 묶어 사용할 수 있게 한다. rest operator을 이용해 가변 인자 함수를 구현할 수 있다.

```javascript
function findMin(...rest) {
  return rest.reduce((a, b) => a < b ? a: b);
};

findMin(7, 3, 5, 2, 4, 1);             // 1
```

객체 rest는 지정된 필드 외의 나머지 필드를 **객체**로 묶어 사용할 수 있게 한다. 객체의 경우, rest operator로 묶을 때 필요한 변수를 제외할 수 있다.

```javascript
const obj = {
  name: "Jennie",
  age: 23,
  address: "Seoul",
  job: "SE",
  gender: "male",
};

const { age, name, ...rest } = obj;
findSamePerson(age, name);
```

배열 rest는 나머지 인자를 다시 **배열**로 묶어 사용할 수 있게 한다. 인자가 하나도 없더라도, rest operator는 빈 배열을 반환한다.

```javascript
function sumArray(sum, arr) {
  if (arr.length === 0) return sum;
  const [head, ...tail] = arr;
  return sumArray(sum + head, tail);      // 재귀함수를 통한 reduce 함수 구현
};

sumArray (0, [1, 2, 3, 4, 5]);
```

#### Spread Operator

Rest Operator를 통해 만들어진 묶인 배열 혹은 객체를 각각의 필드로 변환하는 연산자로, 각각 또 다른 배열의 인자, 함수의 인자, 객체로의 spread를 지원한다.

```javascript
let o = {
  name: "Daniel",
  age: 23,
  address: "Street",
  job: "Software Engineer",
};

let o2 = {...o, name: "Tom", age: 24 }
let o3 = { name: "Tom", age: 24, ..o }    // 뒤에서 덮어 씌우기 때문에 변경된 name, age가 모두 덮어쓰기 된다.

o2.job        // Software Engineer
o3.name       // Daniel
```

```javascript
function findMinInObject(o) {
  return Math.min( ...Object.values(o) )      // 객체의 value를 배열로 반환 -> spread로 펼쳐 하나씩 넘겨준 것과 동일한 효과
}

let o1 = { a: 1 }
let o2 = { b: 3 }
let o3 = { c: 7 }

findMinInFields(
  mergeObjects(o1, o2, o3)
)       // 1
```

배열은 iterable 성질을 가진 객체이므로, 객체에 spread operator로 합쳐도 에러가 발생하지 않습니다. 배열의 각 index에 있는 값들이 ‘0’: 1, ‘1’: 2 처럼 객체에 합쳐집니다.

객체의 필드들을 배열에 spread operator로 합치면 에러가 발생한다.
일반 객체는 iterable 성질이 없으므로, 배열 같은 iterable 객체에 합치려 하면 에러가 발생합니다. 단, iterable을 지원하는 객체는 spread operator로 합칠 수 있습니다.

spread operator로 객체를 복사하면, 객체나 배열 필드의 경우 reference만 복사된다.
객체나 배열 필드는 단순히 reference만 복사됩니다. 따라서, deep copy를 위한 별도의 작업을 해주어야 합니다.

```
function ArrayManipulator(array) {
  function addElement(element) {
    // 예시 코드입니다.
    // 변환된 배열을 `ArrayManipulator`의 인자로 넘겨 리턴합니다.
    return ArrayManipulator([...array, element]);
  }

  function removeElement(index) {
    // 인자를 제거한 배열을 만들어주세요.
    return ArrayManipulator([ ...array.slice(0, index), ...array.slice(index + 1) ]);
  }

  function updateElement(index, element) {
    // 인자를 갱신한 배열을 만들어주세요.
    return ArrayManipulator([ ...array.slice(0, index), element , ...array.slice(index + 1) ]);
  }

  function mapElements(func) {
    // 배열 전체를 변환하세요.
    // Array 객체의 내장 map 함수를 활용해 보세요.
    return ArrayManipulator(array.map(e => func(e)));
  }

  function filterElements(func) {
    // 배열의 특정 원소를 필터하세요.
    // Array 객체의 내장 filter 함수를 활용해 보세요.
    return ArrayManipulator(array.filter(e => func(e)));
  }

  function getArray() {
    return array;
  }

  return {
    addElement,
    removeElement,
    updateElement,
    mapElements,
    filterElements,
    getArray,
  };
}

export default ArrayManipulator;
```
