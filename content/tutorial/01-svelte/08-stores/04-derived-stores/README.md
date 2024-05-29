---
title: 파생 스토어
---

`derived`를 사용하여 하나 이상의 _다른_ 스토어의 값을 기반으로 하는 스토어를 생성할 수 있습니다. 이전 예제를 바탕으로 페이지가 열린 시간을 나타내는 스토어를 만들 수 있습니다.

```js
/// file: stores.js
export const elapsed = derived(
    time,
    ($time) => +++Math.round(($time - start) / 1000)+++
);
```

> 여러 입력 스토어에서 스토어를 파생시키고, 반환하는 대신 값을 명시적으로 `set`할 수도 있습니다. 이는 비동기적으로 값을 유도할 때 유용합니다. 자세한 내용은 [API 참조](https://svelte.dev/docs#run-time-svelte-store-derived)를 참조하십시오.
