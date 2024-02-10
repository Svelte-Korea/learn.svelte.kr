---
title: 경로 파라미터
path: /blog
---

동적 파라미터가 있는 경로를 만드려면 유효한 변수 이름에 대괄호를 씌웁니다. 예를 들어 `src/routes/blog/[slug]/+page.svelte`과 같은 파일은 `/blog/one`, `/blog/two`, `/blog/three` 등에 일치하는 경로를 생성합니다.

해당 파일을 만들어봅시다.

```svelte
/// file: src/routes/blog/[slug]/+page.svelte
<h1>blog post</h1>
```

이제 `/blog` 페이지에서 개별 블로그 게시물로 이동할 수 있습니다. 다음 챕터에서는 콘텐츠를 로드하는 방법을 살펴보겠습니다.

> 다중 경로 파라미터는 한 개 이상의 정적 문자로 구분되는 하나의 URL 세그먼트 _내_ 에 나올 수 있습니다. 예를 들어, `[bar]` 및 `[baz]`가 동적 파라미터일 때 `foo/[bar]x[baz]`는 유효한 경로입니다.
