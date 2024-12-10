---
title: 내보내기(exports)
---

`context="module"` 스크립트 블록에서 내보낸 모든 항목은 모듈 자체에서 내보내기가 됩니다. `stopAll` 함수를 내보내 봅시다.

```svelte
/// file: AudioPlayer.svelte
<script context="module">
	let current;

+++	export function stopAll() {
		current?.pause();
	}+++
</script>
```

이제 `App.svelte`에서 `stopAll`을 가져올 수 있습니다...

```svelte
/// file: App.svelte
<script>
	import AudioPlayer, +++{ stopAll }+++ from './AudioPlayer.svelte';
	import { tracks } from './tracks.js';
</script>
```

...그리고 이벤트 핸들러에서 사용할 수 있습니다.

```svelte
/// file: App.svelte
<div class="centered">
	{#each tracks as track}
		<AudioPlayer {...track} />
	{/each}

+++	<button on:click={stopAll}>
		stop all
	</button>+++
</div>
```

> 기본 내보내기(default export)를 가질 수는 없습니다. 컴포넌트 _자체가_ 기본 내보내기이기 때문입니다.
