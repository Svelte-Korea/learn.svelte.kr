---
title: <svelte:component>
---

컴포넌트는 `<svelte:component>`를 사용하여 유형을 완전히 변경할 수 있습니다. 이 연습에서는 `color`가 `red`인 경우 `RedThing.svelte`, `green`인 경우 `GreenThing.svelte` 하는 식으로 표시하고자 합니다.

이것을 일련의 `if` 블록으로 할 수 _있지만_...

```svelte
/// file: App.svelte
{#if selected.color === 'red'}
	<RedThing/>
{:else if selected.color === 'green'}
	<GreenThing/>
{:else if selected.color === 'blue'}
	<BlueThing/>
{/if}
```

...이는 다소 번거롭습니다. 대신, 단일 동적 컴포넌트를 생성할 수 있습니다.

```svelte
/// file: App.svelte
<select bind:value={selected}>
	{#each options as option}
		<option value={option}>{option.color}</option>
	{/each}
</select>

+++<svelte:component this={selected.component} />+++
```

`this` 값은 어떤 컴포넌트 생성자나 거짓(falsy) 값일 수 있습니다. 거짓 값이면, 아무 컴포넌트도 렌더링되지 않습니다.
