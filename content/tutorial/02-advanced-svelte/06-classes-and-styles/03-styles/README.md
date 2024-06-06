---
title: style 지시어
---

`class`와 마찬가지로, 인라인 `style` 속성을 그대로 작성할 수 있습니다. 왜냐하면 스벨트는 실제로 멋진 부분이 추가된 HTML이기 때문입니다:

```svelte
/// file: App.svelte
<button
	class="card"
	+++style="transform: {flipped ? 'rotateY(0)' : ''}; --bg-1: palegoldenrod; --bg-2: black; --bg-3: goldenrod"+++
	on:click={() => flipped = !flipped}
>
```

스타일이 많아지면 코드가 다소 어수선해질 수 있습니다. `style:` 지시어를 사용하여 코드를 정리할 수 있습니다.

```svelte
/// file: App.svelte
<button
	class="card"
+++	style:transform={flipped ? 'rotateY(0)' : ''}
	style:--bg-1="palegoldenrod"
	style:--bg-2="black"
	style:--bg-3="goldenrod"+++
	on:click={() => flipped = !flipped}
>
```
