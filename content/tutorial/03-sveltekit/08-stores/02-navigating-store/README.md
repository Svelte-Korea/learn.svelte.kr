---
title: navigating
---

`navigating` 스토어는 현재 네비게이션 정보를 담고 있습니다. 링크를 클릭하거나, 앞/뒤로 이동하거나, 계획적으로 진행된 `goto`문처럼 네비게이션이 지속되는 경우에, `navigation`에는 다음과 같은 속성을 가지는 오브젝트가 됩니다.

- `from` 과 `to` — `params`, `route`, `url`  속성을 가진 오브젝트
- `type` — 네비게이션의 타입. 예시로 `link`, `popstate` 와 `goto`가 있습니다.

> 네비게이션 타입에 대한 완전한 정보를 원하면 [`Navigation`](https://kit.svelte.dev/docs/types#public-types-navigation) 문서를 참고해 주세요.

이 스토어를 이용해 네비게이션에 오래 걸리는 경우를 위한 로딩 인디케이터를 표시할 수 있습니다. 이 예제에서, `src/routes/+page.server.js` 와 `src/routes/about/+page.server.js` 에는 인위적인 딜레이가 있습니다. `src/routes/+layout.svelte`,에 `navigating` 스토어를 불러오고 네비게이션 바에 메세지를 추가해봅시다.

```svelte
/// file: src/routes/+layout.svelte
<script>
	import { page, +++navigating+++ } from '$app/stores';
</script>

<nav>
	<a href="/" aria-current={$page.url.pathname === '/'}>
		home
	</a>

	<a href="/about" aria-current={$page.url.pathname === '/about'}>
		about
	</a>

+++	{#if $navigating}
		navigating to {$navigating.to.url.pathname}
	{/if}+++
</nav>

<slot />
```
