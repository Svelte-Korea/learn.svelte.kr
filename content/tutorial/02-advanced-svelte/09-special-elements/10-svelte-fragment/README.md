---
title: <svelte:fragment>
---

`<svelte:fragment>` 요소를 사용하면 컨테이너 DOM 요소로 래핑하지 않고도 명명된 슬롯에 콘텐츠를 배치할 수 있습니다.

이 연습에서는 틱택토 게임을 만들고 있습니다. 그리드를 형성하기 위해 `App.svelte`의 `<button>` 요소는 `Board.svelte`의 `<div class="board">` 요소의 직계 자손이어야 합니다.

현재, 이 요소들은 `<div slot="game">`의 자식 요소로 되어 있어 문제가 있습니다. 이를 수정해 봅시다.

```svelte
/// file: App.svelte
<+++svelte:fragment+++ slot="game">
	{#each squares as square, i}
		<button
			class="square"
			class:winning={winningLine?.includes(i)}
			disabled={square}
			on:click={() => {
				squares[i] = next;
				next = next === 'x' ? 'o' : 'x';
			}}
		>
			{square}
		</button>
	{/each}
</+++svelte:fragment+++>
```
