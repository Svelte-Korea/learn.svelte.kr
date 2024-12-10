---
title: <svelte:head>
---

`<svelte:head>` 요소를 사용하면 문서의 `<head>` 내부에 요소를 삽입할 수 있습니다. 이는 SEO에 중요한 `<title>` 및 `<meta>` 태그와 같은 항목에 유용합니다.

이 튜토리얼의 맥락에서 이를 보여주는 것이 다소 어렵기 때문에, 대신 스타일시트를 로드하는 용도로 사용해 보겠습니다.

```svelte
/// file: App.svelte
<script>
	const themes = ['margaritaville', 'retrowave', 'spaaaaace', 'halloween'];
	let selected = themes[0];
</script>

+++<svelte:head>
	<link rel="stylesheet" href="/stylesheets/{selected}.css" />
</svelte:head>+++

<h1>Welcome to my site!</h1>
```

> 서버 사이드 렌더링(SSR) 모드에서는 `<svelte:head>`의 내용이 나머지 HTML과 별도로 반환됩니다.
