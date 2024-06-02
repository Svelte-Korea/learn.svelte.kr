---
title: 텍스트 영역 입력
---

`<textarea>` 요소는 스벨트에서 텍스트 입력과 유사하게 동작합니다. `bind:value`를 사용해봅시다.

```svelte
/// file: App.svelte
<textarea +++bind:value=+++{value}></textarea>
```

이처럼 이름이 일치하는 경우에는, 축약형을 사용할 수도 있습니다.

```svelte
/// file: App.svelte
<textarea +++bind:value+++></textarea>
```

이 방법은 텍스트 영역뿐만 아니라 모든 바인딩에 적용됩니다.
