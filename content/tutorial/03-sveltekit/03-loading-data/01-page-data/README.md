---
title: 페이지 데이터
path: /blog
---

SvelteKit의 핵심 기능은 3가지로 요약됩니다.

1. **라우팅(Routing)** — 들어온 요청이랑 어느 라우트가 일치하는지 알아내기
2. **로딩(Loading)** — 라우트에 필요한 데이터 가져오기
3. **렌더링(Rendering)** — 서버에서 HTML을 만들거나 브라우저에서 DOM 업데이트하기

라우팅과 렌더링이 어떻게 작동하는지는 다뤘습니다. 이제 중간 부분, 로딩에 대해 알아봅시다.

앱에 있는 모든 페이지는 `+page.svelte`와 같이 있는 `+page.sever.js`에 `load` 함수를 정의할 수 있습니다. 이름에서 알 수 있듯이, 이 모듈은 서버에서만 동작합니다(클라이언트 측 탐색 중이더라도). 그럼, 하드 코딩된 `src/routes/blog/+page.svelte` 데이터를 실제 블로그 데이터로 바꾸기 위해 `src/routes/blog/+page.server.js` 파일을 추가해 봅시다.

```js
/// file: src/routes/blog/+page.server.js
import { posts } from './data.js';

export function load() {
	return {
		summaries: posts.map((post) => ({
			slug: post.slug,
			title: post.title
		}))
	};
}
```

> 이 튜토리얼에서는 `src/routes/blog/data.js`에서 데이터를 가져올 것입니다. 실제 앱에서는, 데이터베이스나 CMS에서 데이터를 가져올 일이 많겠지만, 지금은 이렇게 하겠습니다.

`data` 프롭을 통해 `src/routes/blog/+page.svelte`에서 데이터에 접근할 수 있습니다.

```svelte
/// file: src/routes/blog/+page.svelte
+++<script>
	export let data;
</script>+++

<h1>blog</h1>

<ul>
---	<li><a href="/blog/one">one</a></li>
	<li><a href="/blog/two">two</a></li>
	<li><a href="/blog/three">three</a></li>---
+++	{#each data.summaries as { slug, title }}
		<li><a href="/blog/{slug}">{title}</a></li>
	{/each}+++
</ul>
```

그럼, 포스트 페이지에도 같은 일을 해봅시다.

```js
/// file: src/routes/blog/[slug]/+page.server.js
import { posts } from '../data.js';

export function load({ params }) {
	const post = posts.find((post) => post.slug === params.slug);

	return {
		post
	};
}
```

```svelte
/// file: src/routes/blog/[slug]/+page.svelte
+++<script>
	export let data;
</script>+++

---<h1>blog post</h1>---
+++<h1>{data.post.title}</h1>
<div>{@html data.post.content}</div>+++
```

그리고 우리가 신경 써야할 세부사항이 하나 더 있습니다. 사용자가 `/blog/nope`와 같은 잘못된 경로에 들어갈 경우, 404 페이지를 반환하도록 합시다.

```js
/// file: src/routes/blog/[slug]/+page.server.js
+++import { error } from '@sveltejs/kit';+++
import { posts } from '../data.js';

export function load({ params }) {
	const post = posts.find((post) => post.slug === params.slug);

	+++if (!post) throw error(404);+++

	return {
		post
	};
}
```

다음 장에서 오류 처리에 대해 더 배워봅시다.
