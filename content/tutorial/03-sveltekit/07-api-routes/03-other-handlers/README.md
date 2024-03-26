---
title: 기타 핸들러
---

다른 HTTP 메쏘드에 대해서도 비슷하게 핸들러를 만들 수 있습니다. `src/lib/server/database.js`에 있는 `toggleTodo` 와 `deleteTodo` 를 이용해 할 일을 껐다 켜도록 `PUT` 과 `DELETE` 핸들러를 `src/routes/todo/[id]/+server.js`에 만들어, `/todo/[id]` 라우트를 추가합시다.

```js
/// file: src/routes/todo/[id]/+server.js
import * as database from '$lib/server/database.js';

export async function PUT({ params, request, cookies }) {
	const { done } = await request.json();
	const userid = cookies.get('userid');

	await database.toggleTodo({ userid, id: params.id, done });
	return new Response(null, { status: 204 });
}

export async function DELETE({ params, cookies }) {
	const userid = cookies.get('userid');

	await database.deleteTodo({ userid, id: params.id });
	return new Response(null, { status: 204 });
}
```

브라우저에 실제 데이터를 반환하지 않으니, 비어있는 [리스폰스(response](https://developer.mozilla.org/en-US/docs/Web/API/Response)를 [204 No Content](https://http.dog/204) 상태코드로 반환하도록 합시다.

이벤트 핸들러를 이용해 이 엔드포인트와 상호작용해 봅시다.

```svelte
/// file: src/routes/+page.svelte
<label>
	<input
		type="checkbox"
		checked={todo.done}
		on:change={async (e) => {
			const done = e.currentTarget.checked;

+++			await fetch(`/todo/${todo.id}`, {
				method: 'PUT',
				body: JSON.stringify({ done }),
				headers: {
					'Content-Type': 'application/json'
				}
			});+++
		}}
	/>
	<span>{todo.description}</span>
	<button
		aria-label="Mark as complete"
		on:click={async (e) => {
+++			await fetch(`/todo/${todo.id}`, {
				method: 'DELETE'
			});

			data.todos = data.todos.filter((t) => t !== todo);+++
		}}
	/>
</label>
```
