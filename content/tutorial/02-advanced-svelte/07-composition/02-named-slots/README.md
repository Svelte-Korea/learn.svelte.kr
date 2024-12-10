---
title: 명명된 슬롯(named slots)
---

이전 예제에는 컴포넌트의 직계 자식을 렌더링하는 _기본 슬롯_ 이 포함되어 있었습니다. 때로는 배치에 대한 더 많은 제어가 필요할 수 있습니다. 그런 경우에는 _명명된 슬롯_ 을 사용할 수 있습니다.

`App.svelte` 내부에서, `<span slot="telephone">`와 `company` 및 `address`에 대한 다른 슬롯을 포함한 `<Card>` 컴포넌트를 렌더링하고 있습니다. `Card.svelte`에 상응하는 명명된 슬롯을 추가해 봅시다.

\```svelte
/// file: Card.svelte
<div class="card">
+++	<header>
		<slot name="telephone" />
		<slot name="company" />
	</header>+++

	<slot />
		
+++	<footer>
		<slot name="address" />
	</footer>+++
</div>
\```

`App.svelte`의 `<small>` 요소에 스타일을 추가하여 해당 요소가 자체 줄을 차지하도록 해야 합니다. `<Card>`의 내용은 `font-family`(서체는 ['Silian Rail'](https://www.youtube.com/watch?v=aZVkW9p-cCU))와 같은 `Card.svelte`의 스타일을 상속받지만, 일반적인 범위 규칙이 적용되므로, 스타일을 추가하려면 해당 요소가 있는 `App.svelte`에 추가해야 합니다.

```svelte
/// file: App.svelte
<style>
	main {
		display: grid;
		place-items: center;
		height: 100%;
		background: url(./wood.svg);
	}

+++	small {
		display: block;
		font-size: 0.6em;
		text-align: right;
	}+++
</style>
```

또는, `:global` 수정자를 `Card.svelte` 내에서 사용하여 `.card` 내부의 모든 `small` 요소를 타겟팅할 수도 있습니다:

```svelte
/// file: Card.svelte
<style>
	/* ... */ 

	+++.card :global(small) {
		display: block;
		font-size: 0.6em;
		text-align: right;
	}+++
</style>
```
