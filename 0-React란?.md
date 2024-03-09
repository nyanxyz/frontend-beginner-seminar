# 0. React란?

강의 날짜: 2023년 6월 27일

## 1990년 초

- HTML 등장
- HTML은 문서를 나타내기 위해 만들어짐

## 1993년

- HTML을 동적으로 바꿀 수 없음
- submit을 하면 url을 바꿔서 서버에서 그려서 내려줌

## 2005년

- Ajax 등장
- 문서의 바꿀 부분만 데이터(xml)를 가져와서 자바스크립트로 특정 DOM을 바꾸는 방법
- Gmail, Google Maps를 Ajax로 구현해 “새로고침을 하지 않고 내용이 변한다니!”와 같은 놀라움이 있었음

## HTML5

- 2014년
- 아이폰에 flash가 탑재되지 않으며 발전
- 웹 애플리케이션을 위한 스펙 추가

---

## 과거에는…

- 디자이너: 디자인
- 퍼블리셔: HTML
- 백엔드: 데이터 삽입

- Data가 바뀔 때 DOM에 바인딩하는 것이 어렵다
    - → SSOT를 지키는 것이 어렵다

## jQuery

- DOM 조작을 쉽게 할 수 있음

```jsx
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("#test").html("Hello, jQuery!");
  });
});
</script>
</head>
<body>

<h2 id="test">Hello, World!</h2>
<button>Click me</button>

</body>
</html>
```

- 직접적인 DOM 조작의 남용으로 성능이 느려짐
- 대형 어플리케이션에는 한계가 있음

## React

React provides **a declarative API** so that you don’t have to worry about exactly what changes on every update. … the choices we made in React’s **“diffing” algorithm** so that component **updates are predictable** while being **fast enough** for high-performance apps.

- 컴포넌트 함수가 Element를 return하기만 하면 DOM에 적용하는 것은 React가 해줌
- DOM 갱신, 데이터와 UI 바인딩 해결
- JSX 문법으로 코드에 응집성이 좋다
- Virtual DOM