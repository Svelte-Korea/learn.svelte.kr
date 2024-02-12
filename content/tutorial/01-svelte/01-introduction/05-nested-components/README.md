---
title: Nested components
---

전체 앱을 하나의 컴포넌트만을 사용해 만드는 것은 실용적이지 않습니다. 대신에, 다른 파일에서 여러 컴포넌트를 불러와 마크업에서 사용할 수 있습니다.

`Nested.svelte`를 불러오는 `<script>` 태그를 `App.svelte`의 최상단에 추가하면 ...

```svelte
/// file: App.svelte
+++<script>
	import Nested from './Nested.svelte';
</script>+++
```

... 그리고 `<Nested />` 를 추가합니다.

```svelte
/// file: App.svelte
<p>This is a paragraph.</p>
+++<Nested />+++
```

`Nested.svelte`가 `<p>` 요소를 포함하지만, `App.svelte`의 스타일이 적용되지 않음을 유의하세요.

> HTML 요소와 구분을 위해, 컴포넌트 이름은 항상 대문자로 시작합니다.