---
title: 오류 페이지
---

`load` 함수 내에서 문제가 발생하면 스벨트킷은 오류 페이지를 렌더링합니다.

기본 오류 페이지는 다소 밋밋합니다. `src/routes/+error.svelte` 컴포넌트를 생성해서 이를 사용자 정의할 수 있습니다.

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

`+error.svelte` 컴포넌트가 루트 `+layout.svelte` 내에 렌더링된다는 점에 유의하세요. 더 세분화된 `+error.svelte` 경계를 생성할 수 있습니다.

```svelte
/// file: src/routes/expected/+error.svelte
<h1>this error was expected</h1>
```

이 컴포넌트는 `/expected`에 대해 렌더링되며, 다른 오류가 발생할 경우 루트 `src/routes/+error.svelte` 페이지가 렌더링됩니다.
