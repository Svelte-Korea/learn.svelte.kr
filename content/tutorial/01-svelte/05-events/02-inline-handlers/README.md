---
title: 인라인 핸들러
---

이벤트 핸들러를 인라인으로 선언할 수도 있습니다.

```svelte
/// file: App.svelte
<script>
	let m = { x: 0, y: 0 };

	---function handleMove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}---
</script>

<div
	on:pointermove={+++(e) => {
		m = { x: e.clientX, y: e.clientY };
	}+++}
>
	The pointer is at {m.x} x {m.y}
</div>
```

> 일부 프레임워크에서는 성능상의 이유로, 특히 루프 내에서 인라인 이벤트 핸들러를 피하라는 권고를 볼 수 있습니다. 그 조언은 스벨트에는 적용되지 않습니다. 컴파일러는 선택한 형식에 관계없이 항상 올바른 작업을 수행합니다.
