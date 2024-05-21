---
title: 리디렉트
---

`throw` 메커니즘을 사용하여 한 페이지에서 다른 페이지로 리디렉션할 수도 있습니다.

`src/routes/a/+page.server.js`에 새로운 `load` 함수를 생성합시다.

```js
/// file: src/routes/a/+page.server.js
import { redirect } from '@sveltejs/kit';

export function load() {
	throw redirect(307, '/b');
}
```

이제 `/a`로 이동하면 바로 `/b`로 리디렉션됩니다.

`throw redirect(...)`는 `load` 함수, 폼 액션, API 라우트 및 `handle` 훅 내에서 사용할 수 있으며, 이에 대해서는 이후 장에서 논의할 것입니다.

가장 일반적으로 사용되는 상태 코드는 다음과 같습니다.

- `303` — 폼 액션의 경우, 성공적인 제출 후
- `307` — 임시 리디렉션
- `308` — 영구 리디렉션
