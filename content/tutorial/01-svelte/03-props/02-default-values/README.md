---
title: Default values
---

We can easily specify default values for props in `Nested.svelte`:

```svelte
/// file: Nested.svelte
<script>
	export let answer +++= 'a mystery'+++;
</script>
```

If we now add a second component _without_ an `answer` prop, it will fall back to the default:

```svelte
/// file: App.svelte
<Nested answer={42}/>
+++<Nested />+++
```
---
title: 기본값
---

`Nested.svelte`에서 props의 기본값을 쉽게 지정할 수 있습니다.

```svelte
/// file: Nested.svelte
<script>
	export let answer +++= 'a mystery'+++;
</script>
```

이제 `answer` prop _없이_ 두 번째 컴포넌트를 추가하면, 기본값이 사용될 것입니다.

```svelte
/// file: App.svelte
<Nested answer={42}/>
+++<Nested />+++
```
