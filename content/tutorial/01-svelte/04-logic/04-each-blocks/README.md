---
title: Each 블록
---

사용자 인터페이스를 구축할 때 데이터 목록을 자주 다루게 됩니다. 이 연습에서는 `<button>` 마크업을 여러 번 반복해서 각기 다른 색상이 된 상태입니다. 여기서 개선해 봅시다.

일일이 복사, 붙여넣기 및 편집하는 대신 첫 버튼만 남기고, `each` 블록을 사용할 수 있습니다.

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

이 예제에 사용되는 `colors` 와 같이 `each` 와 같이 쓸 수 있는 표현식으로는 `length` 속성이 있는, 배열이나 배열과 유사한 객체면 다 가능합니다. 일반적인 이터러블(iterable)은 `each [...iterable]` 형태로 순회 가능합니다.

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

현재의 _인덱스_ 를 두 번째 인자로 가져올 수 있습니다.

```svelte
/// file: App.svelte
<div>
	{#each colors as color, +++i}+++
		<button
			aria-current={selected === color}
			aria-label={color}
			style="background: {color}"
			on:click={() => selected = color}
		>+++{i + 1}+++</button>
	{/each}
</div>
```
