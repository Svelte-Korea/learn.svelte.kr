---
title: 레이아웃(Layouts)
---

앱에 있는 다른 라우트든 같은 UI를 공유하는 경우가 많습니다. 매번 `+page.svelte` 에 반복해서 작성하는 대신에, 같은 디렉터리의 모든 라우트에서 사용할 수 있는 `+layout.svelte` 컴포넌트를 이용할 수 있습니다.

이 앱에는 `src/routes/+page.svelte` 와 `src/routes/about/+page.svelte` 두 가지 라우트가 있습니다. 이 페이지는 같은 네비게이션 UI를 공유합니다. `src/routes/+layout.svelte` 파일을 만들어 봅시다...

```
src/routes/
├ about/
│ └ +page.svelte
+++├ +layout.svelte+++
└ +page.svelte
```

그리고 중복된 내용을 `+page.svelte`에서 방금 만든 `+layout.svelte`로 옮깁시다. `<slot />` 요소는 페이지 콘텐츠가 렌더링 되는 위치입니다.

```svelte
/// file: src/routes/+layout.svelte
<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

<slot />
```

이제 `+layout.svelte` 파일이 모든 자식 라우트, (존재한다면) 같은 계층에 있는 `+page.svelte`에도 적용됩니다. 레이아웃은 임의의 깊이까지 중첩될 수 있습니다.
