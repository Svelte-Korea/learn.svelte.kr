---
title: Await 블록
---

대부분의 웹 애플리케이션은 어느 시점에서 비동기 데이터를 처리해야 합니다. 스벨트는 마크업 내에서 직접[promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)의 값을 _await_ 하는 것을 쉽게 만들어 줍니다:

```svelte
/// file: App.svelte
+++{#await promise}+++
	<p>...waiting</p>
+++{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}+++
```

> 가장 최근의 `promise`만 고려되므로, 경쟁 조건에 대해 걱정할 필요가 없습니다.

promise가 거부되지 않는다는 것을 알고 있다면, `catch` 블록을 생략할 수 있습니다. 또한 promise가 해결될 때까지 아무것도 표시하고 싶지 않다면 첫 번째 블록을 생략할 수도 있습니다.

```svelte
/// no-file
{#await promise then number}
	<p>The number is {number}</p>
{/await}
```
