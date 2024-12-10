---
title: Animate 지시어
---

[이전 장](/tutorial/deferred-transitions)에서는 요소가 하나의 할 일 목록에서 다른 목록으로 이동할 때 움직임의 환상을 만들기 위해 지연된 전환을 사용했습니다.

이 환상을 완성하려면 전환하지 _않는_ 요소에도 움직임을 적용해야 합니다. 이를 위해 `animate` 지시어를 사용합니다.

먼저, `flip` 함수(flip은 ['First, Last, Invert, Play'](https://aerotwist.com/blog/flip-your-animations/)의 약자입니다.)를 `svelte/animate`에서 `TodoList.svelte`로 가져옵시다.

```svelte
/// file: TodoList.svelte
<script>
	+++import { flip } from 'svelte/animate';+++
	import { send, receive } from './transition.js';

	export let store;
	export let done;
</script>
```

그런 다음 이를 `<li>` 요소에 추가합니다.

```svelte
/// file: TodoList.svelte
<li
	class:done
	in:receive={{ key: todo.id }}
	out:send={{ key: todo.id }}
	+++animate:flip+++
>
```

이 경우 움직임이 조금 느리므로 `duration` 매개변수를 추가할 수 있습니다.

```svelte
/// file: TodoList.svelte
<li
	class:done
	in:receive={{ key: todo.id }}
	out:send={{ key: todo.id }}
	animate:flip+++={{ duration: 200 }}+++
>
```

> `duration`은 `d => milliseconds` 함수일 수도 있으며, 여기서 `d`는 요소가 이동해야 하는 픽셀 수입니다.

모든 전환과 애니메이션이 JavaScript가 아닌 CSS로 적용되고 있으므로, 메인 스레드를 차단하지도, 차단되지도 않는다는 점에 유의하세요.
