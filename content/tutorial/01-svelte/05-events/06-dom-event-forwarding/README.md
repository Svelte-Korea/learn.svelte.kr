---
title: DOM 이벤트 전달(forwarding)
---

이벤트 전달은 DOM 이벤트에도 작동합니다.

`<BigRedButton>`에서 클릭에 대한 알림을 받고 싶다면, `BigRedButton.svelte`의 `<button>` 요소에서 `click` 이벤트를 전달하면 됩니다.

```svelte
/// file: BigRedButton.svelte
<button +++on:click+++>
	Push
</button>
```
