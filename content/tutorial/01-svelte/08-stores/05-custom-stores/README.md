---
title: Custom stores
---

As long as an object correctly implements the `subscribe` method, it's a store. Beyond that, anything goes. It's very easy, therefore, to create custom stores with domain-specific logic.

For example, the `count` store from our earlier example could include `increment`, `decrement` and `reset` methods and avoid exposing `set` and `update`:

```js
/// file: stores.js
function createCount() {
	const { subscribe, set, update } = writable(0);

	return {
		subscribe,
		increment: () => +++update((n) => n + 1)+++,
		decrement: () => +++update((n) => n - 1)+++,
		reset: () => +++set(0)+++
	};
}
```

---
title: 사용자 정의 스토어
---

객체가 `subscribe` 메서드를 올바르게 구현하기만 하면 스토어가 됩니다. 그 외에는 상관 없습니다. 따라서 도메인별 로직을 가진 사용자 정의 스토어를 쉽게 만들 수 있습니다.

예시로, 이전 예제의 `count` 스토어는 `increment`, `decrement`, `reset` 메서드를 포함하고 `set` 및 `update`의 노출을 피할 수 있습니다.

```js
/// file: stores.js
function createCount() {
	const { subscribe, set, update } = writable(0);

	return {
		subscribe,
		increment: () => +++update((n) => n + 1)+++,
		decrement: () => +++update((n) => n - 1)+++,
		reset: () => +++set(0)+++
	};
}
```
