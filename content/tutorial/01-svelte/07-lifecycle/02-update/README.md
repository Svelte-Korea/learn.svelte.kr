---
title: beforeUpdate와 afterUpdate
---

`beforeUpdate` 함수는 DOM이 업데이트되기 직전에 작업을 예약합니다. `afterUpdate`는 그 반대 역할을 하며, DOM이 데이터와 동기화된 후에 코드를 실행하는 데 사용됩니다.

이 둘을 함께 사용하면 요소의 스크롤 위치를 업데이트하는 것과 같이 순수한 상태 기반 방법으로는 달성하기 어려운 작업을 명령적으로 수행할 수 있어 유용합니다.

이 [Eliza](https://en.wikipedia.org/wiki/ELIZA) 챗봇은 채팅 창을 계속 스크롤해야 해서 사용하기 불편합니다. 이를 해결해 봅시다.

```js
/// file: App.svelte
let div;
+++let autoscroll = false;+++

beforeUpdate(() => {
+++	if (div) {
		const scrollableDistance = div.scrollHeight - div.offsetHeight;
		autoscroll = div.scrollTop > scrollableDistance - 20;
	}+++
});

afterUpdate(() => {
+++	if (autoscroll) {
		div.scrollTo(0, div.scrollHeight);
	}+++
});
```

`beforeUpdate`는 컴포넌트가 마운트되기 전에 처음 실행되므로, `div`의 속성을 읽기 전에 `div`가 존재하는지 확인해야 합니다.
