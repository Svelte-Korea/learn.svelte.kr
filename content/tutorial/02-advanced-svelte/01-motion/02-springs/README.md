---
title: 스프링(Springs)
---

스프링(`spring`) 함수는 트윈드(`tweened`) 대신에 사용할 수 있는 함수로, 값이 자주 바뀌는 경우에 더 좋은 결과를 보여주는 경우가 많습니다.

이 예제에는 두 스토어가 있습니다. 하나는 원의 좌푯값을 표현하고, 다른 하나는 크기를 표현합니다. 이것들을 스프링으로 바꿔 봅시다.

```svelte
/// file: App.svelte
<script>
	import { +++spring+++ } from 'svelte/+++motion+++';

	let coords = +++spring+++({ x: 50, y: 50 });
	let size = +++spring+++(10);
</script>
```

두 스프링 다 `stiffness` 와 `damping` 기본값을 가지고 있습니다. 이 값들은 스프링의, 음, 스프링다움을 조정합니다. 우리가 지정한 초기값으로도 바꿀 수 있습니다.

```
/// file: App.svelte
let coords = spring({ x: 50, y: 50 }, +++{
	stiffness: 0.1,
	damping: 0.25
}+++);
```

마우스를 이리저리 움직여 보고, 슬라이더를 드래그해서 스프링의 행동에 어떤 영향을 미치는지 느껴보세요. 스프링 모션이 진행 중인 상황에서도 값을 조정할 수 있다는 걸 명심하세요.
