# 5. useContext, useRef, Rules of hooks

강의 날짜: 2023년 7월 11일

## useContext

[https://react.dev/learn/passing-data-deeply-with-context](https://react.dev/learn/passing-data-deeply-with-context)

![Untitled](assets/Untitled%204.png)

![Untitled](assets/Untitled%205.png)

![props drilling to the sky~](assets/Untitled%206.png)

props drilling to the sky~

1. **Create** a context.
2. **Use** that context from the component that needs the data.
3. **Provide** that context from the component that specifies the data.

![Untitled](assets/Untitled%207.png)

![Untitled](assets/Untitled%208.png)

```tsx
export const LevelContext = createContext<number>(1);

type SectionProps = {
  level?: number;
  children: React.ReactNode;
};

export function Section({ level, children }: SectionProps) {
  return (
    <LevelContext.Provider value={level ?? 1}>{children}</LevelContext.Provider>
  );
}

```

```tsx
type HeadingProps = {
  children: React.ReactNode;
};

export function Heading({ children }: HeadingProps) {
  const level = useContext(LevelContext);

  switch (level) {
    case 1:
      return <h1>{children}</h1>;
    case 2:
      return <h2>{children}</h2>;
    case 3:
      return <h3>{children}</h3>;
    case 4:
      return <h4>{children}</h4>;
    case 5:
      return <h5>{children}</h5>;
    case 6:
      return <h6>{children}</h6>;
    default:
      throw Error('Unknown level: ' + level);
  }
}
```

## useRef

[https://react.dev/learn/referencing-values-with-refs](https://react.dev/learn/referencing-values-with-refs)

- 변해도 update가 일어나지 않는 state를 만들 수 있다.

```tsx
const lastId = useRef<number>(0);

lastId.current
console.log(lastId.current); // 0
```

- Storing [timeout IDs](https://developer.mozilla.org/docs/Web/API/setTimeout)
- Storing and manipulating [DOM elements](https://developer.mozilla.org/docs/Web/API/Element), which we cover on [the next page](https://react.dev/learn/manipulating-the-dom-with-refs)
- Storing other objects that aren’t necessary to calculate the JSX.

## Rules of hooks

[https://react.dev/warnings/invalid-hook-call-warning](https://react.dev/warnings/invalid-hook-call-warning)

- Functions whose names start with `use` are called *[Hooks](https://react.dev/reference/react)* in React.

- ✅ Call them at the top level in the body of a [function component](https://react.dev/learn/your-first-component).
- ✅ Call them at the top level in the body of a [custom Hook](https://react.dev/learn/reusing-logic-with-custom-hooks).

```tsx
function Counter() {
  // ✅ Good: top-level in a function component
  const [count, setCount] = useState(0);
  // ...
}

function useWindowWidth() {
  // ✅ Good: top-level in a custom Hook
  const [width, setWidth] = useState(window.innerWidth);
  // ...

	useEffect(() => {
		setWidth(document.width);
	}, []);

	return width;
}
```

- 🔴 Do not call Hooks inside conditions or loops.
- 🔴 Do not call Hooks after a conditional `return` statement.
- 🔴 Do not call Hooks in event handlers.
- 🔴 Do not call Hooks in class components.
- 🔴 Do not call Hooks inside functions passed to `useMemo`, `useReducer`, or `useEffect`.

```tsx
function Bad({ cond }) {
  if (cond) {
    // 🔴 Bad: inside a condition (to fix, move it outside!)
    const theme = useContext(ThemeContext);
  }
  // ...
}

function Bad() {
  for (let i = 0; i < 10; i++) {
    // 🔴 Bad: inside a loop (to fix, move it outside!)
    const theme = useContext(ThemeContext);
  }
  // ...
}

function Bad({ cond }) {
  if (cond) {
    return;
  }
  // 🔴 Bad: after a conditional return (to fix, move it before the return!)
  const theme = useContext(ThemeContext);
  // ...
}

function Bad() {
  function handleClick() {
    // 🔴 Bad: inside an event handler (to fix, move it outside!)
    const theme = useContext(ThemeContext);
  }
  // ...
}

function Bad() {
  const style = useMemo(() => {
    // 🔴 Bad: inside useMemo (to fix, move it outside!)
    const theme = useContext(ThemeContext);
    return createStyle(theme);
  });
  // ...
}

class Bad extends React.Component {
  render() {
    // 🔴 Bad: inside a class component (to fix, write a function component instead of a class!)
    useEffect(() => {})
    // ...
  }
}
```