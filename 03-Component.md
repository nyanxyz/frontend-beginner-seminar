# 3. Component

강의 날짜: 2023년 7월 4일

## 컴포넌트 생성하기

[https://react.dev/learn/your-first-component](https://react.dev/learn/your-first-component)

![Untitled](assets/Untitled%202.png)

```jsx
function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3As.jpg"
      alt="Katherine Johnson"
      width={100}
      height={100}
    />
  );
}
```

- 다른 파일에서 변수나 함수를 참조해 사용하려면 `export`와 `import`가 필요하다.

### `export` vs `export default`

…

## Props 전달하기

[https://react.dev/learn/passing-props-to-a-component](https://react.dev/learn/passing-props-to-a-component)

![Untitled](assets/Untitled%203.png)

```tsx
<div>
  <h1>Amazing scientists</h1>
  <Profile name="Katherine Johnson" />
  <Profile name="Dorothy Vaughan" />
  <Profile name="Mary Jackson" />
</div>
```

```tsx
type ProfileProps = {
  name: "Katherine Johnson" | "Dorothy Vaughan" | "Mary Jackson";
};

const sources = {
  "Katherine Johnson": "https://i.imgur.com/MK3eW3As.jpg",
  "Dorothy Vaughan": "https://i.imgur.com/3F28WN2.jpeg",
  "Mary Jackson": "https://i.imgur.com/kjGcFYg.jpeg",
};

export function Profile({ name }: ProfileProps) {
  return <img src={sources[name]} alt={name} width={100} height={100} />;
}
```

- 이름까지 표시하도록 바꾸려면?
- `<Component>hello</Component>` 와 같이 사용한 경우 hello는 어떻게 전달받지?

## 리스트 렌더링하기

[https://react.dev/learn/rendering-lists](https://react.dev/learn/rendering-lists)

```tsx
const scientistNames = ["Katherine Johnson", "Dorothy Vaughan", "Mary Jackson"];
```

```tsx
{scientistNames.map((name) => (
  <Profile key={name} name={name} />
))}
```