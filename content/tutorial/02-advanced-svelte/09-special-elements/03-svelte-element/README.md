---
title: <svelte:element>
---

마찬가지로, 어떤 종류의 DOM 요소를 렌더링할지 미리 알 수 없는 경우도 있습니다. 이럴 때 `<svelte:element>`가 유용합니다. [이전 연습](svelte-component)과 마찬가지로, 긴 `if` 블록 시퀀스를 단일 동적 요소로 대체할 수 있습니다.

```svelte
/// file: App.svelte
<select bind:value={selected}>
	{#each options as option}
		<option value={option}>{option}</option>
	{/each}
</select>

+++<svelte:element this={selected}>
	I'm a <code>&lt;{selected}&gt;</code> element
</svelte:element>+++
```

`this` 값은 어떤 문자열이거나 거짓(falsy) 값일 수 있습니다. 거짓 값이면, 아무 요소도 렌더링되지 않습니다.
