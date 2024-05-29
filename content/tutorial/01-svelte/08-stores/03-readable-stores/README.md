---
title: 읽기 가능한 스토어
---

모든 스토어가 참조하는 사람에 의해 쓰기 가능할 필요는 없습니다. 예를 들어, 마우스 위치나 사용자의 지리적 위치를 나타내는 스토어가 있을 때, 외부에서 이러한 값을 설정할 수 있는 것은 말이 되지 않습니다. 이러한 경우에는 _읽기 가능한(readable)_ 스토어가 필요합니다.

`stores.js`를 여세요. `readable`의 첫 번째 인자는 초기 값으로, 아직 값이 없으면 `null` 또는 `undefined`일 수 있습니다. 두 번째 인자는 `set` 콜백을 받고 `stop` 함수를 반환하는 `start` 함수입니다. `start` 함수는 스토어가 첫 구독자를 얻을 때 호출되고, `stop`은 마지막 구독자가 구독을 해지할 때 호출됩니다.

```js
/// file: stores.js
export const time = readable(+++new Date()+++, function start(set) {
+++	const interval = setInterval(() => {
		set(new Date());
	}, 1000);+++

	return function stop() {
		+++clearInterval(interval);+++
	};
});
```
