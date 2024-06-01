---
title: DOM 이벤트
---

이미 간단히 본 것처럼, `on:` 지시어를 사용하여 요소의 클릭이나 [포인터 이동](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointermove_event)과 같은 DOM 이벤트를 감지할 수 있습니다.

```svelte
/// file: App.svelte
<div +++on:pointermove={handleMove}+++>
	The pointer is at {m.x} x {m.y}
</div>
```
