---
title: 리다이렉트
---

`throw` 메커니즘을 이용해 다른 페이지로 리다이렉트 시킬수 있습니다.

`src/routes/a/+page.server.js`에 새 `load` 함수를 만들어 봅시다.

```js
/// file: src/routes/a/+page.server.js
import { redirect } from '@sveltejs/kit';

export function load() {
	throw redirect(307, '/b');
}
```

`/a` 로 이동하면 `/b` 로 이동하게 됩니다.

`load` 함수, 폼 액션, API 라우트, `handle` 훅(나중에 다룰 내용입니다.)에서 `throw redirect(...)` 를 사용할 수 있습니다.

가장 흔하게 사용되는 리다이렉트는 다음과 같습니다.

- `303` — 폼 액션에서 성공적인 제출 다음에 사용.
- `307` — 임시적인 리다이렉트
- `308` — 영구적인 리다이렉트
