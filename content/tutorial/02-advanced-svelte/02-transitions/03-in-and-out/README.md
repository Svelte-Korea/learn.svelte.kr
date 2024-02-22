---
title: 인 앤 아웃
---

`transition` 지시어 대신에, 요소에 `in` 이나 `out`, 아니면 둘 모두의 지시어를 설정할 수 있습니다. `fly` 와 함께 `fade` 를 불러옵시다.

```js
/// file: App.svelte
import { +++fade+++, fly } from 'svelte/transition';
```

`transition` 지시어를 `in` 과 `out` 불리된 지시어로 바꿔 봅시다.

```svelte
/// file: App.svelte
<p +++in+++:fly={{ y: 200, duration: 2000 }} +++out:fade+++>
	Flies in, +++fades out+++
</p>
```

이 경우엔, 전환은 되돌릴 수 _없습니다_.
