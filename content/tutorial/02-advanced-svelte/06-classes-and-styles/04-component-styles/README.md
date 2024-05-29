---
title: 컴포넌트 스타일
---

종종 자식 컴포넌트의 스타일에 영향을 주어야 할 때가 있습니다. 예를 들어, 이 박스들을 빨강, 초록, 파랑으로 만들고 싶다고 해봅시다.

한 가지 방법은 `:global` CSS 수정자를 사용하는 것으로, 이를 통해 다른 컴포넌트 내부의 요소를 무차별적으로 타겟팅할 수 있습니다.

```svelte
/// file: App.svelte
<style>
	.boxes :global(.box:nth-child(1)) {
		background-color: red;
	}

	.boxes :global(.box:nth-child(2)) {
		background-color: green;
	}

	.boxes :global(.box:nth-child(3)) {
		background-color: blue;
	}
</style>
```

하지만 그렇게 하지 _말아야_ 할 이유가 많습니다. 우선, 코드가 매우 장황해집니다. 또한, 이는 불안정합니다. `Box.svelte`의 구현 세부사항에 대한 변경은 선택자를 망가뜨릴 수 있습니다.

무엇보다, 이는 무례한 방식입니다. 컴포넌트는 자신이 프롭(props)으로 노출하는 변수들을 결정하는 것과 마찬가지로, '외부'에서 제어할 수 있는 스타일을 스스로 결정할 수 있어야 합니다. `:global`은 최후의 수단으로 사용해야 합니다.

`Box.svelte` 내부에서 `background-color`가 [CSS 사용자 정의 속성](https://developer.mozilla.org/en-US/docs/Web/CSS/--*)에 의해 결정되도록 변경합시다.

```svelte
/// file: Box.svelte
<style>
	.box {
		width: 5em;
		height: 5em;
		border-radius: 0.5em;
		margin: 0 0 1em 0;
		background-color: +++var(--color, #ddd)+++;
	}
</style>
```

`<div class="boxes">`과 같은 모든 부모 요소는 `--color`의 값을 설정할 수 있지만, 개별 컴포넌트에도 설정할 수 있습니다.

```svelte
/// file: App.svelte
<div class="boxes">
	<Box +++--color="red"+++ />
	<Box +++--color="green"+++ />
	<Box +++--color="blue"+++ />
</div>
```

값은 다른 속성과 마찬가지로 동적일 수 있습니다.

이 기능은 필요한 경우 각 컴포넌트를 `<div style="display: contents">`로 감싸고 사용자 정의 속성을 적용함으로써 작동합니다.
