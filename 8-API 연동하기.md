# 8. API 연동하기

강의 날짜: 2023년 7월 18일 → 2023년 7월 25일

## API란?

application programming interface

## 서버-클라이언트 모델

## REST API

## API Call

1. `fetch`
2. `axios`

## Axios를 이용한 API 연동

```jsx
yarn create next-app api-practice
yarn add axios
```

```jsx
axios.get('https://jsonplaceholder.typicode.com/users')
axios.get('https://jsonplaceholder.typicode.com/users/1')
```

## React-Query를 이용한 서버 상태 관리

[https://tanstack.com/query/v4/docs/react/overview](https://tanstack.com/query/v4/docs/react/overview)

- 서버 상태는 사용자의 제어를 벗어난 위치에서 원격으로 유지된다.
- 비동기 요청을 통해 `fetching` 또는 `updating`이 가능하다.
- 소유권을 공유한다. 즉 사용자 모르게 다른 사용자가 변경할 수 있다.
- 시간이 지남에 따라 `stale` 또는 `outdated`된다.

```tsx
import "@/styles/globals.css";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import type { AppProps } from "next/app";

const queryClient = new QueryClient();

export default function App({ Component, pageProps }: AppProps) {
  return (
    <QueryClientProvider client={queryClient}>
      <Component {...pageProps} />
    </QueryClientProvider>
  );
}
```

```tsx
const queryClient = new QueryClient();

export default function App({ Component, pageProps }: AppProps) {
  return (
    <QueryClientProvider client={queryClient}>
      <Component {...pageProps} />
    </QueryClientProvider>
  );
}
```

### useQuery (GET)

```jsx
const { data: users, error, isSuccess, isError, isLoading } = useQuery(['users'], getUsers);
const { data: users } = useQuery(['users', 1], getUsers);
```

### useMutation (POST, DELETE, PUT)

마땅한 API가 없어서 예시코드는 생략…

```jsx
const { mutate: likePost } = useMutation({
	mutationFn: rLikePost,
	onMutate: () => {
		...
		// like 상태가 되도록 state를 바꿈
	},
	onSuccess: () => {
		...
		// 그냥 냅둠
	},
	onError: () => {
		...
		// 원래대로 돌림
	}
}
```