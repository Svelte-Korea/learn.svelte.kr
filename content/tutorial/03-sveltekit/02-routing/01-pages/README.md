---
title: 페이지(Pages)
---

스벨트킷은 파일시스템 기반의 라우팅을 사용합니다. 이것은 사용자가 특정 URL로 이동할 때의 앱 동작이 코드의 디렉토리에 의해 정의된다는 뜻입니다.

`src/routes` 안의 모든 `+page.svelte` 파일은 앱의 페이지를 생성합니다. 이 앱에서는 현재 `/` 에 매핑되는 하나의 앱 페이지 `src/routes/+page.svelte`만 존재합니다. 만약 우리가 `/about`, 으로 이동하면, 404 Not Found 에러를 마주할 것입니다.

수정해봅시다. `src/routes/+page.svelte`의 내용을 복사해서 두 번째 페이지 `src/routes/about/+page.svelte`를 성성하고, 갱신해보세요.

```svelte
/// file: src/routes/about/+page.svelte
<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

<h1>+++about+++</h1>
<p>this is the +++about+++ page.</p>
```

이제 우리는 `/` 와 `/about`으로 모두 이동할 수 있습니다.

> 기존 다중 페이지 앱과 다르게, `/about`으로 이동했다가 뒤로 이동하면 단일 페이지 앱처럼 현재 페이지의 내용을 갱신합니다. 이를 통해 서버 렌더링 된 빠른 시작과 즉각적인 이동이라는 두 가지 장점을 모두 누릴 수 있습니다. (이 동작은 [구성](https://kit.svelte.dev/docs/page-options)할 수 있습니다.)
