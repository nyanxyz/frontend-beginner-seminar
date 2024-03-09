# 6. TODO 리스트 만들기

강의 날짜: 2023년 7월 11일

```bash
git clone https://github.com/snulife/todolist
cd todolist
yarn
yarn dev
```

## TodoItem 컴포넌트 작성과 배열 렌더링하기

## Controlled vs Uncontrolled

- Controlled: state에 의해 제어되는 Component
    - 입력값이 변경될 때마다 state를 업데이트하고,
    - 이는 Component의 렌더링을 트리거
- Uncontrolled: ref를 사용하여 입력값을 얻는다.
    - state에 의해 제어되지 않는다.

### Uncontrolled - 거의 안 쓴다.

```tsx
const ref = useRef<HTMLInputElement>(null);

<input ref={ref} />

console.log(ref.current?.value)
```

### Controlled

```tsx
const [value, setValue] = useState<string>('');

<input value={value} onChange={(e) => setValue(e.target.value)} />

console.log(value)
```

## TodoItems를 관리하는 array state 만들기

## `+` button 작동시키기

## Extra mile: 각 아이템에 고유한 id 부여하기

## Extra mile: 삭제 버튼 만들기

## Super Extra mile: Done 기능

- Done을 표시할 수 있는 기능을 추가하고,
- Done Todo가 아래에 위치하게 정렬하기

## Homework

- 아래에 남은 태스크의 개수 표시와 clear all 버튼 만들기
    
    ![Untitled](assets/Untitled%209.png)
    
- 아무것도 입력되지 않은 상태에서 + button의 불투명도를 낮추고 disabled로 만들기
    
    ![Untitled](assets/Untitled%2010.png)
    

## 참고

- [https://tailwindcss.com/](https://tailwindcss.com/)
- [3. CSS](https://www.notion.so/3-CSS-120b8fc76feb471aae8b4118c8ae7f6b?pvs=21)
- [인터랙티브 웹 구현해보자!](https://www.notion.so/e542b0bfdeb44ee3b409d0bafebad8c4?pvs=21)
- answer 브랜치에 구현된 코드 참고 가능