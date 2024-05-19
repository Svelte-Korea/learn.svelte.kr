---
title: 문
---

We're not limited to declaring reactive _values_ — we can also run arbitrary _statements_ reactively. For example, we can log the value of `count` whenever it changes:

우리는 반응형 _값_ 선언에만 국한되지 않고 임의의 _문_ 을 반응형으로 실행할 수도 있습니다. 예를 들어 `count` 값이 변경될 때마다 이를 기록할 수 있습니다.

```js
/// file: App.svelte
let count = 0;

+++$: console.log(`the count is ${count}`);+++
```

문을 블록과 함께 쉽게 그룹화할 수 있습니다.

```js
/// file: App.svelte
$: +++{+++
	console.log(`the count is ${count}`);
	console.log(`this will also be logged whenever count changes`);
+++}+++
```

`if` 블록 앞에 `$:`를 넣을 수도 있습니다.

```js
/// file: App.svelte
$: +++if (count >= 10)+++ {
	alert('count is dangerously high!');
	count = 0;
}
```
