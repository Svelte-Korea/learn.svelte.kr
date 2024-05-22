---
title: 명명된 폼 액션
---

하나의 액션만 있는 페이지는 실제로 매우 드뭅니다. 대부분의 경우 한 페이지에 여러 액션이 필요합니다. 이 앱은 todo를 만드는 것만으로는 충분하지 않습니다. 완료된 todo를 삭제해 봅시다.

`default` 액션을 명명된 `create` 및 `delete` 액션으로 교체하는 것부터 해봅시다.

```js
/// file: src/routes/+page.server.js
export const actions = {
	+++create+++: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}+++,+++

+++	delete: async ({ cookies, request }) => {
		const data = await request.formData();
		db.deleteTodo(cookies.get('userid'), data.get('id'));
	}+++
};
```

> Default 액션은 명명된 액션과 공존할 수 없습니다.

`<form>` 요소에는 `<a>` 요소의 `href` 속성과 유사한 선택적 `action` 속성이 있습니다. 기존 폼을 업데이트하여 새로운 `create` 액션을 가리키도록 해봅시다.

```svelte
/// file: src/routes/+page.svelte
<form method="POST" +++action="?/create"+++>
	<label>
		add a todo:
		<input
			name="description"
			autocomplete="off"
		/>
	</label>
</form>
```

> `action` 속성은 어떤 URL이든 될 수 있습니다. 액션이 다른 페이지에 정의되어 있다면 `/todos?/create`와 같은 URL이 될 수 있습니다. 액션이 _이_ 페이지에 있기 때문에, 경로명 생략이 가능하며, 따라서 `?` 문자가 앞에 붙습니다.

다음으로, 각 todo에 대해 고유하게 식별하는 숨겨진 `<input>`을 포함한 폼을 생성해 봅시다.

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	{#each data.todos as todo (todo.id)}
		<li>
+++			<form method="POST" action="?/delete">
				<input type="hidden" name="id" value={todo.id} />
				<span>{todo.description}</span>
				<button aria-label="Mark as complete" />
			</form>+++
		</li>
	{/each}
</ul>
```
