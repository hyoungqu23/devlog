---
title: "[Elice SW 2기] mini-log #003 : CSS의 이해"
date : "2022-04-06T23:46:37.121Z"
description: Elice, SW, WEB, Frontend, Bootcamp, 이고잉, HTML, CSS
---

## CSS
처음에는 디자인을 하는 새로운 태그를 만들었다.(`<font>` 등) 하지만, HTML은 정보를 다루고, WEB은 **정보**인데, 디자인을 위한 태그들의 등장으로 그 가치가 떨어졌다.

결국, 디자인을 하는 언어를 새로 만들었다. 이렇게 만들어진 CSS의 등장으로 인해 HTML의 정보적 기능을 온전히 보존하고 디자인 기능을 별도로 분리할 수 있었다.

### CSS 기본 문법
> Selector Declaration<br />
> `Selector { Property: Value; }`

[CSS Selectors](https://www.w3schools.com/css/css_selectors.asp)

### CSS 적용 방법
- Inline CSS: `style="..."`<br />
- Internal CSS: `<style>...</style>`<br />
- External CSS: `<link rel="stylesheet" href="style.css">`

### CSS 우선순위
[참고자료](https://stuffandnonsense.co.uk/archives/css_specificity_wars.html)<br />
[참고자료 - 게임](https://flukeout.github.io/)

### CSS 주요 속성
#### 001. [`display`](https://www.w3schools.com/cssref/pr_class_display.asp)
기본값이 있고 이를 CSS로 수정할 수 있다.
- `Block` 화면 전체 만큼
- `Inline` 자기 크기 만큼

> ❗ user agent = 브라우저 ... 브라우저의 기본 설정 값이 존재한다.(F12 통한 개발자 도구에서 확인 가능)

#### 002. [`margin`](https://www.w3schools.com/cssref/pr_margin.asp)
Content의 외부 여백을 설정하는 단축 속성. [여기](https://www.w3schools.com/css/css_margin.asp)서 자세히 확인할 수 있다.

#### 003. [`padding`](http://w3schools.com/cssref/pr_margin.asp)
Content의 내부 여백을 설정하는 단축 속성. [여기](https://www.w3schools.com/css/css_padding.asp)서 자세히 확인할 수 있다.

#### 004. [`border`](https://www.w3schools.com/cssref/pr_border.asp)
Content의 테두리를 설정하는 단축 속성. [여기](https://www.w3schools.com/css/css_border.asp)서 자세히 확인할 수 있다.

### [Grid Layout](https://www.w3schools.com/css/css_grid.asp)
행과 열로 구성된 그리드 시스템을 활용하는 것으로, 기존에 활용하던 float, position보다 더 쉽게 웹 페이지의 구성을 만들 수 있게 해준다.

### 미디어쿼리
[반응형 웹 디자인(RWD)](https://www.w3schools.com/css/css_rwd_intro.asp)을 위해 활용한다.

`max-height: 480px`: 480px 이하에서 적용되는 쿼리<br />
`min-height: 480px`: 480px 이상에서 적용되는 쿼리

<hr />

[참고 - bootstrap(반응형)](https://getbootstrap.com/)<br />
[참고 - 코드 공유](https://jsbin.com/?html,css,output)