---
title: 점진적 향상
---

우리 앱은 `<form>`을 사용하므로 사용자가 자바스크립트를 사용하지 않아도 작동합니다. ([이는 생각보다 자주 발생합니다.](https://kryogenix.org/code/browser/everyonehasjs.html)) 이는 앱이 강력하다는 의미이므로 좋습니다.

대부분의 경우 사용자는 자바스크립트를 사용 _합니다._ 이러한 경우 스벨트킷이 클라이언트 측 라우팅을 사용하여 `<a>` 요소를 점진적으로 향상시키는 것과 동일한 방식으로 경험을 _점진적으로 향상시킬_ 수 있습니다.

`$app/forms`에서 `enhance` 함수를 가져옵시다.

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { enhance } from '$app/forms';+++

	export let data;
	export let form;
</script>
```

그리고 `<form>` 요소에 `use:enhance` 지시어를 추가합시다.

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/create" +++use:enhance+++>
```

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/delete" +++use:enhance+++>
```

이걸로 충분합니다! 이제 자바스크립트가 활성화되면 `use:enhance`가 전체 페이지 리로드를 제외하고 브라우저 기본 동작을 에뮬레이트합니다. 이는 다음 동작들을 수행합니다.

- `form` 프롭을 업데이트합니다.
- 성공적인 응답 시 모든 데이터를 무효화하여 `load` 함수를 다시 실행합니다.
- 리디렉션 응답 시 새 페이지로 이동합니다.
- 오류가 발생하면 가장 가까운 오류 페이지를 렌더링합니다.

이제 페이지를 리로드하는 대신 업데이트하므로 전환 같은 작업이 추가로 가능합니다.

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { fly, slide } from 'svelte/transition';+++
	import { enhance } from '$app/forms';

	export let data;
	export let form;
</script>
```

```svelte
/// file: src/routes/+page.svelte
<li +++in:fly={{ y: 20 }} out:slide+++>...</li>
```
