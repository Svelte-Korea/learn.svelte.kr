---
title: updated
---

`updated` 스토어는 현재 페이지가 열린 순간 기준으로 앱의 새 버전이 배포되었는지 알려주는 `true`, `false` 값을 가지고 있습니다. 이 스토어가 작동하려면, `svelte.config.js`에 `kit.version.pollInterval` 을 명시해야합니다.

```svelte
/// file: src/routes/+layout.svelte
<script>
	import { page, navigating, +++updated+++ } from '$app/stores';
</script>
```

버전 변경은 제품에서만 일어나고, 개발 중에서는 발생하지 않습니다. 그래서 `$updated` 값은 튜토리얼에서 항상 `false` 입니다.

`pollInterval`에 상관없이 새 버전을 확인하고 싶다면 `updated.check()`을 호출하세요.

```svelte
/// file: src/routes/+layout.svelte

+++{#if $updated}+++
	<div class="toast">
		<p>
			A new version of the app is available

			<button on:click={() => location.reload()}>
				reload the page
			</button>
		</p>
	</div>
+++{/if}+++
```
