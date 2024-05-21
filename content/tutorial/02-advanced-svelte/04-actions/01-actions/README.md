---
title: Use 지시어
---

액션은 본질적으로 요소 수준의 생명주기 함수입니다. 다음과 같은 경우에 유용합니다:

- 서드파티 라이브러리와의 인터페이스
- 지연 로드된 이미지
- 툴팁
- 사용자 정의 이벤트 핸들러 추가

이 앱에서는 `<canvas>`에 낙서를 하고 메뉴를 통해 색상과 브러시 크기를 변경할 수 있습니다. 하지만 메뉴를 열고 Tab 키로 옵션을 순환하면 포커스가 모달 내부에 _갇히지_ 않는 것을 곧 알게 될 것입니다.

이 문제를 액션으로 해결할 수 있습니다. `actions.js`에서 `trapFocus`를 가져옵시다.

```svelte
/// file: App.svelte
<script>
	import Canvas from './Canvas.svelte';
	+++import { trapFocus } from './actions.js';+++

	const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet', 'white', 'black'];
	let selected = colors[0];
	let size = 10;

	let showMenu = true;
</script>
```

그런 다음 `use:` 지시어를 사용하여 메뉴에 추가합시다.

```svelte
/// file: App.svelte
<div class="menu" +++use:trapFocus+++>
```

이제 `actions.js`의 `trapFocus` 함수를 살펴봅시다. 노드가 DOM에 마운트될 때 액션 함수는 `node`(이 경우 `<div class="menu">`)와 함께 호출되며, `destroy` 메서드가 있는 액션 객체를 반환할 수 있습니다.

먼저, Tab 키 입력을 가로채는 이벤트 리스너를 추가합시다.

```js
/// file: actions.js
focusable()[0]?.focus();

+++node.addEventListener('keydown', handleKeydown);+++
```

다음으로, 노드가 마운트 해제될 때 이벤트 리스너를 제거하고 요소가 마운트됐던 위치에 포커스를 복원하는 등의 정리 작업을 해야 합니다.

```js
/// file: actions.js
focusable()[0]?.focus();

node.addEventListener('keydown', handleKeydown);

+++return {
	destroy() {
		node.removeEventListener('keydown', handleKeydown);
		previous?.focus();
	}
};+++
```

이제 메뉴를 열면 Tab 키로 옵션을 순환할 수 있습니다.

