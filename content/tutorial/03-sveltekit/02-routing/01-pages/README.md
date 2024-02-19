---
title: 페이지(Pages)
---

스벨트킷은 파일 시스템 기반 라우팅을 사용합니다. _라우트(route)_, 즉 사용자가 특정 URL로 이동했을 때 앱이 해야 할 일코드 베이스의 디렉터리에서 정의됩니다.

모든 `src/routes` 안에 있는 각 `+page.svelte` 파일은 이 앱에 페이지를 만듭니다. 지금, 이 앱에는 `src/routes/+pages.svelte` 한 페이지만 있습니다. 이는 `/`에 대응됩니다. 만약 `/about`으로 이동하면 404 Not Found 오류를 보게 됩니다.

이걸 고쳐 봅시다. 두 번째 페이지 `src/routes/about/+page.svelte`를 만들고 `src/routes/+page.svelte`의 내용을 복사하고, 아래처럼 바꾸세요.

```svelte
/// file: src/routes/about/+page.svelte
<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

<h1>+++about+++</h1>
<p>this is the +++about+++ page.</p>
```

이제 `/`와 `/about` 사이를 이동할 수 있습니다.

> 기존 멀티 페이지 앱과는 다르게, `/about` 들어갔다 나오면 현재 페이지의 콘텐츠를 업데이트합니다. 이를 통해 서버 렌더링을 통한 빠른 시작과 즉각적인 탐색이라는 두 장점을 다 얻을 수 있습니다. (이 동작은 [설정에서 변경할 수 있습니다.](https://kit.svelte.dev/docs/page-options))