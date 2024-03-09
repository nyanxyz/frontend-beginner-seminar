# 12. Toy Project

강의 날짜: 2023년 8월 18일

### 1. create next-app

```tsx
yarn create next-app toy-snulife
```

- toy-snulife
- Typescript
- ESLint
- Pages router (No App router)
- No tailwind
- src

### 2. 초기 세팅

1. lint 설정
    1. prettier
    2. eslint
        1. [https://typescript-eslint.io/getting-started](https://typescript-eslint.io/getting-started)
        2. [https://eslint.org/docs/latest/rules/](https://eslint.org/docs/latest/rules/)
2. 사용할 스타일링 라이브러리
    - https://www.figma.com/file/2SvPMl3lsEAJ0kgJxqWK4a/%F0%9F%91%8B-System?type=design&node-id=298-605&mode=dev
    1. reset css
        1. [https://www.daleseo.com/css-normalize-reset/](https://www.daleseo.com/css-normalize-reset/)
        2. all: unset
    2. font family
        1. [https://spoqa.github.io/spoqa-han-sans/#webfont](https://spoqa.github.io/spoqa-han-sans/#webfont)
    3. chakra-ui
        1. [https://chakra-ui.com/getting-started](https://chakra-ui.com/getting-started)
3. 사용할 데이터 패칭 라이브러리
    1. axios
        1. [https://axios-http.com/kr/docs/intro](https://axios-http.com/kr/docs/intro)
    2. react-query
        1. [https://tanstack.com/query/v4/docs/react/installation](https://tanstack.com/query/v4/docs/react/installation)
4. 컨벤션 정하기

- **SLDS**
    
    colors.ts
    
    ```tsx
    export const colors = {
      White: '#ffffff',
      Grey0: '#f8f9fa',
      Grey1: '#f1f3f5',
      Grey2: '#e9edf0',
      Grey3: '#e3e7eb',
      Grey4: '#ced4da',
      Grey5: '#adb5bd',
      Grey6: '#868e96',
      Grey7: '#495057',
      Grey8: '#343a40',
      Grey9: '#212529',
      SLBlue: '#03b8f1',
    };
    ```
    
    Button.tsx
    
    ```tsx
    import { colors } from '@/constants/colors';
    import styled from '@emotion/styled';
    import { ComponentProps } from 'react';
    import { Spinner } from './Spinner';
    
    type ButtonProps = ComponentProps<'button'> & {
      loading?: boolean;
    };
    
    export function Button({ children, loading = false, disabled = false, ...props }: ButtonProps) {
      return (
        <SldsButton disabled={disabled || loading} {...props}>
          {loading ? <Spinner size={24} /> : children}
        </SldsButton>
      );
    }
    
    const SldsButton = styled.button`
      width: 100%;
      height: 50px;
      border-radius: 6px;
      background: ${colors.SLBlue};
      font-size: 16px;
      font-style: normal;
      font-weight: 700;
      color: ${colors.White};
    
      &:disabled {
        background: ${colors.Grey3};
      }
    `;
    ```
    
    Icon.tsx
    
    ```tsx
    type SquareIconProps = {
      size: number;
    };
    type RectIconProps = {
      width: number;
      height: number;
    };
    type IconSizeProps = SquareIconProps | RectIconProps;
    
    type IconProps = IconSizeProps & {
      name: string;
    };
    
    export function Icon({ name, ...props }: IconProps) {
      const src = `/icons/${name}.svg`;
    
      if ('size' in props) {
        return <img src={src} width={props.size} height={props.size} alt="" />;
      }
    
      return <img src={src} width={props.width} height={props.height} alt="" />;
    }
    ```
    
    Input.tsx
    
    ```tsx
    import { colors } from '@/constants/colors';
    import styled from '@emotion/styled';
    import { ComponentProps } from 'react';
    
    type InputProps = ComponentProps<'input'>;
    
    export function Input(props: InputProps) {
      return <SldsInput {...props} />;
    }
    
    const SldsInput = styled.input`
      border-radius: 6px;
      border: 1px solid ${colors.Grey2};
      background: ${colors.Grey0};
      width: 100%;
      padding: 15px 16px;
      font-size: 14px;
      color: ${colors.Grey8};
      &::placeholder {
        color: ${colors.Grey4};
      }
    `;
    ```
    
    Spinner.tsx
    
    ```tsx
    import { colors } from '@/constants/colors';
    import { css } from '@emotion/react';
    import styled from '@emotion/styled';
    import { HTMLAttributes } from 'react';
    
    interface SpinnerProps extends HTMLAttributes<HTMLDivElement> {
      trackThickness?: number;
      filledTrackColor?: string;
      trackColor?: string;
      size?: number;
    }
    
    export function Spinner({
      trackThickness = 4,
      trackColor = 'transparent',
      filledTrackColor = colors.White,
      size = 24,
      ...rest
    }: SpinnerProps) {
      const boxSize = size + trackThickness;
    
      return (
        <SpinnerRoot size={size} {...rest}>
          <svg
            height={boxSize}
            width={boxSize}
            viewBox={`0 0 ${boxSize} ${boxSize}`}
          >
            <LoaderSvg
              cx={boxSize / 2}
              cy={boxSize / 2}
              r={size / 2}
              style={{
                strokeWidth: `${trackThickness}px`,
                stroke: trackColor,
              }}
            />
            <LoaderSvg
              cx={boxSize / 2}
              cy={boxSize / 2}
              r={size / 2}
              animate={true}
              style={{
                strokeWidth: `${trackThickness}px`,
                stroke: filledTrackColor,
              }}
            />
          </svg>
        </SpinnerRoot>
      );
    }
    
    const SpinnerRoot = styled.div<{ size: number }>`
      display: flex;
      align-content: center;
      justify-content: center;
      position: relative;
    
      ${({ size }) => css`
        @keyframes fill-animation {
          0% {
            stroke-dasharray: ${size * 3.14 * 0.25} ${size * 3.14 * 0.75};
            stroke-dashoffset: 0;
          }
          50% {
            stroke-dasharray: ${size * 3.14 * 0.5};
            stroke-dashoffset: ${size * 3.14 * 0.5};
          }
          100% {
            stroke-dasharray: ${size * 3.14 * 0.25} ${size * 3.14 * 0.75};
            stroke-dashoffset: ${size * 3.14};
          }
        }
      `}
    `;
    
    const LoaderSvg = styled.circle<{ animate?: boolean }>`
      position: absolute;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      fill: none;
      stroke-linecap: round;
    
      ${({ animate }) =>
        animate &&
        css`
          animation: fill-animation 1.1s cubic-bezier(1, 1, 1, 1) 0s infinite;
        `}
    `;
    ```
    

### 3. 로그인 화면 제작

[https://www.figma.com/file/wu3rhPOSP6p5vX7c5neUdE/%F0%9F%91%8B-Community-(PC%2FMobile)?type=design&node-id=17-2724&mode=dev](https://www.figma.com/file/wu3rhPOSP6p5vX7c5neUdE/%F0%9F%91%8B-Community-(PC%2FMobile)?type=design&node-id=17-2724&mode=dev)

```tsx
### login
POST {{host}}/auth/login/
Content-Type: application/json

{
  "username": "{{username}}",
  "password": "{{password}}"
}
```

### 4. 게시물 조회 화면 제작

1. 게시물 리스트 - 8/29 (화)
2. 게시물 상세

```tsx
### 익게 목록 읽기
GET {{host}}/boards/free/posts/

### post detail가져오기 - free부분에 path
### {{host}}/boards/{board_path}/posts/{post_id}/
GET {{host}}/boards/free/posts/1/
```

### 5. 게시물 작성 화면 제작

### 6. 게시물 수정 화면 제작

### Git

main에서 새로운 브랜치 파기

```tsx
git checkout -b board
```

작업 후 커밋하기

```tsx
git add .
git commit -m "commit message"
```

push하기

```tsx
git push -u origin [branch name]
```

PR 날리기

- Reviewer로 냔지 지정