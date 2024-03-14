---
title: 페이지 새로고침
---

일반적으로 스벨트킷은 페이지 간 이동 시 페이지를 새로 고치지 않습니다. 예제에서 `/` 와 `/about` 간 이동 시 타이머가 계속 작동하는 것을 볼 수 있습니다.

그러나 가끔 이 동작을 비활성화하고 싶을 수 있습니다. 이 경우, 개별 링크 또는 링크를 감싸는 부모 요소에 `data-sveltekit-reload` 속성을 추가하면 됩니다.

```svelte
/// file: src/routes/+layout.svelte
<nav +++data-sveltekit-reload+++>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>
```

사용 가능한 링크 옵션과 해당 값에 대한 자세한 내용은 [link options 문서](https://kit.svelte.dev/docs/link-options)를 참조하세요.