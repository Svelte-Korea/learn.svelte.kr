---
title: 체크박스 입력
---

체크박스는 상태 간 전환에 사용됩니다. `input.value` 대신 `input.checked`에 바인딩합시다.

```svelte
/// file: App.svelte
<input type="checkbox" +++bind:+++checked={yes}>
```
