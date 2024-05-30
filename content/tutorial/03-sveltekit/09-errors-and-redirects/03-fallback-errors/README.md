---
title: 에러 폴백
---

루트 레이아웃 데이터를 불러오는 과정에 발생한 에러와 에러 페이지를 불러오는 중에 에러가 발생하는 것처럼 진짜 심각한 일이 일어난다면, 스벨트킷은 정적인 에러 페이지를 띄워 대응(폴백, fall back)합니다.

이러한 액션을 일으키기 위해 `src/routes/+layout.server.js` 파일을 만들어 봅시다.

```js
/// file: src/routes/+layout.server.js
export function load() {
	throw new Error('yikes');
}
```

폴백 에러 페이지를 수정해봅시다. `src/error.html` 파일을 만드세요.

```html
/// file: src/error.html
<h1>Game over</h1>
<p>Code %sveltekit.status%</p>
<p>%sveltekit.error.message%</p>
```

이 파일에는 다음 정보가 담길 수 있습니다.

- `%sveltekit.status%` — HTTP 상태코드
- `%sveltekit.error.message%` — 에러 메시지