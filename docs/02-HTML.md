## Overview

HTML(Hyper Text Markup Language)

Tag를 사용해서 브라우저에게 어떤 content를 보여줄지 알려준다.
Tag는 attribute(속성)을 사용해서 content의 모습이나 기능을 변경할 수 있다.
Tag와 attribute를 올바른 위치에서 올바른 방법으로 사용해야 브라우저가 이해하고 원하는 대로 content를 표시해 줄 수 있다.

Tag의 종류는 굉장히 많으므로 다 외우려고 하면 안 된다.
문서를 찾아보거나 구글링을 통해 필요한 tag를 찾아서 사용할 수 있으면 된다.
어떤 tag들을 알고 있는지 보다 **HTML이 브라우저에서 어떤 원리로 작동하는지 이해하는게 더 중요하다.**

문서는 [MDN HTML element reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)를 참고하면 좋다.

## Structure

HTML 파일의 전체 구조

```html
<!DOCTYPE html>

<html>
  <head>
    <meta content="content" />
  </head>
  <body>
    <h1>Hello!</h1>
  </body>
</html>
```

- `<!DOCTYPE html>` : HTML 문서임을 명시하는 것. 항상 첫 줄에 쓴다.
- `<head></head>` : Website 환경 설정 등 눈에 보이지 않는 content를 정의하는 영역. 탭에 표시되는 website 제목, 구글 검색 시 표시되는 문구 등을 설정할 수 있다.
- `<body></body>` : Website에 실제로 표시되는 content들을 정의하는 영역. 실제 content들은 모두 여기에 작성해야 한다.

## Tag

브라우저에게 '여기부터 여기까지가 image야/title이야'와 같이 content의 유형을 알려주기 위해 사용하는 것.
이 때, **tag를 열었으면 항상 같은 tag로 닫아야 한다.**

```html
<tagname>content</tagname>
```

Tag는 중첩으로 사용할 수도 있다.
이 때, pair를 잘 맞춰서 tag를 닫아줘야 한다.

```html
<p>
  Hello! My name is <strong>joey</strong>
</p>
```

닫는 tag를 사용할 필요가 없는 tag를 self-closing tag라고 한다.
```html
<img src="logo.png" />
```

## Tag attribute

- Tag에 속성을 추가해서 content의 모습이나 기능을 변경할 수 있다.
- 모든 tag에서 사용할 수 있는 attribute도 있고, (e.g. id)
- 특정 tag에서만 사용할 수 있는 attribute도 있다. (e.g. src, value 등)
- 모든 tag에 쓸 수 있는 `id`는 그 tag를 고유하게(unique) 식별할 수 있는 값이므로, 
  - Tag에는 `id` attribute를 한 개만 가져야 하고,
  - 다른 tag에서 같은 `id`를 사용하면 안된다.

## Semantic tag

- HTML tag 중에는 그 자체로는 아무 의미가 없는 tag들이 있다. (e.g. `<div>`)
- Semantic tag는 그 자체로 의미를 가지는 tag로, 문서만 보고도 어떤 content인지 쉽게 파악할 수 있다.
- 필요성
  - `<div>`는 content의 영역을 구분해 주는 container box
  - 과거에는 `<div id="header">`와 같은 형태로 사용하면서 `<div>`를 무분별하게 사용하여 HTML 문서만 보고는 어떤 content들이 있는지 파악하기 어려웠음
  - `<div>`대신 `<header>`, `<main>`, `<footer>` 같은 semantic tag를 사용하면 어떤 영역으로 사용하는지 한 눈에 알아볼 수 있음
- 참고 : [MDN Semantics 문서](https://developer.mozilla.org/en-US/docs/Glossary/Semantics#semantic_elements

## Tags and attributes

### Header
```html
<h1>Hello!</h1>
<h2>Hello!</h2>
<h3>Hello!</h3>
<h4>Hello!</h4>
<h5>Hello!</h5>
<h6>Hello!</h6>
```

### List

```html
<!-- Ordered list -->
<ol>
  <!-- List items -->
  <li>one</li>
  <li>two</li>
  <li>three</li>
</ol>

<!-- Unordered list -->
<ul>
  <li>apple</li>
  <li>banana</li>
  <li>orange</li>
</ul>
```

### Link

```html
<a href="https://www.google.com" target="_blank">
  Go to Google
</a>
```

- `href` : 이동할 URL
- `target` : 새 page를 여는 곳
  - `_self` : 현재 탭에서 열기 (default)
  - `_blank` : 새 탭에서 열기

### Image

```html
<img src="https://someimageprovider.com/image.png" />
<img src="localPath/logo.png" />
```

### Meta data

```html
<meta content="some contents" name="description" />
<meta charset="utf-8">
```

- `description` : 구글 검색 시 표시되는 정보를 알려주기 위한 이름
- `charset` : Web page의 text encoding 설정

### Form

```html
<form>
  <input required type="text" />
  <input type="button" value="Button" />
  <input placeholder="Password" type="password" />
  <input type="color" />
  <input type="submit" value="Create Account" />
  <input type="file" />
</form>
```

- `<form></form>` : 정보를 submit할 때 사용하는 control들을 위한 container
- `<input>` : 사용자로부터 data를 입력받는 control

### Sectioning

```html
<div>
  <h1>Hello!</h1>
</div>
<div>
  <h2>My name is Joey.</h2>
</div>
```

- HTML 문서의 content들은 기본적으로 가로로 정렬됨
- 세로로 정렬하기 위해서는 section을 나눠주어야 함
- `<div>`로 content section을 구분할 수 있음