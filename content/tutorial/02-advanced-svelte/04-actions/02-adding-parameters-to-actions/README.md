---
title: 매개변수 더하기
---

전환 및 애니메이션과 마찬가지로 액션은 인자를 취할 수 있으며, 액션 함수는 해당 요소와 함께 호출됩니다.

이 연습에서는 [`Tippy.js`](https://atomiks.github.io/tippyjs/) 라이브러리를 사용하여 `<button>`에 툴팁을 추가하고자 합니다. 액션은 이미 `use:tooltip`으로 연결되어 있지만, 버튼을 가리키거나(또는 키보드로 포커스하면) 툴팁에 내용이 표시되지 않습니다.

먼저, 액션이 옵션을 받아 Tippy에 전달해야 합니다.

```js
/// file: App.svelte
function tooltip(node, +++options+++) {
	const tooltip = tippy(node, +++options+++);

	return {
		destroy() {
			tooltip.destroy();
		}
	};
}
```

그런 다음, 액션에 옵션을 전달해야 합니다.

```svelte
/// file: App.svelte
<button use:tooltip+++={{ content, theme: 'material' }}+++>
	Hover me
</button>
```

이제 툴팁이 거의 작동합니다. 다만 `<input>`의 텍스트를 변경하면 툴팁에 새로운 내용이 반영되지 않는데, 반환된 객체에 `update` 메서드를 추가하여 해결할 수 있습니다.

```js
/// file: App.svelte
function tooltip(node, options) {
	const tooltip = tippy(node, options);

	return {
+++		update(options) {
			tooltip.setProps(options);
		},+++
		destroy() {
			tooltip.destroy();
		}
	};
}
```
