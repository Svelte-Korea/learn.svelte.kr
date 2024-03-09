---
title: 전환 이벤트
---

전환의 시작과 끝을 알면 유용할 때가 많습니다. 스벨트는 다른 DOM 이벤트와 같이 처리할 수 있는 이벤트를 발생시킵니다.

```svelte
/// file: App.svelte
<p
	transition:fly={{ y: 200, duration: 2000 }}
	+++on:introstart={() => status = 'intro started'}
	on:outrostart={() => status = 'outro started'}
	on:introend={() => status = 'intro ended'}
	on:outroend={() => status = 'outro ended'}+++
>
	Flies in and out
</p>
```
