---
title: 전환 지연
---

스벨트 전환 엔진에는 전환을 _지연하여_ 여러 요소 간의 전환을 조정하는 강력한 기능이 있습니다.

한 목록에서 클릭하면 반대편 목록으로 이동하는 이 한 쌍의 투두 리스트를 봅시다. 현실 세계에는 객체는 그렇게 작동하지 않습니다. 한쪽에서 사라져서 다른 곳으로 나타나는 게 아니라, 일련의 위치를 따라 이동합니다. 모션은 사용자가 앱에서 어떤 일이 일어나고 있는지 이해하도록 도와줍니다.

`crossfade` 함수를 이용해 이 효과를 얻을 수 있습니다. `transition.js`에서 보다시피, 이 함수는 `send`와 `receive` 라는 한 쌍의 전환을 만듭니다. 요소가 '보내질(sent)' 때, `받는(receive)` 요소를 찾아 해당 요소의 상대 위치로 변환해 사라지고 나타는 전환을 만듭니다. 요소가 `받을(receive)` 때 에는 반대 일이 생깁니다. 대응되는 요소가 없으면, `fallback` 전환이 사용됩니다.

`TodoList.svelte` 열고, transition.js 에서 `send`와 `receive`를 불러옵시다.

```svelte
/// file: TodoList.svelte
<script>
	+++import { send, receive } from './transition.js';+++

	export let store;
	export let done;
</script>
```

그런 다음, `<li>` 요소에 적용합니다. `todo.id` 속성을 요소와 연결 짓는 키로 사용합시다.

```svelte
/// file: TodoList.svelte
<li
	class:done
	+++in:receive={{ key: todo.id }}+++
	+++out:send={{ key: todo.id }}+++
>
```

이제, 여러분이 항목을 클릭하면 자연스럽게 새로운 위치로 움직이게 되었습니다. 전환되지 않는 요소들이 어색하게 움직이는 문제는 다음 장에서 수정해 봅시다.
