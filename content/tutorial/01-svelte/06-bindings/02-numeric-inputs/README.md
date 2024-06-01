---
title: 숫자 입력
---

DOM에서는 모든 것이 문자열입니다. 이는 `type="number"` 및 `type="range"`와 같은 숫자 입력을 다룰 때 도움이 되지 않습니다. `input.value`를 사용하기 전에 이를 강제로 숫자로 변환해야 하기 때문입니다.

`bind:value`를 사용하면 스벨트가 이를 처리해줍니다.

```svelte
/// file: App.svelte
<label>
	<input type="number" +++bind:+++value={a} min="0" max="10" />
	<input type="range" +++bind:+++value={a} min="0" max="10" />
</label>

<label>
	<input type="number" +++bind:+++value={b} min="0" max="10" />
	<input type="range" +++bind:+++value={b} min="0" max="10" />
</label>
```
