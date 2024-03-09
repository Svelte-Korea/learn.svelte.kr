---
title: 커스텀 CSS 전환
---

`svelte/transition` 모듈에는 몇 가지 전환이 내장되어 있지만, 자신만의 전환 또한 쉽게 만들 수 있습니다. 예시로 `fade` 전환의 코드를 다뤄보겠습니다.

```js
/// no-file
function fade(node, { delay = 0, duration = 400 }) {
	const o = +getComputedStyle(node).opacity;

	return {
		delay,
		duration,
		css: (t) => `opacity: ${t * o}`
	};
}
```

이 함수는 전환이 적용될 노드와 내부로 전달될 다른 파라미터들 두 개의 인자를 받아 아래 속성들이 적용된 전환 객체를 반환합니다.

- `delay` — 전환이 시작하기까지 걸리는 시간(milliseconds 단위)
- `duration` — 전환의 길이(milliseconds 단위)
- `easing` — `p => t` 이징 함수.([트윈](/tutorial/tweens) 챕터를 참고하세요.)
- `css` — `u === 1 - t`인 `(t, u) => css` 함수.
- `tick` — 노드에 영향을 주는 `(t, u) => {...}` 함수.

`t` 값은 등장의 첫 시점이나 퇴장의 마지막 시점에 `0`이 됩니다. 등장의 마지막과 퇴장의 첫 시점에는 `1`이 됩니다.

대부분의 경우 `tick` 속성을 반환하면 _안되고_ `css` 속성을 반환해야 합니다. 왜냐하면 CSS 애니메이션은 UI 가 느려지는 걸 방지하기 위해 메인 스레드와 별개로 작동해야 하기 때문입니다. 스벨트는 전환을 '시뮬레이션' 하고 CSS 애니메이션을 생성 후 실행하도록 합니다.

예를 들어, `fade` 전환은 아래 같은 CSS 애니메이션을 만듭니다.

```css
/// no-file
0% { opacity: 0 }
10% { opacity: 0.1 }
20% { opacity: 0.2 }
/* ... */
100% { opacity: 1 }
```

어쨌든, 더 창의적인 것도 만들 수 있습니다. 진짜 쓸데없는 걸 한 번 만들어 봅시다.

```svelte
/// file: App.svelte
<script>
	import { fade } from 'svelte/transition';
	+++import { elasticOut } from 'svelte/easing';+++

	let visible = true;

	function spin(node, { duration }) {
		return {
			duration,
			css: t => +++{
				const eased = elasticOut(t);

				return `
					transform: scale(${eased}) rotate(${eased * 1080}deg);
					color: hsl(
						${Math.trunc(t * 360)},
						${Math.min(100, 1000 * (1 - t))}%,
						${Math.min(50, 500 * (1 - t))}%
					);`
			}+++
		};
	}
</script>
```

명심하세요. 큰 힘에는 큰 책임이 따릅니다.
