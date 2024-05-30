---
title: 에러 페이지
---

`load` 함수 안에서 뭔가 잘못되면, 스벨트킷은 에러 페이지를 렌더합니다.

기본 에러 페이지는 특색이 없습니다. `src/routes/+error.svelte` 컴포넌트를 만들어서 에러 페이지를 꾸밀 수 있습니다.

```svelte
/// file: src/routes/+error.svelte
<script>
	import { page } from '$app/stores';
	import { emojis } from './emojis.js';
</script>

<h1>{$page.status} {$page.error.message}</h1>
<span style="font-size: 10em">
	{emojis[$page.status] ?? emojis[500]}
</span>
```

`+error.svelte` 컴포넌트는 루트 `+layout.svelte` 안에 렌더된다는 것을 명심합시다. 보다 세밀한 `+error.svelte` 경계를 만들 수도 있습니다.

```svelte
/// file: src/routes/expected/+error.svelte
<h1>this error was expected</h1>
```

이 컴포넌트는 `/expected`에서 렌됩니다. 반면에, 다른 곳에서 발생한 에러는 루트 `src/routes/+error.svelte` 페이지가 렌더됩니다.

