---
title: 커스텀 JS 전환
---

전환을 만드는데 CSS를 사용하는 것이 일반적으로 권장되긴 하지만, 자바스크립트 없이 만들 수 없는 효과도 있습니다. 타자기 효과가 그 예시입니다.

```js
/// file: App.svelte
function typewriter(node, { speed = 1 }) {
	const valid = node.childNodes.length === 1 && node.childNodes[0].nodeType === Node.TEXT_NODE;

	if (!valid) {
		throw new Error(`This transition only works on elements with a single text node child`);
	}

	+++const text = node.textContent;
	const duration = text.length / (speed * 0.01);

	return {
		duration,
		tick: (t) => {
			const i = Math.trunc(text.length * t);
			node.textContent = text.slice(0, i);
		}
	};+++
}
```
