---
title: 이벤트 전달
---

DOM 이벤트와 달리, 컴포넌트 이벤트는 _버블링_ 되지 않습니다. 깊게 중첩된 컴포넌트에서 이벤트를 듣고 싶다면, 중간 컴포넌트들이 이벤트를 _전달_ 해야 합니다.

이번 예제는 [이전 장](/tutorial/component-events)과 동일한 `App.svelte`와 `Inner.svelte`가 있지만, 이제 `<Inner/>`를 포함하는 `Outer.svelte` 컴포넌트가 있습니다.

이 문제를 해결하는 한 가지 방법은 `Outer.svelte`에 `createEventDispatcher`를 추가하여 `message` 이벤트를 듣고, 이를 처리할 핸들러를 만드는 것입니다.

```svelte
/// file: Outer.svelte
<script>
	import Inner from './Inner.svelte';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function forward(event) {
		dispatch('message', event.detail);
	}
</script>

<Inner on:message={forward}/>
```

하지만 이는 많은 코드를 작성해야 하므로, 스벨트는 이에 대한 간단한 방법을 제공합니다. 값이 없는 `on:message` 이벤트 지시어는 '모든 `message` 이벤트를 전달'한다는 의미입니다.

```svelte
/// file: Outer.svelte
<script>
	import Inner from './Inner.svelte';
</script>

<Inner +++on:message+++/>
```
