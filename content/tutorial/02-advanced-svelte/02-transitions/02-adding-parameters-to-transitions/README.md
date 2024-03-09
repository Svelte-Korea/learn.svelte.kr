---
title: 파라미터 추가하기
---

전환 함수는 파라미터를 받을 수 있습니다. `fade` 전환을 `fly`로 바꿔봅시다.

```svelte
/// file: App.svelte
<script>
	import { +++fly+++ } from 'svelte/transition';
	let visible = true;
</script>
```

그리고 `<p>` 에 몇 옵션들과 같이 적용해 봅시다.

```svelte
/// file: App.svelte
<p transition:+++fly={{ y: 200, duration: 2000 }}+++>
	+++Flies+++ in and out
</p>
```

전환은 _되돌릴 수 있다_ 는 걸 명심합시다. 전환이 진행 중일 때 체크박스를 토글한다면, 시작이나 끝 지점이 아닌 현재 위치에서 전환이 시작됩니다.
