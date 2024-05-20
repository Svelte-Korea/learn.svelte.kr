---
title: 스토어 바인딩
---

스토어가 쓰기 가능하다면, 다시 말해 `set` 메서드를 가지고 있다면 로컬 컴포넌트 상태와 마찬가지로 그 값에 바인딩할 수 있습니다.

이 예제에서는 `stores.js`에서 쓰기 가능한 스토어 `name`과 파생 스토어 `greeting`을 내보내고 있습니다. `App.svelte`에서 `<input>` 요소를 업데이트합시다.

```svelte
/// file: App.svelte
<input +++bind:+++value={$name}>
```

이제 입력 값을 변경하면 `name` 및 모든 종속 항목이 업데이트됩니다.

컴포넌트 내에서 스토어 값에 직접 할당할 수도 있습니다. `on:click` 이벤트 핸들러를 추가하여 `name`을 업데이트해봅시다.

```svelte
/// file: App.svelte
<button +++on:click={() => $name += '!'}+++>
	Add exclamation mark!
</button>
```

`$name += '!'` 할당은 `name.set($name + '!')`와 동일합니다.
