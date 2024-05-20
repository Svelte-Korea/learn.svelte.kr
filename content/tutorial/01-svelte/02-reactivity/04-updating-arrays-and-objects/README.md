---
title: 배열과 객체 업데이트하기
---

스벨트의 반응성은 할당에 의해 트리거되기 때문에 `push` 및 `splice`와 같은 배열 메서드를 사용하면 자동으로 업데이트가 발생하지 않습니다. 예를 들어, 'Add a number' 버튼을 클릭하면 `addNumber` 내에서 `numbers.push(...)`를 호출하고 있음에도 아무 작업도 수행되지 않습니다.

이 문제를 해결하는 방법으로는 할당을 다시하는 방법이 있습니다.

```js
/// file: App.svelte
function addNumber() {
	numbers.push(numbers.length + 1);
	+++numbers = numbers;+++
}
```

하지만 좀 더 관용적인 해결책이 있습니다.

```js
/// file: App.svelte
function addNumber() {
	numbers = +++[...numbers, numbers.length + 1];+++
}
```

유사한 패턴을 사용하여 `pop`, `shift`, `unshift` 및 `splice`를 대체할 수 있습니다.

`obj.foo += 1` 또는 `array[i] = x`과 같은 배열과 객체의 _속성_ 에 대한 할당은 값 자체에 대한 할당과 동일한 방식으로 작동합니다.

```js
/// file: App.svelte
function addNumber() {
	numbers[numbers.length] = numbers.length + 1;
}
```

경험적으로, 업데이트된 변수의 이름이 할당 왼쪽에 나타나야 합니다. 예시를 들어보겠습니다.

```js
/// no-file
const obj = { foo: { bar: 1 } };
const foo = obj.foo;
foo.bar = 2;
```

이 경우 `obj = obj`로 후속 작업을 수행하지 않는 한 `obj.foo.bar`에 대한 반응성이 나타나지 않습니다.
