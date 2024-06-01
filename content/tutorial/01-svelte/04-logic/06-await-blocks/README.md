---
title: Await 블록
---

대부분의 웹 애플리케이션은 어느 시점에서 비동기 데이터를 처리해야 합니다. 스벨트에서는 마크업 내에서 직접 [promises](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Guide/Using_promises)의 값을 _기다리는(await)_ 것을 쉽게 처리할 수 있습니다.

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

> 가장 최근 `프로미스(promise)` 만 고려되므로, 레이스 컨디션을 걱정할 필요가 없습니다.

프로미스가 거부(reject)되지 않는 상황이면, `catch` 블록은 없어도 됩니다. 프로미스가 수행(resolve) 되기 전까지 아무것도 보여주기 싫다면 첫 블록을 제거해 버리면 됩니다.

```svelte
/// no-file
{#await promise then number}
	<p>The number is {number}</p>
{/await}
```
