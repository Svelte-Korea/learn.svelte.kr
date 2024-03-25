---
title: GET 핸들러
---

스벨트킷을 이용하면 페이지를 만드는 것 말고도, _API_ _라우트_ 를 만들 수 있습니다. HTTP 메소드(`GET`, `PUT`, `POST`, `PATCH` 와 `DELETE`)에 대응하는 함수를 내보내는 `+server.js` 파일을 만들면 됩니다.
이 앱은 버튼이 클릭되면 `/roll` API 라우트에서 데이터를 가져옵니다. `src/routes/roll/+sever.js` 파일을 만들어서 라우트를 만듭시다.

```js
/// file: src/routes/roll/+server.js
export function GET() {
	const number = Math.floor(Math.random() * 6) + 1;

	return new Response(number, {
		headers: {
			'Content-Type': 'application/json'
		}
	});
}
```

이제 버튼을 클릭하면 잘 작동합니다.

리퀘스트 핸들러는 반드시 [리스폰스(Response)](https://developer.mozilla.org/en-US/docs/Web/API/Response/Response) 객체를 반환해야합니다. API 라우트에선 JSON을 반환하는 것이 흔한데, 스벨트킷에서 제공하는 함수를 사용하면 편하게 그런 리스폰스를 만들 수 있습니다.

```js
/// file: src/routes/roll/+server.js
+++import { json } from '@sveltejs/kit';+++

export function GET() {
	const number = Math.floor(Math.random() * 6) + 1;

---	return new Response(number, {
		headers: {
			'Content-Type': 'application/json'
		}
	});---
+++	return json(number);+++
}
```
