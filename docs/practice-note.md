# Practice Note

Clone project에서 새로 배운 것

## index.html

- 대부분의 서버들은 기본적으로 `index.html` 파일을 처음 탐색한다.
- Website의 entry point 역할을 한다.

## BEM(Block Element Modifier) Convention

- CSS를 읽기 쉽게 작성하기 위한 이름 명명 규칙
  1. `block__element--modifier` 형식으로 작성한다.
  2. `id`보다 `class`를 우선 사용한다.
     - 나중에 `id`였는지 `class`였는지 알기 어려워서 통일시킴
     - 특별한 이유가 없다면 `class`를 사용한다.
- 사용 예: `user-component__title--not-bold`
  1. `user-component`라는 block 안에서
  2. `title`에 해당하는 class인데
  3. `not-bold`라는 modifier로 동작

## Form attributes: action, method

- `action` : Form 안에서 submit 되었을 때 이동할 URL
- `method` : `action`을 실행하는 방법
  - `post`
    - Network request에 사용
    - Data를 request body에 데이터를 담아 보내는 방식
    - Backend server에 데이터를 전송할 때 사용하게 됨
  - `get`
    - Data를 URL에 담아서 보내는 방식
    - URL을 가진 누구나 data를 볼 수 있으므로 보안에 취약
    - **username, password 같은 민감한 정보를 넣으면 안된다.**

## Icon 사용하기

- `<i></i>` : icon element
- 직접 만들어서 사용
- Icon provider를 설치해서 사용
  - e.g. Font awesome은 script를 사용해서 `fa` namespace의 class를 갖는 아이콘 팩을 추가한다.
  - `<script></script>` : `<body></body>`의 가장 마지막에 추가한다.

## CSS structure

- HTML에서 css link를 한 번만 추가해도 동작하도록 만들기 위해 main css file이 다른 css file을 import하도록 만든다.
- `@import url("");` : Font 및 URL로부터 외부 css를 import 한다.
- `@import "{PATH}";` : 다른 경로에 있는 css file을 import 한다.
- Base files
  - `styles.css`
    - main file
    - Font 및 다른 css file을 import하고 전역 style을 선언한다.
  - `reset.css`
    - 브라우저가 element에 입히는 기본 style을 제거하는 css
    - 브라우저 기본 style을 모두 지우고 작업해야 하므로 다른 css들 보다 먼저 import한다.
  - `variables.css`
    - Custom property(or Variable)들을 선언해 두는 css
    - 다른 css에서도 사용해야 하므로 다른 css들 보다 먼저 import한다.
- CSS는 적용하는 block component를 기준으로 파일을 나눠서 작성하는게 좋다.
- CSS 파일을 나눌 때는 용도에 따라 분리하는게 좋다.
  - component : 다른 screen에서도 재사용되는 component에 대한 CSS
  - screens : 특정 screen에서만 사용되는 component에 대한 CSS

## CSS의 기본 동작

1. width를 200px로 설정 -> box width를 200px로 만듦
2. padding-left를 50px로 설정
3. 이 때, padding을 준 공간은 사용할 수 없으므로 content width는 150px가 되어 버림
4. CSS는 width를 200px로 만들기 위해 padding만큼 content 영역 width를 넓힘
5. 결과적으로 250px의 width를 가지게 됨 -> width 200px과 padding 50px을 모두 가지려고 함

즉, width를 parent의 100%로 설정했지만 좌/우 padding이 총 100px 있으므로
content width가 100px만큼 늘어나서 화면 밖으로 나가버린다.

## box-sizing

- box의 최종 width/height를 계산하는 방법 설정
- content-box(default) : Default CSS behavior -> 위의 문제 발생
- border-box : border and padding이 box size에 포함되도록 함
  - padding을 넣어도 box size를 변경하지 말라고 CSS에게 알려준다.
  - 즉, padding을 넣어도 box size를 그대로 유지하고 싶을 때 사용

## Width가 다른 세 개의 element 중 가운데 element의 가운데 정렬

1. 모든 div를 가운데에 배치한다.
   ```css
   .status-bar {
     display: flex;
     justify-content: center;
   }
   ```
2. 각 div가 같은 크기를 갖게 한다.
   ```css
   .status-bar__column {
     /* parent: status-bar */
     /* status-bar는 3개 elemtn를 배치한다고 가정 */
     width: 33%;
   }
   ```
