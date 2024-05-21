---
title: 타당성 검증
---

사용자들은 기회만 되면 온갖 말도 안 되는 데이터를 제출합니다. 혼란을 방지하려면 폼 데이터를 검증하는 것이 중요합니다.

첫 번째 방어선은 브라우저의 [내장 폼 검증](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation#using_built-in_form_validation)으로, `<input>`을 필수 항목으로 표시하는 등의 일을 쉽게 만들어 줍니다.

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/create">
	<label>
		add a todo
		<input
			name="description"
			autocomplete="off"
			+++required+++
		/>
	</label>
</form>
```

`<input>`이 비어 있을 때 엔터 키를 눌러보세요.

이러한 종류의 검증은 유용하지만 충분하지 않습니다. 유일성과 같은 일부 검증 규칙은 `<input>` 속성을 사용하여 표현할 수 없으며, 어떤 경우에는 사용자가 브라우저의 개발자 도구를 사용하여 속성을 삭제할 수 있습니다. 이러한 문제를 방지하기 위해 항상 서버 측 검증을 사용해야 합니다.

`src/lib/server/database.js`에서 설명이 존재하고 유일한지 검증해 봅시다.

```js
/// file: src/lib/server/database.js
export function createTodo(userid, description) {
+++	if (description === '') {
		throw new Error('todo must have a description');
	}+++

	const todos = db.get(userid);

+++	if (todos.find((todo) => todo.description === description)) {
		throw new Error('todos must be unique');
	}+++

	todos.push({
		id: crypto.randomUUID(),
		description,
		done: false
	});
}
```

중복된 todo를 제출해 보세요. 이런! 스벨트킷이 불친절한 에러 페이지를 보여주네요. 서버에서는 'todos must be unique' 오류를 확인할 수 있지만, 스벨트킷은 예상 밖의 오류 메시지가 종종 민감한 데이터를 포함하고 있기 때문에 사용자에게 숨깁니다.

사용자가 문제를 수정할 수 있도록 같은 페이지에 머물며 무엇이 잘못되었는지 표시하는 게 훨씬 낫겠죠. `fail` 함수를 사용하면 이를 위해 액션에서 데이터를 적절한 HTTP 상태 코드와 함께 반환할 수 있습니다.

```js
/// file: src/routes/+page.server.js
+++import { fail } from '@sveltejs/kit';+++
import * as db from '$lib/server/database.js';

export function load({ cookies }) {...}

export const actions = {
	create: async ({ cookies, request }) => {
		const data = await request.formData();

+++		try {+++
			db.createTodo(cookies.get('userid'), data.get('description'));
+++		} catch (error) {
			return fail(422, {
				description: data.get('description'),
				error: error.message
			});
		}+++
	}
}
```

`src/routes/+page.svelte`에서 폼 제출 후에만 채워지는 `form` 프롭을 통해 반환된 값에 접근할 수 있습니다.

```svelte
/// file: src/routes/+page.svelte
<script>
	export let data;
	+++export let form;+++
</script>

<div class="centered">
	<h1>todos</h1>
	
	+++{#if form?.error}
		<p class="error">{form.error}</p>
	{/if}+++
	
	<form method="POST" action="?/create">
		<label>
			add a todo:
			<input
				name="description"
				+++value={form?.description ?? ''}+++
				autocomplete="off"
				required
			/>
		</label>
	</form>
</div>
```

> `form` 프롭을 통해 데이터를 저장할 때 '성공!' 메시지를 표시하는 것과 같이 `fail`로 래핑하지 _않고도_ 액션에서 데이터를 반환할 수 있습니다.