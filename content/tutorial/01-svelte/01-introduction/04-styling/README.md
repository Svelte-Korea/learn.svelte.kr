---
title: Styling
---

HTML에서와 같이, `<style>` 태그를 컴포넌트에 추가할 수 있습니다. `<p>` 요소에 스타일을 추가해 봅시다.

```svelte
/// file: App.svelte
<p>This is a paragraph.</p>

<style>
+++	p {
		color: goldenrod;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}+++
</style>
```

중요한 것은, 방금 작성한 규칙들은 _컴포넌트 범위에서만 적용_ 됩니다. 다읍 단계에서 보겠지만, 이는 실수로 앱의 다른 부분에서 `<p>` 요소의 스타일을 변경할 일이 없음을 의미합니다. 
