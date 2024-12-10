---
title: 슬롯 콘텐츠 확인
---

일부 경우에는 슬롯 콘텐츠가 전달되었는지 여부에 따라 컴포넌트의 일부를 제어하고 싶을 수 있습니다. 예를 들어, `App.svelte`에서 `<header>`를 제거하면...

```svelte
/// file: App.svelte
---<header slot="header" class="row">
	<span class="color" />
	<span class="name">name</span>
	<span class="hex">hex</span>
	<span class="rgb">rgb</span>
	<span class="hsl">hsl</span>
</header>---

<div class="row">
	<span class="color" style="background-color: {row.hex}" />
	<span class="name">{row.name}</span>
	<span class="hex">{row.hex}</span>
	<span class="rgb">{row.rgb}</span>
	<span class="hsl">{row.hsl}</span>
</div>
```

...`FilterableList.svelte`는 여전히 `<div class="header">`를 렌더링하고 있어 보기 흉한 이중 경계선이 남습니다.

이를 `FilterableList.svelte`에서 특수 변수 `$$slots`를 사용하여 수정할 수 있습니다:

```svelte
/// file: FilterableList.svelte
+++{#if $$slots.header}+++
	<div class="header">
		<slot name="header"/>
	</div>
+++{/if}+++
```
