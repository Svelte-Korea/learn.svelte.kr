---
title: Each 블록 바인딩
---

`each` 블록 내의 속성에 바인딩할 수도 있습니다.

```svelte
/// file: App.svelte
{#each todos as todo}
	<li class:done={todo.done}>
		<input
			type="checkbox"
			+++bind:+++checked={todo.done}
		/>

		<input
			type="text"
			placeholder="What needs to be done?"
			+++bind:+++value={todo.text}
		/>
	</li>
{/each}
```

> 이러한 `<input>` 요소와 상호 작용하면 배열이 변형된다는 점에 유의하세요. 불변 데이터를 선호하는 경우, 이러한 바인딩을 피하고 대신 이벤트 핸들러를 사용해야 합니다.
