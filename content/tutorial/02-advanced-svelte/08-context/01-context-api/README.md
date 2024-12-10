---
title: setContext와 getContext
---

컨텍스트 API는 데이터와 함수를 프롭(props)으로 전달하거나 많은 이벤트를 디스패치하지 않고도 컴포넌트 간의 '대화'를 가능하게 하는 메커니즘을 제공합니다. 이는 고급 기능이지만 유용한 기능입니다. 이 연습에서는 생성 예술의 선구자 중 한 명인 조지 니스(George Nees)의 [Schotter](https://collections.vam.ac.uk/item/O221321/schotter-print-nees-georg/)를 컨텍스트 API를 사용하여 재구성할 것입니다.

`Canvas.svelte` 내부에, 캔버스에 항목을 추가하는 `addItem` 함수가 있습니다. `setContext`를 사용하여 이를 `<Canvas>` 내부의 `<Square>`와 같은 컴포넌트에서 사용할 수 있도록 할 수 있습니다.

```svelte
/// file: Canvas.svelte
<script>
	import { +++setContext+++, afterUpdate, onMount, tick } from 'svelte';

	// ...

	onMount(() => {
		ctx = canvas.getContext('2d');
	});

+++	setContext('canvas', {
		addItem
	});+++

	function addItem(fn) {...}

	function draw() {...}
</script>
```

이제 자식 컴포넌트 내부에서 `getContext`를 사용하여 컨텍스트를 가져올 수 있습니다.

```svelte
/// file: Square.svelte
<script>
	+++import { getContext } from 'svelte';+++

	export let x;
	export let y;
	export let size;
	export let rotate;

	+++getContext('canvas').addItem(draw);+++

	function draw(ctx) {...}
</script>
```

지금까지는 흥미롭지 않습니다. 이제 그리드에 약간의 무작위성을 추가해 봅시다.

```svelte
/// file: App.svelte
<div class="container">
	<Canvas width={800} height={1200}>
		{#each Array(12) as _, c}
			{#each Array(22) as _, r}
				<Square
					x={180 + c * 40+++ + jitter(r * 2)+++}
					y={180 + r * 40+++ + jitter(r * 2)+++}
					size={40}
					+++rotate={jitter(r * 0.05)}+++
				/>
			{/each}
		{/each}
	</Canvas>
</div>
```

[lifecycle functions](/tutorial/onmount)과 마찬가지로, `setContext`와 `getContext`는 컴포넌트 초기화 중에 호출되어야 합니다. (컨텍스트 키(여기에서는 `'canvas'`)는 문자열이 아닌 것을 포함해 원하는 모든 것이 될 수 있으며, 이는 컨텍스트에 누가 접근할 수 있는지 제어하는 데 유용합니다.)

컨텍스트 객체는 스토어를 포함하여 무엇이든 포함할 수 있습니다. 이를 통해 시간에 따라 변경되는 값을 자식 컴포넌트에 전달할 수 있습니다.

```js
/// no-file
// 부모 컴포넌트에서
import { setContext } from 'svelte';
import { writable } from 'svelte/store';

setContext('my-context', {
	count: writable(0)
});
```

```js
/// no-file
// 자식 컴포넌트에서
import { getContext } from 'svelte';

const { count } = getContext('my-context');

$: console.log({ count: $count });
```
