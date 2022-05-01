---
title: "Gatsby Blog Documentation"
date: "2022-04-03T23:46:37.121Z"
description: Gatsby
category: "blog"
---

공부하면서 하나하나 블로그에 세련됨을 추가할 수 있게끔 기록하면서 티끌 모아 태산을 경험하고자 한다.

## 개발 환경 설정
### Gatsby 개발에 있어 필요한 지식들
솔직히 말하자면, 제대로 아는 건 없다고 본다. 다만, 나는 꾸준하게 성장할 예정이므로 상관 없다.

1. HTML
2. CSS
3. JavaScript
4. Command Line
5. React
6. GraphQL

### Gatsby 설치
[`Node.js`](https://nodejs.org/ko/)(와 함께 package manager `npm`), [Git](https://gitforwindows.org/)를 설치한 후 Gatsby site를 개발하기 위한 명령을 실행할 수 있는 `Gatsby-CLI`를 설치해야 한다.
```
npm install -g gatsby-cli
```
설치가 완료되면, 올바른 버전이 설치되었는지 확인해보자!
```
gatsby --version
```
사용 가능한 다른 명령어들은 다음 명령어를 통해 확인할 수 있다는 점 잊지 말자!
```
gatsby --help
```

### Gatsby-blog-starter를 활용한 첫 프로젝트 생성
starter를 선택한 후 다음 명령어로 프로젝트를 생성할 수 있다. 참고로 설정한 프로젝트 이름으로 디렉토리가 생성되는 점을 잊지 말아야 한다.
```
gatsby new {your-project-name} {link-to-starter}
```
이후 다음 명령어로 로컬 서버에서 프로젝트를 실행할 수 있다.
```
cd {your-project-name}
gatsby develop
```