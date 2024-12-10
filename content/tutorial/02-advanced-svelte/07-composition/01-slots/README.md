---
title: 슬롯
---

엘리먼트가 자식을 가질 수 있는 것처럼 컴포넌트도 자식을 가질 수 있습니다.

```html
/// no-file
<div>
	<p>I'm a child of the div</p>
</div>
```

 그러나 컴포넌트가 자식을 허용하려면, 자식을 어디에 배치할지 알아야 합니다. 이를 `<slot>` 요소를 사용하여 수행합니다. `Card.svelte` 안에 다음 내용을 추가하세요.

```svelte
/// file: Card.svelte
<div class="card">
	+++<slot />+++
</div>
```

이제 카드에 자식을 넣을 수 있습니다.

```svelte
/// file: App.svelte
<Card>
	+++<span>Patrick BATEMAN</span>+++
	+++<span>Vice President</span>+++
</Card>
```
