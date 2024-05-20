---
title: 슬롯 대체 콘텐츠(slot fallbacks)
---

컴포넌트는 `<slot>` 요소 안에 콘텐츠를 넣어서 비어 있는 슬롯에 대한 _대체 콘텐츠_ 를 지정할 수 있습니다.

```svelte
/// file: Card.svelte
<div class="card">
	<header>
		<slot name="telephone">
			+++<i>(telephone)</i>+++
		</slot>
		
		<slot name="company">
			+++<i>(company name)</i>+++
		</slot>
	</header>

	<slot>
		+++<i>(name)</i>+++
	</slot>
		
	<footer>
		<slot name="address">
			+++<i>(address)</i>+++
		</slot>
	</footer>
</div>
```
