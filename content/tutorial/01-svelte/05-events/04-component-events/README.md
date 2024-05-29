---
title: 컴포넌트 이벤트
---

컴포넌트는 이벤트를 보낼 수도 있습니다. 이를 위해 이벤트 디스패처를 생성해야 합니다. `Inner.svelte`를 업데이트해봅시다.

```svelte
/// file: Inner.svelte
<script>
	+++import { createEventDispatcher } from 'svelte';+++

	+++const dispatch = createEventDispatcher();+++

	function sayHello() {
		dispatch('message', {
			text: 'Hello!'
		});
	}
</script>
```

> `createEventDispatcher`는 컴포넌트가 처음 인스턴스화될 때 호출되어야 합니다. `setTimeout` 콜백 내에서 나중에 호출할 수 없습니다. 이렇게 하면 `dispatch`가 컴포넌트 인스턴스에 연결됩니다.

그런 다음, `App.svelte`에서 `on:message` 핸들러를 추가합시다.

```svelte
/// file: App.svelte
<Inner +++on:message={handleMessage}+++ />
```

> 이벤트 이름을 다른 것으로 변경해 볼 수도 있습니다. `Inner.svelte`에서 `dispatch('message', {...})`를 `dispatch('greet', {...})`로 변경하고 `App.svelte`에서 속성 이름을 `on:message`에서 `on:greet`로 변경해 봅시다.
