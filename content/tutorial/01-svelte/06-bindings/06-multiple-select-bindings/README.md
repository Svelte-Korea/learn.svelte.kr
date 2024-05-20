---
title: Select 요소의 multiple 속성
---

`<select>` 요소에 `multiple` 속성을 추가하면, 단일 값을 선택하는 대신 배열을 채웁니다.

체크박스를 `<select multiple>`로 교체합시다.

```svelte
/// file: App.svelte
<h2>Flavours</h2>

+++<select multiple bind:value={flavours}>+++
	{#each ['cookies and cream', 'mint choc chip', 'raspberry ripple'] as flavour}
+++		<option>{flavour}</option>+++
	{/each}
+++</select>+++
```

`<option>`의 값이 요소의 내용과 동일하기 때문에 `value` 속성을 생략할 수 있습니다.

> 여러 옵션을 선택하려면 `control` 키(또는 MacOS에서는 `command` 키)를 누르고 있어야 합니다.
