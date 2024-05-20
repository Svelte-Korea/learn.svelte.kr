---
title: <svelte:document>
---

`<svelte:document>` 요소를 사용하면 `document`에서 발생하는 이벤트를 수신할 수 있습니다. 이는 `window`에서 발생하지 않는 `selectionchange`와 같은 이벤트에 유용합니다.

`selectionchange` 핸들러를 `<svelte:document>` 태그에 추가해봅시다.

```svelte
/// file: App.svelte
<svelte:document +++on:selectionchange={handleSelectionChange}+++ />
```

> 모든 브라우저에서 `document`에서 `mouseenter` 및 `mouseleave` 이벤트가 발생하지 않으므로, 이 요소에서 해당 핸들러를 피하세요. 대신 `<svelte:body>`를 사용하세요.
