---
title: 할당
---

스벨트의 중심에는 DOM을 애플리케이션 상태와 동기화 상태로 유지하기 위한 강력한 _반응성_ 시스템(예: 이벤트에 대한 응답)이 있습니다.

이를 확인하려면 먼저 이벤트 핸들러를 연결해야 합니다 (이에 대해서는 [나중에](/tutorial/dom-events) 배울 것입니다.)

```svelte
/// file: App.svelte
<button +++on:click={increment}+++>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>
```

`increment` 함수 내에서 우리가 해야 하는 일은 `count` 값을 변경하는 것뿐입니다.

```js
/// file: App.svelte
function increment() {
	+++count += 1;+++
}
```

스벨트는 DOM을 업데이트해야 함을 알려주는 일부 코드를 사용하여 이 할당을 `계측`합니다.
