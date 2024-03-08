기본적으로 Next.js에는 접근성 문제를 조기에 발견하는 데 도움이 되는 `eslint-plugin-jsx-a11y` 플러그인이 존재한다.

예를 들어, `alt` 텍스트가 없는 이미지가 있는 경우, `aria-*` , `role` 속성을 잘못 사용하는 경우 등을 경고한다.

`next lint` 를 추가한다.

```tsx
// package.json
"scripts": {
    "build": "next build",
    "dev": "next dev",
    "seed": "node -r dotenv/config ./scripts/seed.js",
    "start": "next start",
    "lint": "next lint"
},
```

그런 다음 `npm run lint` 를 실행한다.

다음과 같은 경고가 표시된다.

`no ESLint warnings or errors`

만약 `alt` 텍스트 없이 이미지만 있다면?

```tsx
./app/ui/invoices/table.tsx
45:25  Warning: Image elements must have an alt prop,
either with meaningful text, or an empty string for decorative images. jsx-a11y/alt-text
```

위와 같은 경고가 표시된다.

Vercel에 애플리케이션을 배포하려고 할 때도 빌드 로그 경고가 표시되는데, `next lint` 가 빌드 프로세스의 일부로 실행되기 때문이다.

따라서 애플리케이션을 배포하기 전에 로컬로 `lint` 를 실행하여 접근성 문제를 파악해야 한다.

## aria 라벨

- `aria-describedby="customer-error"`
  요소와 오류 메시지 컨테이너 간의 관계를 설정한다. 이는 요소의 오류에 대한 설명을 `id="customer-error"` 요소가 설명함을 나타낸다.
  화면 판독기는 사용자가 해당 요소와 상호작용하여 오류를 알릴 때 이 설명을 읽는다.
- `id="customer-error"`
  이 id 속성은 입력에 대한 오류 메시지를 보유하는 HTML 요소를 고유하게 식별한다. `aria-describedby` 와의 관계를 확립하는 데 필요하다.
- `aria-live="polite"`
  스크린 리더는 내부 오류가 업데이트되면 정중하게 사용자에게 알려야 한다.
  콘텐츠가 변경되면 스크린 리더는 이러한 변경 사항을 사용자에게 알려주지만, 사용자의 서비스 사용을 방해하지 않도록 유휴 상태인 경우에만 해당된다.
