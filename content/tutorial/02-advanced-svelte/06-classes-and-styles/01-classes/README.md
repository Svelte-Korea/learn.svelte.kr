---
title: class 지시어
---

다른 속성과 마찬가지로, JavaScript 속성을 사용하여 클래스를 지정할 수 있습니다. 여기서는 카드에 `flipped` 클래스를 추가할 수 있습니다.

```svelte
/// file: App.svelte
<button
	class="card +++{flipped ? 'flipped' : ''}+++"
	on:click={() => flipped = !flipped}
>
```

이제 카드를 클릭하면 카드가 뒤집히며, 예상대로 작동합니다.

이 작업을 좀 더 깔끔하게 만들 수 있습니다. 조건에 따라 클래스를 추가하거나 제거하는 것은 UI 개발에서 매우 일반적인 패턴이므로, Svelte는 이를 단순화하기 위한 특수 지시어를 포함하고 있습니다.

```svelte
/// file: App.svelte
<button
	class="card"
	+++class:flipped={flipped}+++
	on:click={() => flipped = !flipped}
>
```

이 지시어는 'flipped가 참일 때마다 `flipped` 클래스를 추가'한다는 의미입니다.
