---
title: onMount
---

모든 컴포넌트는 생성될 때 시작되고 파괴될 때 끝나는 _생명주기_ 를 가집니다. 이 생명주기 동안 특정 순간에 코드를 실행할 수 있는 몇 가지 함수가 있습니다. 그 중 가장 자주 사용하게 될 것은 `onMount`로, 컴포넌트가 처음으로 DOM에 렌더링된 후에 실행됩니다.

이번 연습에는 `gradient.js`의 `paint` 함수를 사용하여 애니메이션을 하고 싶은 `<canvas>`가 있습니다. 먼저 `svelte`에서 `onMount` 함수를 가져옵시다.

```svelte
/// file: App.svelte
<script>
	+++import { onMount } from 'svelte';+++
	import { paint } from './gradient.js';
</script>
```

그런 다음, 컴포넌트가 마운트될 때 실행되는 콜백을 추가합니다:

```svelte
/// file: App.svelte
<script>
	import { onMount } from 'svelte';
	import { paint } from './gradient.js';

+++	onMount(() => {
		const canvas = document.querySelector('canvas');
		const context = canvas.getContext('2d');+++

+++		requestAnimationFrame(function loop(t) {
			requestAnimationFrame(loop);
			paint(context, t);
		});
	});+++
</script>
```

> [나중의 연습](bind-this)에서 `document.querySelector`를 사용하지 않고 요소 참조를 얻는 방법을 배울 것입니다.

지금까지는 순조롭게 진행되었습니다. 스벨트 로고 모양으로 부드럽게 움직이는 색상을 볼 수 있을 것입니다. 하지만 하나의 문제가 있는데, 컴포넌트가 파괴된 후에도 루프가 계속됩니다. 이를 해결하려면, `onMount`에서 정리 함수를 반환해야 합니다.

```js
/// file: App.svelte
onMount(() => {
	const canvas = document.querySelector('canvas')
	const context = canvas.getContext('2d');

	+++let frame =+++ requestAnimationFrame(function loop(t) {
		+++frame =+++ requestAnimationFrame(loop);
		paint(context, t);
	});

+++	return () => {
		cancelAnimationFrame(frame);
	};+++
});
```
