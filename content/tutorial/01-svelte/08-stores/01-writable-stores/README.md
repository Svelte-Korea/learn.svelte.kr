---
title: 쓰기 가능한 스토어
---

모든 애플리케이션 상태가 애플리케이션의 컴포넌트 계층 내에 있는 것은 아닙니다. 때로는 여러 관련 없는 컴포넌트나 일반 JavaScript 모듈에서 접근해야 하는 값이 있을 수 있습니다.

스벨트에서는 이를 _스토어_ 로 처리합니다. 스토어는 스토어 값이 변경될 때마다 관련 당사자가 알림을 받을 수 있는 `subscribe` 메서드를 가진 객체일 뿐입니다. `App.svelte`에서 `count`는 스토어이며, `count.subscribe` 콜백에서 `count_value`를 설정하고 있습니다.

`stores.js`를 열어 `count`의 정의를 확인하세요. 이는 _쓰기 가능한(writable)_ 스토어로, `subscribe` 메서드 외에도 `set` 및 `update` 메서드를 가지고 있습니다.

이제, `Incrementer.svelte`에서 `+` 버튼을 연결합시다.

```js
/// file: Incrementer.svelte
function increment() {
	+++count.update((n) => n + 1);+++
}
```

`+` 버튼을 클릭하면 이제 count가 업데이트됩니다. `Decrementer.svelte`에서는 반대로 구현하세요.

마지막으로, `Resetter.svelte`에서 `reset`을 구현합시다.

```js
/// file: Resetter.svelte
function reset() {
	+++count.set(0);+++
}
```

