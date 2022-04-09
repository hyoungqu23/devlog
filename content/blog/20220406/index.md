---
title: [Elice] SW 엔지니어 트랙 2기 3일차 mini-log
date: "2022-04-06T23:46:37.121Z"
description: Elice, SW, WEB, Frontend, Bootcamp, 이고잉, HTML, CSS
---
# CSS
처음에는 디자인을 하는 태그를 만들었다.(`<font>` 등) HTML은 정보를 다루고, WEB은 정보인데, 디자인을 위한 태그들의 등장으로 가치가 떨어졌다.

결국, 디자인을 하는 언어를 새로 만들었다. 이렇게 만들어진 CSS의 등장으로 인해 HTML의 정보적 기능을 온전히 보존하고 디자인 기능을 별도로 분리할 수 있었다.

## CSS 기본 문법
> Selector Declaration

> Selector { Property: Value; }

## CSS 적용 방법
- Inline CSS: `style="..."`
- Internal CSS: `<style>...</style>`
- External CSS: `<link rel="stylesheet" href="style.css">`

## CSS 우선순위
[참고자료](https://stuffandnonsense.co.uk/archives/css_specificity_wars.html)
[참고자료-게임](https://flukeout.github.io/)

## CSS 주요 속성
### `display`
기본값이 있고 이를 CSS로 수정할 수 있다.
- `Block` 화면 전체 만큼
- `Inline` 자기 크기 만큼

> ❗ user agent = 브라우저 ... 브라우저의 기본 설정 값이 존재한다.(F12 통한 개발자 도구에서 확인 가능)

### `margin`
외부 여백

### `padding`
내부 여백

### `border`

## Grid Layout

## 미디어쿼리
반응형 웹 디자인을 위해 활용한다.

`max-height: 480px`: 480px 이하에서 적용되는 쿼리
`min-height: 480px`: 480px 이상에서 적용되는 쿼리


[참고 - bootstrap(반응형)](https://getbootstrap.com/)
[참고 - 코드 공유](https://jsbin.com/?html,css,output)