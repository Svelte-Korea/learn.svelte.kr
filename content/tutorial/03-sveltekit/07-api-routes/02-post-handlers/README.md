---
title: POST 핸들러.
---

데이터를 변경하기 위한 `POST` 와 같은 요청들도 처리할 수 있습니다. 대부분의 경우엔 [폼 액션](the-form-element)를 대신 사용하는 것이 더 편합니다. 코드도 더 짧고, 자바스크립트 없이도 작동하며, 더 유연하기(resilient) 때문입니다.

`<input>` 안에 있는 '할일 추가' `keydown` 이벤트 핸들러에서, 서버로 데이터를 포스트 해봅시다.

```svelte
/// file: src/routes/+page.svelte
<input
	type="text"
	autocomplete="off"
	on:keydown={async (e) => {
		if (e.key !== 'Enter') return;

		const input = e.currentTarget;
		const description = input.value;

+++		const response = await fetch('/todo', {
			method: 'POST',
			body: JSON.stringify({ description }),
			headers: {
				'Content-Type': 'application/json'
			}
		});+++

		input.value = '';
	}}
/>
```

이제 JSON을 `/todo` API 라우트로 포스트 해봅시다. 쿠키에 있는 `userid` 값을 보내고, 응답 안에 새 할 일의 `id` 를 받아봅시다.

`src/routes/todo/+server.js` 파일에 `src/lib/server/database.js`에 있는 `createTodo`를 호출하는 `POST` 핸들러를 만들어 봅시다.

```js
/// file: src/routes/todo/+server.js
import { json } from '@sveltejs/kit';
import * as database from '$lib/server/database.js';

export async function POST({ request, cookies }) {
	const { description } = await request.json();

	const userid = cookies.get('userid');
	const { id } = await database.createTodo({ userid, description });

	return json({ id }, { status: 201 });
}
```

`load` 함수와 폼 액션과 마찬가지로, `request`는 표준 `[리퀘스트Request](https://developer.mozilla.org/en-US/docs/Web/API/Request)` 객체입니다. `await request.json()`는 이벤트 핸들러로 포스트 된 데이터를 반환합니다.

 데이터베이스에 새롭게 생긴 할 일의 `id` 를 [201 Created](https://http.dog/201) 상태 코드로 반환하고 있습니다. 이벤트 핸들러에서 이 값을 이용해 페이지를 업데이트 해도록 바꿔 봅시다.
```svelte
/// file: src/routes/+page.svelte
<input
	type="text"
	autocomplete="off"
	on:keydown={async (e) => {
		if (e.key !== 'Enter') return;

		const input = e.currentTarget;
		const description = input.value;

		const response = await fetch('/todo', {
			method: 'POST',
			body: JSON.stringify({ description }),
			headers: {
				'Content-Type': 'application/json'
			}
		});

+++		const { id } = await response.json();

		data.todos = [...data.todos, {
			id,
			description
		}];+++

		input.value = '';
	}}
/>
```

> 페이지를 다시 로드해도 같은 결과를 얻을 수 있도록 `data`를 변경해야 합니다.
