---
title: 폴백 오류
---

루트 레이아웃 데이터를 로드하는 동안, 또는 오류 페이지를 렌더링하는 동안 오류가 발생하는 등 문제가 _정말_ 심각해지면 스벨트킷은 정적 오류 페이지로 폴백(fall back)합니다.

확인하기 위해 새로운 `src/routes/+layout.server.js` 파일을 추가해 봅시다.

```js
/// file: src/routes/+layout.server.js
export function load() {
	throw new Error('yikes');
}
```

정적 오류 페이지를 사용자 정의할 수 있습니다. `src/error.html` 파일을 생성하세요.

```html
/// file: src/error.html
<h1>Game over</h1>
<p>Code %sveltekit.status%</p>
<p>%sveltekit.error.message%</p>
```

이 파일에는 다음 내용을 포함할 수 있습니다.

- `%sveltekit.status%` — HTTP 상태 코드
- `%sveltekit.error.message%` — 오류 메시지
