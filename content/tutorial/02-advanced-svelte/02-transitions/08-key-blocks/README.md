---
title: 키 블록
---

키 블록(Key blocks)은 표현식의 값이 바뀌면 그 안의 내용을 지우고 다시 만듭니다. 이 기능은 DOM에 들어가고 나갈때 뿐만 아이라 값이 바뀔 때도 전환이 재생되게 하는데 유용합니다.

이 예시에서는 `transition.js`에 있는 `typewriter` 효과를 로딩 메시지, 즉 `i` 값이 바뀔 때마다 재생되게 합니다. `<p>` 요소를 키 블록으로 감싸보세요.

```svelte
/// file: App.svelte
+++{#key i}+++
	<p in:typewriter={{ speed: 10 }}>
		{messages[i] || ''}
	</p>
+++{/key}+++
```
