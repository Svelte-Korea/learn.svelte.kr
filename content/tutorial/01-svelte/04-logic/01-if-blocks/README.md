---
title: If 블록
---

HTML에는 조건문이나 반복문과 같은 _로직_ 을 표현하는 방법이 없습니다. 하지만 스벨트에는 있습니다.

조건부로 마크업을 렌더링하려면, 이를 `if` 블록으로 감쌉니다. `count`가 `10`보다 클 때 나타나는 텍스트를 추가해 봅시다.

```svelte
/// file: App.svelte
<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

+++{#if count > 10}
	<p>{count} is greater than 10</p>
{/if}+++
```

직접 컴포넌트를 업데이트하고 버튼을 클릭해 보세요.
