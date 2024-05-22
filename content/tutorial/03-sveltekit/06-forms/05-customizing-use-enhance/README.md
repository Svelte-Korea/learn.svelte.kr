---
title: use:enhance 사용자 정의하기
---

`use:enhance`를 사용하여 그저 브라우저의 기본 동작을 에뮬레이션하는 것보다 더 나아갈 수 있습니다. 콜백을 제공함으로써 **대기 상태** 및 **옵티미스틱 UI**와 같은 기능을 추가할 수 있습니다. 두 액션에 인위적인 지연을 추가하여 느린 네트워크를 시뮬레이션해 봅시다.

```js
/// file: src/routes/+page.server.js
export const actions = {
	create: async ({ cookies, request }) => {
		+++await new Promise((fulfil) => setTimeout(fulfil, 1000));+++
		...
	},

	delete: async ({ cookies, request }) => {
		+++await new Promise((fulfil) => setTimeout(fulfil, 1000));+++
		...
	}
};
```

항목을 생성하거나 삭제할 때, UI가 업데이트되기까지 1초가 걸리므로 사용자가 혼란스러워할 수 있습니다. 이를 해결하기 위해 로컬 상태를 추가합시다.

```svelte
/// file: src/routes/+page.svelte
<script>
	import { fly, slide } from 'svelte/transition';
	import { enhance } from '$app/forms';

	export let data;
	export let form;

+++	let creating = false;
	let deleting = [];+++
</script>
```

그리고 첫 번째 `use:enhance` 안에서 `creating`을 토글합시다.

```svelte
/// file: src/routes/+page.svelte
<form
	method="POST"
	action="?/create"
+++	use:enhance={() => {
		creating = true;

		return async ({ update }) => {
			await update();
			creating = false;
		};
	}}+++
>
	<label>
		add a todo:
		<input
			+++disabled={creating}+++
			name="description"
			value={form?.description ?? ''}
			autocomplete="off"
			required
		/>
	</label>
</form>
```

그러고 나면 데이터를 저장하는 동안 메시지를 표시할 수 있습니다.

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	<!-- ... -->
</ul>

+++{#if creating}
	<span class="saving">saving...</span>
{/if}+++
```

삭제의 경우, 서버가 무언가를 검증하기를 기다릴 필요가 없이 바로 UI를 업데이트할 수 있습니다.

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	{#each +++data.todos.filter((todo) => !deleting.includes(todo.id))+++ as todo (todo.id)}
		<li in:fly={{ y: 20 }} out:slide>
			<form
				method="POST"
				action="?/delete"
				+++use:enhance={() => {
					deleting = [...deleting, todo.id];
					return async ({ update }) => {
						await update();
						deleting = deleting.filter((id) => id !== todo.id);
					};
				}}+++
			>
				<input type="hidden" name="id" value={todo.id} />
				<button aria-label="Mark as complete">✔</button>

				{todo.description}
			</form>
		</li>
	{/each}
</ul>
```

> `use:enhance`는 아주 다양하게 사용 가능합니다. 제출을 `cancel()`하거나, 리디렉션을 처리하고, 폼의 리셋 여부를 제어하는 등의 작업을 할 수 있습니다. [문서](https://kit.svelte.dev/docs/modules#$app-forms-enhance)에서 자세한 내용을 확인하세요.
