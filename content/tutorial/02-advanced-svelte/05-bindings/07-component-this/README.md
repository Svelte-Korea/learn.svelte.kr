---
title: 컴포넌트 인스턴스에 대한 바인딩
---

DOM 요소에 바인딩할 수 있는 것처럼, `bind:this`를 사용하여 컴포넌트 인스턴스 자체에 바인딩할 수 있습니다.

이는 컴포넌트에 업데이트된 프롭(props)을 제공하는 대신 프로그램적으로 상호 작용해야 하는 드문 경우에 유용합니다. [몇 가지 연습 전](actions)의 캔버스 앱을 다시 살펴보면, 화면을 지우는 버튼을 추가하면 좋을 것입니다.

먼저, `Canvas.svelte`에서 함수를 내보냅시다.

```svelte
/// file: Canvas.svelte
export let color;
export let size;

+++export function clear() {
	context.clearRect(0, 0, canvas.width, canvas.height);
}+++
```

그런 다음, 컴포넌트 인스턴스에 대한 참조를 만듭시다.

```svelte
/// file: App.svelte
<script>
	import Canvas from './Canvas.svelte';
	import { trapFocus } from './actions.js';

	const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet', 'white', 'black'];
	let selected = colors[0];
	let size = 10;

	let showMenu = true;
	+++let canvas;+++
</script>

<div class="container">
	<Canvas +++bind:this={canvas}+++ color={selected} size={size} />
```

마지막으로, `clear` 함수를 호출하는 버튼을 추가합시다.

```svelte
/// file: App.svelte
<div class="controls">
	<button class="show-menu" on:click={() => showMenu = !showMenu}>
		{showMenu ? 'close' : 'menu'}
	</button>

+++	<button on:click={() => canvas.clear()}>
		clear
	</button>+++
</div>
```
