---
title: 라우트 파라미터
path: /blog
---

동적 파라미터를 가진 라우트를 만들려면, 대괄호(`[]`)와 유효한 변수명을 사용하면 됩니다. 예를 들면, `src/routes/blog/[slug]/+page.svelte` 같은 파일은 `/blog/one`, `/blog/two`, `/blog/three`와 같은 페이지와 매치되는 라우트를 만듭니다.

그 파일을 만들어 봅시다.

```svelte
/// file: src/routes/blog/[slug]/+page.svelte
<h1>blog post</h1>
```

이제 `/blog` 페이지에서 개별적인 블로그 포스트 파일로 이동이 가능합니다. 다음 장에서, 각자 콘텐츠를 어떻게 불러오는지를 다루겠습니다.

> 한 URL 세그먼트 _안_ 에서 여러 라우트 파라미터를 사용할 수 있습니다. 파라미터별로 최소 하나의 정해진 글자를 사용해서 구별하면 됩니다. 예를 들어,  `foo/[bar]x[baz]`는 유효한 라우트고, `[bar]` 와 `[baz]`는 동적 파라미터입니다.
