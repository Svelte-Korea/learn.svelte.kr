---
title: 레이아웃 데이터
path: /blog
---

`+layout.svelte` 파일이 각 자식 라우트에 UI를 만들듯이, `+layout.server.js` 파일은 각 자식 라우트를 위해 데이터를 불러옵니다.

'more posts' 사이드바를 우리 블로그 포스트 페이지에 추가하고 싶을 때, `src/routes/blog/[slug]/+page.server.js`의 `load` 함수에서  `summaries` 를 반환하게 _할_ _수_ 있습니다. `src/routes/blog/+page.server.js`에서 했듯이 말이죠. 하지만 반복이 발생합니다.

그 대신, `src/routes/blog/+page.server.js`의 이름을`src/routes/blog/+layout.server.js` 로 바꿔봅시다. `/blog` 라우트가 계속 작동하는 것을 명심합시다. `data.summaries`는 여전히 페이지에서 사용가능합니다.

그럼, 포스트 페이지를 위한 레이아웃에 사이드바를 추가해 봅시다.

```svelte
/// file: src/routes/blog/[slug]/+layout.svelte
<script>
	export let data;
</script>

<div class="layout">
	<main>
		<slot />
	</main>

+++	<aside>
		<h2>More posts</h2>
		<ul>
			{#each data.summaries as { slug, title }}
				<li>
					<a href="/blog/{slug}">{title}</a>
				</li>
			{/each}
		</ul>
	</aside>+++
</div>

<style>
	@media (min-width: 640px) {
		.layout {
			display: grid;
			gap: 2em;
			grid-template-columns: 1fr 16em;
		}
	}
</style>
```

레이아웃과 그 아래 있는 모든 페이지는 부모 `+layout/server.js`에 있는 `data.summaries`를 이어받습니다.

한 포스트에서 다른 포스트로 이동할 때, 그 포스트 자체 데이터만 로드하면 됩니다. 레이아웃 데이터는 여전히 유효합니다. 자세한 설명은 [무효화(invalidation)](https://kit.svelte.dev/docs/load#rerunning-load-functions)에 대한 설명을 참고하세요.
