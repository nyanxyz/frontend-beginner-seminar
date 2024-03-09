# 4. Lifecycle, useEffect, useState

강의 날짜: 2023년 7월 4일

## 라이프사이클

[https://react.dev/learn/lifecycle-of-reactive-effects](https://react.dev/learn/lifecycle-of-reactive-effects)

Every React component goes through the same lifecycle:

- A component *mounts* when it’s added to the screen.
- A component *updates* when it receives new props or state, usually in response to an interaction.
- A component *unmounts* when it’s removed from the screen.

## useEffect

[https://react.dev/learn/synchronizing-with-effects](https://react.dev/learn/synchronizing-with-effects)

```tsx
useEffect(() => {
  console.log("Mount");

  return () => {
    console.log("Unmount");
  };
}, []);
```

```tsx
useEffect(() => {
  console.log("Update");
});
```

```tsx
useEffect(() => {
  console.log("Update number");
}, [number]);

useEffect(() => {
  console.log("Update string");
}, [string]);
```

## useState

- 리렌더링이 일어나려면 업데이트가 일어나야 한다.
- 또는, 업데이트가 일어나면 이를 반영하기 위해 리렌더링이 일어나야 한다.
- 어떤 값이 변화했을 때 이것이 DOM에 반영되려면, state나 props가 변해야 한다.

```tsx
function Component() {
	const [count, setCount] = useState(0);
	
	const handleClick = () => {
	  setCount(2);
	};
	
	return (
	  <div>
	    <div>count: {count}</div>
	    <button onClick={handleClick}>count를 2로 변경</button>
	  </div>
	);
}
```

## 두 컴포넌트가 하나의 state를 사용해야 할 때

[https://react.dev/learn/sharing-state-between-components](https://react.dev/learn/sharing-state-between-components)