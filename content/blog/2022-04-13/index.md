---
title: "[Elice SW 2기] mini-log #008 : JavaScript의 이해 3"
date : "2022-04-13T23:46:37.121Z"
description: Elice, SW, WEB, Frontend, Bootcamp, 이고잉, HTML, CSS, JavaScript, CodingTest, DOM, event
---
## JavaScript 이해
### Review
`git add .`으로 버전 관리하는 것은 좋지 않다. 데이터베이스의 중요한 정보가 버전 관리 될 수 있기 때문이다. 결국, 하나하나 파일을 확인하고 Staging하여 Commit해야 한다.(ignore 필요)
`git commit -a "message"`: 한 번은 명확하게 `add`해야 활용할 수 있는 옵션으로, 자동으로 `add` 하게 하는 옵션이다.
VSCode의 동기화는 `pull` 한 후 `push`하는 방식이다.

#### 버그 탐색을 위한 Binary Search
전체의 절반만 탐색하는 방식.

#### `...` BTN 구현하기
[`<input type=button />`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button)
[`<span>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/span)
[`document.getElementById('hidden')`](https://developer.mozilla.org/ko/docs/Web/API/Document/getElementById)
```html
<div>
  JavaScript is
  <span
    style="background-color: grey; padding: 0 5px; cursor: pointer;"
    onclick="
      if (this.display !== 'none') {
        this.style.display='none';
        document.getElementById('hidden').style.display='inline';
      } else {
        this.style.display='inline';
        document.getElementById('hidden').style.display='none';
      }
    "
  >
    ...
  </span>
  <span id="hidden" style="display: none">
    a programming language that is one of the core technologies of the World Wide Web, alongside HTML and CSS.
  </span>
</div>
```

[`innerHTML`](https://developer.mozilla.org/ko/docs/Web/API/Element/innerHTML): 내부의 텍스트를 포함해 태그 등 다른 것도 가져온다
[`innerText`](https://developer.mozilla.org/ko/docs/Web/API/HTMLElement/innerText): 내부의 텍스트만 가져오지, 태그 등 이외의 것을 가져올 수 없다.
특정 웹 페이지에서 `document.querySelector('body').innerText`를 통해 모든 텍스트를 가져올 수 있다.
[`document.querySelector()`](https://developer.mozilla.org/ko/docs/Web/API/Document/querySelector)
```html
<div>
  JavaScript is
  <span
    style="background-color: grey; padding: 0 5px; cursor: pointer;"
    onclick="
      if (this.display !== 'none') {
        this.style.display='none';
        document.getElementById('content').innerHTML =`a programming language that is one of the core technologies of the World Wide Web, alongside HTML and CSS.`;
      } else {
        this.style.display='inline';
        document.getElementById('content').innerHTML='';
      }
    "
  >
    ...
  </span>
  <span id="content"></span>
</div>
```

### [Array](https://www.w3schools.com/js/js_arrays.asp)
서로 연관된 데이터를 모아서 그룹핑한 후에 이름을 붙인것이 배열이다.
```javascript
let contents = ['HTML', 'CSS', 'JavaScript'];
let members = ['James', 'Smith', 'Jordan'];
let scores = [10, 20, 30];

console.log(contents);
console.log(members);
console.log(scores);
```

#### 배열 조회
`elements`의 `index`를 활용해 배열 `elements`의 값을 조회할 수 있다.
```javascript
console.log(contents[0]);     // HTML
console.log(members[2]);      // Jordan
console.log(scores[1]);       // 20
```

#### 배열 길이 출력
`length` method를 활용해 배열의 길이를 출력할 수 있다.
```javascript
console.log(contents.length);     // 3
```

#### 배열 데이터 추가
[참고 - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
`push(value)` method를 활용해 배열의 맨 마지막에 `elements`를 추가하고, 해당 배열의 길이(`arr.length`)를 반환한다.
```javascript
contents.push("React.JS");

console.log(contents);
```

### [Loop - `for` 문](https://www.w3schools.com/js/js_loop_for.asp)
[참고](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for)
> for (초기값; Boolean(반복 조건); 증감) { 동작문 }

```javascript
console.log(1);
for (let i = 0; i < 3; i++) {
  console.log(2);
  console.log(3);
}
console.log(4);

1
2
3
2
3
2
3
4
```

[`debugger`](https://ko.javascript.info/debugging-chrome)를 활용해서 한 줄씩 코드를 실행할 수 있다.

### Array와 Loop
[`document.write()`](https://developer.mozilla.org/ko/docs/Web/API/Document/write)
```javascript
for (let i = 0; i < members.length; i++) {
  document.write('<li>' + members[i] + '</li>');
}
```
덮어쓰기 되어 원하는 결과가 나오지 않는다.
```javascript
<ul>
<script>
  let contents=['html', 'css', 'js'];
  for (i=0; i<contents.length; i++) {
    document.querySelector('ul').innerHTML = `<li> ${contents[i]} </li>`;}
</script>
</ul>
```
수정
```javascript
<ul></ul>
<script>
  let tag = "";
  let contents=['html', 'css', 'js'];
  for (i=0; i<contents.length; i++) {
    tag += `<li> ${contents[i]} </li>`;
  }
  document.querySelector('ul').innerHTML = tag;
</script>
```
`git reset --hard`로 복구
`; git push` 커밋 후 바로 push

[`document.querySelectorAll()`](https://developer.mozilla.org/ko/docs/Web/API/Document/querySelectorAll)

### [Function](https://www.w3schools.com/js/js_functions.asp)
함수는 서로 연관된 코드를 그룹핑해서 이름을 붙인 것이다.
```javascript
console.log(100000*0.1);

let price = 100000;
let tax_rate = 0.1;

console.log(price * tax_rate);

function calc_tax() {
  let price = 100000;
  let tax_rate = 0.1;
  console.log(price * tax_rate);
}

calc_tax();
```

#### 함수의 입력
함수는 입력 값(parameter?)에 따라서 다른 값을 반환한다.

입력 값의 기본 값을 설정할 수 있다.

#### 함수의 출력
return 키워드를 통해 반환(출력) 값을 설정할 수 있다.