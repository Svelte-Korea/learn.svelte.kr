---
title: 축약형 class 지시어
---

종종 클래스 이름은 클래스가 의존하는 값의 이름과 동일합니다.

```svelte
/// no-file
<button
	class="card"
	class:flipped={flipped}
	on:click={() => flipped = !flipped}
>
```

이런 경우 축약형을 사용할 수 있습니다.

```svelte
/// file: App.svelte
<button
	class="card"
	+++class:flipped+++
	on:click={() => flipped = !flipped}
>
```
