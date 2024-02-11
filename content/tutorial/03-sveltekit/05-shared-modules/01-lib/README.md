---
title: $lib 별칭(The $lib alias)
---

SvelteKit 이 디렉토리 기반 라우팅을 사용하는 덕분에, 모듈과 컴포넌트를 그들이 사용되는 위치 근처에 배치하기 쉽습니다. 경험적으로, '코드가 사용되는 곳 근처에 코드를 놓는 것'이 좋습니다.

가끔, 코드는 여러번 사용됩니다. 이런 경우에는 그런 파일을 모든 라우트에서 `../../../../` 같은 기다란 임포트 없는 곳에 넣을 수 잇으면 편하겠죠. SvelteKit에는 `src/lib` 디렉토리가 그 역할을 합니다. 이 디렉토리 안에 있는 모든 건 `src` 내에 있는 모듈 모듈에서 `$lib` 별칭을 통해 접근할 수 있습니다.

이 예제의 두 `+page.svelte` 파일은 `src/lib/message.js`를 불러옵니다. `/a/deeply/nested/route`으로 이동하면, 앱이 멈춥니다. 왜냐하면 경로를 잘못 썼기 때문입니다. `$lib/message.js`를 사용하도록 바꿔봅시다.

```svelte
/// file: src/routes/a/deeply/nested/route/+page.svelte
<script>
	import { message } from +++'$lib/message.js'+++;
</script>

<h1>a deeply nested route</h1>
<p>{message}</p>
```

`src/routes/+page.svelte`에도 같은 일을 해봅시다.

```svelte
/// file: src/routes/+page.svelte
<script>
	import { message } from +++'$lib/message.js'+++;
</script>

<h1>home</h1>
<p>{message}</p>
```
