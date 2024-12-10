---
title: <svelte:window>
---

어떤 DOM 요소에든 이벤트 리스너를 추가할 수 있는 것처럼, `<svelte:window>`를 사용하여 `window` 객체에 이벤트 리스너를 추가할 수 있습니다.

여기, 이미 선언된 `handleKeydown` 함수가 있습니다. 이제 `keydown` 리스너를 추가하기만 하면 됩니다.

```svelte
/// file: App.svelte
<svelte:window +++on:keydown={handleKeydown}+++ />
```

> DOM 요소와 마찬가지로, `preventDefault`와 같은 [이벤트 수정자](/tutorial/event-modifiers)를 추가할 수 있습니다.
