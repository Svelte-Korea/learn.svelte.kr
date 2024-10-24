---
title: 자동 구독
---

이전 예제의 앱은 작동하지만, 미묘한 버그가 있습니다. 스토어를 구독은 하지만 해지하지는 않습니다. 컴포넌트가 여러 번 인스턴스화되고 파괴되면 _메모리 누수_ 가 발생할 수 있습니다.

먼저 `App.svelte`에서 `unsubscribe`를 선언합시다.

```js
/// file: App.svelte
+++const unsubscribe =+++ count.subscribe((value) => {
	count_value = value;
});
```

> `subscribe` 메서드를 호출하면 `unsubscribe` 함수가 반환됩니다.

`unsubscribe`를 선언했지만, 여전히 `onDestroy` 생명주기 훅 등을 통해 호출해야 합니다.

```svelte
/// file: App.svelte
<script>
	+++import { onDestroy } from 'svelte';+++
	import { count } from './stores.js';
	import Incrementer from './Incrementer.svelte';
	import Decrementer from './Decrementer.svelte';
	import Resetter from './Resetter.svelte';

	let count_value;

	const unsubscribe = count.subscribe(value => {
		count_value = value;
	});

	+++onDestroy(unsubscribe);+++
</script>

<h1>The count is {count_value}</h1>
```

그러나 특히 컴포넌트가 여러 스토어를 구독하는 경우, 이러한 방식은 다소 번거로워집니다. 대신, 스벨트는 스토어 이름 앞에 `$`를 붙여 스토어 값을 참조할 수 있는 트릭이 있습니다.

```svelte
/// file: App.svelte
<script>
	---import { onDestroy } from 'svelte';---
	import { count } from './stores.js';
	import Incrementer from './Incrementer.svelte';
	import Decrementer from './Decrementer.svelte';
	import Resetter from './Resetter.svelte';

	---let count_value;---

	---const unsubscribe = count.subscribe(value => {
		count_value = value;
	});---

	---onDestroy(unsubscribe);---
</script>

<h1>The count is {+++$count+++}</h1>
```

> 자동 구독은 컴포넌트의 최상위 범위에 선언되거나 가져온 스토어 변수에만 작동합니다.

`$count`를 마크업 내에서 뿐만 아니라, 이벤트 핸들러나 반응형 선언과 같은 `<script>` 내 어디서든 사용할 수 있습니다.

> `$`로 시작하는 모든 이름은 스토어 값을 참조하는 것으로 간주됩니다. 이는 사실상 예약된 문자입니다.스벨트는 `$` 접두사를 사용하여 변수를 선언하지 못하도록 합니다.
