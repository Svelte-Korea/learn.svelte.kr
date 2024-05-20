---
title: Each 블록
---

사용자 인터페이스를 구축할 때 데이터 목록을 자주 다루게 됩니다. 이번 연습에서는 `<button>` 마크업을 여러 번 반복하며 각기 다른 색상을 적용했지만, 아직 추가해야 할 부분이 더 있습니다.

일일이 복사, 붙여넣기 및 편집하는 대신 첫 번째 버튼을 제외한 모든 버튼을 제거한 다음, `each` 블록을 사용할 수 있습니다.

```svelte
/// file: App.svelte
<div>
	+++{#each colors as color}+++
		<button
			aria-current={selected === 'red'}
			aria-label="red"
			style="background: red"
			on:click={() => selected = 'red'}
		></button>
	+++{/each}+++
</div>
```

> 표현식(여기에서는 `colors`)은 아무 배열이나 배열과 유사한 객체(즉, `length` 속성이 있는 객체)일 수 있습니다. `each [...iterable]`로 제네릭 이터러블(Generic Tterables)을 순회할 수 있습니다.

이제 `"red"`의 위치에 `color` 변수를 사용해야 합니다.

```svelte
/// file: App.svelte
<div>
	{#each colors as color}
		<button
			aria-current={selected === +++color+++}
			aria-label=+++{color}+++
			style="background: +++{color}+++"
			on:click={() => selected = +++color+++}
		></button>
	{/each}
</div>
```

현재의 _인덱스_ 를 두 번째 인수로 가져올 수 있습니다. 이렇게요.

```svelte
/// file: App.svelte
<div>
	{#each colors as color, +++i+++}
		<button
			aria-current={selected === color}
			aria-label={color}
			style="background: {color}"
			on:click={() => selected = color}
		>+++{i + 1}+++</button>
	{/each}
</div>
```
