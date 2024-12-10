---
title: 그룹 입력
---

여러 `type="radio"` 또는 `type="checkbox"` 입력이 동일한 값과 관련이 있는 경우, `value` 속성과 함께 `bind:group`을 사용할 수 있습니다. 동일한 그룹의 라디오 입력은 상호 배타적이며, 동일한 그룹의 체크박스 입력은 선택된 값들의 배열을 형성합니다.

라디오 입력에 `bind:group={scoops}`를 추가합시다.

```svelte
/// file: App.svelte
<input
	type="radio"
	name="scoops"
	value={number}
	+++bind:group={scoops}+++
/>
```

그리고 체크박스 입력에 `bind:group={flavours}`를 추가하세요.

```svelte
/// file: App.svelte
<input
	type="checkbox"
	name="flavours"
	value={flavour}
	+++bind:group={flavours}+++
/>
```
