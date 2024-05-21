---
title: 기본값
---

프롭의 기본값을 쉽게 지정할 수 있습니다. `Nested.svelte`를 봐 봅시다.

```svelte
/// file: Nested.svelte
<script>
	export let answer +++= 'a mystery'+++;
</script>
```

이제 `answer` 프롭 _없이_ 두 번째 컴포넌트를 추가하면, 기본값이 사용될 것입니다.

```svelte
/// file: App.svelte
<Nested answer={42}/>
+++<Nested />+++
```
