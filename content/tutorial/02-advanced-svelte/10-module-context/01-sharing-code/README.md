---
title: 코드 공유하기
---

지금까지 본 모든 예제에서 `<script>` 블록은 각 컴포넌트 인스턴스가 초기화될 때 실행되는 코드를 포함합니다. 대부분의 컴포넌트에 대해서는 이걸로 충분합니다.

아주 가끔, 개별 컴포넌트 인스턴스 외부에서 코드를 실행해야 할 필요가 있습니다. 예를 들어, [이전 연습](media-elements)의 사용자 정의 오디오 플레이어로 돌아가서, 네 개의 트랙을 동시에 재생할 수 있습니다. 하나를 재생할 때 다른 모든 것을 중지하면 더 좋을 것입니다.

이를 위해 `<script context="module">` 블록을 선언할 수 있습니다. 이 안에 포함된 코드는 컴포넌트가 인스턴스화될 때가 아니라, 모듈이 처음 평가될 때 한 번 실행됩니다. 이를 `AudioPlayer.svelte`의 맨 위에 배치합시다. (이는 _별도의_ 스크립트 태그입니다.)

```svelte
/// file: AudioPlayer.svelte
+++<script context="module">
	let current;
</script>+++
```

이제 상태 관리를 하지 않고도 컴포넌트들이 서로 '대화'할 수 있습니다.

```svelte
/// file: AudioPlayer.svelte
<audio
	src={src}
	bind:currentTime={time}
	bind:duration
	bind:paused
+++	on:play={(e) => {
		const audio = e.currentTarget;

		if (audio !== current) {
			current?.pause();
			current = audio;
		}
	}}+++
	on:ended={() => {
		time = 0;
	}}
/>
```
