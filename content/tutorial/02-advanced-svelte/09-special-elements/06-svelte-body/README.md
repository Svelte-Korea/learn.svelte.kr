---
title: <svelte:body>
---

`<svelte:window>`와 유사하게, `<svelte:body>` 요소를 사용하면 `document.body`에서 발생하는 이벤트를 수신할 수 있습니다. 이는 `window`에서 발생하지 않는 `mouseenter` 및 `mouseleave` 이벤트에 유용합니다.

이 `mouseenter` 및 `mouseleave` 핸들러를 `<svelte:body>` 태그에 추가해봅시다.

```svelte
/// file: App.svelte
<svelte:body
	+++on:mouseenter={() => hereKitty = true}+++
	+++on:mouseleave={() => hereKitty = false}+++
/>
```

그리고 `<body>` 위에 마우스를 올려봅시다.
