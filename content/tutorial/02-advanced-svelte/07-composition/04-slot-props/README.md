---
title: 슬롯 프롭(props)
---

컴포넌트는 _슬롯 프롭(props)_ 을 통해 데이터를 _다시_ 전달할 수 있습니다. 이 앱에는 명명된 CSS 색상의 목록이 있습니다. `<input>`에 입력하면 목록이 필터링됩니다.

현재 모든 행에 `AliceBlue`가 표시되고 있으며, 이는 아름다운 색상이지만 우리가 원하는 것은 아닙니다.

`FilterableList.svelte`를 엽시다. 목록의 각 필터링된 항목에 대해 `<slot>`이 렌더링되고 있습니다. 데이터를 슬롯에 전달합시다.

```svelte
/// file: FilterableList.svelte
<div class="content">
	{#each data.filter(matches) as item}
		<slot +++{item}+++ />
	{/each}
</div>
```

(다른 맥락에서와 마찬가지로, `{item}`은 `item={item}`의 축약형입니다.)

그런 다음, 다른 쪽에서 `let:` 지시어를 사용하여 슬롯 콘텐츠에 데이터를 노출합시다.

```svelte
/// file: App.svelte
<FilterableList
	data={colors}
	field="name"
	+++let:item={row}+++
>
	<div class="row">
		<span class="color" style="background-color: {row.hex}" />
		<span class="name">{row.name}</span>
		<span class="hex">{row.hex}</span>
		<span class="rgb">{row.rgb}</span>
		<span class="hsl">{row.hsl}</span>
	</div>
</FilterableList>
```

마지막으로, 더 이상 필요 없는 플레이스홀더 변수를 제거합시다.

\```svelte
/// file: App.svelte
<script>
	import FilterableList from './FilterableList.svelte';
	import { colors } from './colors.js';

	---let row = colors[0];---
</script>
\```

> 명명된 슬롯도 프롭(props)을 가질 수 있습니다. 컴포넌트 자체가 아닌 `slot="..."` 속성이 있는 요소에서 `let` 지시어를 사용하세요.
