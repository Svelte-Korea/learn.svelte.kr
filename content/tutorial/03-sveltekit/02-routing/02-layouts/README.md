---
title: 레이아웃
---

앱의 다른 경로가 공통 UI를 공유하는 경우가 많습니다. 각각 `+page.svelte`에서 이를 반복하는 대신, 동일한 디렉토리의 모든 경로에 적용되는 `+layout.svelte`컴포넌트를 사용할 수 있습니다.

이 앱에는 내비게이션 UI가 같은 `src/routes/+page.svelte` 와 `src/routes/about/+page.svelte` 두 개의 경로가 있습니다. 새로운 `src/routes/+layout.svelte` 파일을 생성하고...

```
src/routes/
├ about/
│ └ +page.svelte
+++├ +layout.svelte+++
└ +page.svelte
```

...이어서 `+page.svelte` 에서 겹치는 내용을 새로운 `+layout.svelte` 파일로 옮겨봅시다. `<slot />`은 페이지의 내용을 렌더링하는 요소입니다.

```svelte
/// file: src/routes/+layout.svelte
<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

<slot />
```

`+layout.svelte`파일은 (만약 존재한다면)동일 레벨 경로의 `+page.svelte`를 포함해서 모든 하위 경로에 적용됩니다. 레이아웃은 임의의 깊이까지 중첩할 수 있습니다.