3. 가운데 element가 child들을 가운데 정렬하도록 한다.
   ```css
   .status-bar__column:nth-child(2) {
     display: flex;
     justify-content: center;
   }
   ```
4. 마지막 element가 child들을 오른쪽 정렬하도록 한다.
   ```css
   .status-bar__column:last-child {
     display: flex;
     justify-content: flex-end;
     align-items: center; /* cross axis 정렬 필요할 때 추가 */
   }
   ```

=> 모두 같은 너비를 갖게 한 다음에 각 container에서 위치를 조정한 방법이다.

## Status bar를 상단에 고정시키기

1. `position: fixed;`
   - fixed position을 갖게 하고 width를 고정시키면 스크롤해도 상단에 고정된다.
   - 이 때, width 정보가 사라지므로 `width` property도 추가한다. (e.g. `width: 100%`)
   - status bar 아래에 있는 다른 box들이 겹치는 문제가 있다.
   - `padding-top`을 줘서 해결할 수도 있지만 그다지 좋은 방법은 아니다. (status bar의 높이가 달라진다면 top padding을 일일이 수정해 줘야 한다.)
2. `position: sticky;`
   - box가 갖는 border 및 padding이 화면 밖으로 벗어나지 않도록 스크롤하면 따라다니게 만듦
   - status-bar는 상단에 딱 붙어있는 box이므로, 스크롤하면 계속 위에 붙어있게 된다.
   - fixed position과 달리 다른 layer로 이동하지 않으므로 다른 box와 겹치지 않는다.

## .not()

- Condition을 만족하지 않는 element들을 선택함
- `login-form` id를 가진 element 하위에서 `type`이 `"submit"`이 **아닌** input을 찾는 예시
  ```css
  #login-form input:not([type="submit"]) {
    border-bottom: 1px solid rgba(0, 0, 0, 0.2);
    transition: border-color 0.3s ease-in-out;
  }
  ```

## inherit

- Property value로 사용
- Parent value를 상속받아 사용함

## Shortcuts

- `!` : HTML form 자동완성
- `link:css` : HTML에 css file를 연결하는 `<link>` tag 추가 (with stylesheet)

## Flex order

- `order` : Flexbox가 element들을 배치하는 순서
- Flexbox 안에 들어가는 element들의 order를 변경해서 배치되는 순서를 조작할 수 있다.
- Flex children에만 사용할 수 있다.
- 단순히 '좌->우' 순서를 '우->좌'로 바꾸려고 한다면, order를 조절하지 않고 `justify-content`를 `row-reverse`로 설정해도 된다.

```css
.message-row--own message__bubble {
  order: 1;
}
.message-row--own message__time {
  order: 0;
}
```

## z-index

- Screen에 표시되는 element들의 z axis 방향 순서
- 'Layer'라고도 부른다.
- 화면 맨 앞에 나와 있을수록 `z-index`가 높고, `z-index`를 높게 설정할수록 해당 element가 화면 앞으로 배치되어 다른 element들을 덮어쓴다.

## will-change

- 브라우저에게 어떤 property가 변경될 것인지 미리 알려줘서 해당 property를 변경하는 작업에 GPU 자원을 더 사용해서 연산 성능을 높임
- `scale()` transform을 사용할 때, scale 값이 너무 작으면 animation이 정상적으로 동작하지 않는 문제가 있었음
- `will-change: transform;` def를 추가하면 transform이 동작할 때 문제를 해결할 수 있다.

## Animation forwards, delay

- `forwards`
  - Animation 실행이 종료되면, 해당 element는 최초 상태로 되돌아감
  - `animation`에 `forwards` 값을 추가하면 key frame이 종료된 후 마지막 속성값을 유지시킨다.
- `animation-delay` : animation이 실행되는 시간을 지연시키는 property

```css
@keyframes hideSplashScreen {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}

#splash-screen {
  animation: hideSplashScreen 0.25s linear forwards;
}
```

- Animation이 종료되면 `#splash-screen`의 `opacity`는 다시 1로 돌아갈 것
- `forwards` 값을 추가함으로써 animation 종료 후 계속 `opacity` 값을 0으로 유지한다.
