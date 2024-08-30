---
title: 차원
---

모든 블록 수준 요소에는 `clientWidth`, `clientHeight`, `offsetWidth` 및 `offsetHeight` 바인딩이 있습니다.

```svelte
/// file: App.svelte
<div +++bind:clientWidth={w} bind:clientHeight={h}+++>
	<span style="font-size: {size}px" contenteditable>{text}</span>
	<span class="size">{w} x {h}px</span>
</div>
```

이 바인딩은 읽기 전용입니다. `w`와 `h`의 값을 변경해도 요소에는 아무런 영향을 미치지 않습니다.

> 요소는 [이 기술](http://www.backalleycoder.com/2013/03/18/cross-browser-event-based-element-resize-detection/)과 유사한 방법을 사용하여 측정됩니다. 약간의 오버헤드가 발생하므로 많은 수의 요소에 대해 이를 사용하는 것은 권장되지 않습니다.
>
> `display: inline` 요소는 이 방법으로 측정할 수 없으며, 다른 요소를 포함할 수 없는 요소(예: `<canvas>`)도 마찬가지입니다. 이러한 경우 래퍼 요소를 대신 측정해야 합니다.
