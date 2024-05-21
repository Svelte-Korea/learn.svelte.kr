---
title: This
---

[이전 연습](onmount)에서 `onMount` 생명주기 함수를 사용하여 캔버스에 그림을 그리는 방법을 배웠습니다.

하지만 이 예제에는 버그가 있습니다 — `document.querySelector('canvas')`를 사용하고 있어, 항상 페이지에서 첫 번째 `<canvas>` 요소를 반환하게 되며, 이는 우리 컴포넌트에 속한 것이 아닐 수 있습니다.

대신, 읽기 전용 `this` 바인딩을 사용하여 요소에 대한 참조를 얻을 수 있습니다.

```js
/// file: App.svelte
+++let canvas;+++

onMount(() => {
	---const canvas = document.querySelector('canvas')---
	const context = canvas.getContext('2d');

	let frame = requestAnimationFrame(function loop(t) {
		frame = requestAnimationFrame(loop);
		paint(context, t);
	});

	return () => {
		cancelAnimationFrame(frame);
	};
});
```

```svelte
/// file: App.svelte
<canvas
	+++bind:this={canvas}+++
	width={32}
	height={32}
></canvas>
```

캔버스의 값은 컴포넌트가 마운트될 때까지 `undefined`임에 유의하세요.
