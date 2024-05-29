---
title: 미디어 요소
---

<audio> 및 <video> 요소의 속성에 바인딩함으로써 `AudioPlayer.svelte`와 같은 사용자 정의 플레이어 UI 등을 쉽게 구축할 수 있습니다.

먼저, 바인딩과 함께 `<audio>` 요소를 추가합시다. `src`, `duration` 및 `paused`에 대해 축약형을 사용합니다.

```svelte
/// file: AudioPlayer.svelte
<div class="player" class:paused>
+++	<audio
		{src}
		bind:currentTime={time}
		bind:duration
		bind:paused
	/>+++

	<button
		class="play"
		aria-label={paused ? 'play' : 'pause'}
	/>
```

다음으로, `<button>`에 `paused`를 토글하는 이벤트 핸들러를 추가합시다.

```svelte
/// file: AudioPlayer.svelte
<button
	class="play"
	aria-label={paused ? 'play' : 'pause'}
	+++on:click={() => paused = !paused}+++
/>
```

이제 우리 오디오 플레이어는 기본적인 기능을 갖추고 있습니다. 슬라이더를 드래그하여 트랙의 특정 부분으로 이동할 수 있는 기능을 추가해 봅시다. 슬라이더의 `pointerdown` 핸들러 내에 `time`을 업데이트할 수 있는 `seek` 함수가 있습니다.

```js
/// file: AudioPlayer.svelte
function seek(e) {
	const { left, width } = div.getBoundingClientRect();

	let p = (e.clientX - left) / width;
	if (p < 0) p = 0;
	if (p > 1) p = 1;

	+++time = p * duration;+++
}
```

트랙이 끝나면 되감기 기능을 추가합시다.

```svelte
/// file: AudioPlayer.svelte
<audio
	{src}
	bind:currentTime={time}
	bind:duration
	bind:paused
+++	on:ended={() => {
		time = 0;
	}}+++
/>
```

`<audio>` 및 `<video>` 요소에 대한 전체 바인딩은 이하 7개의 _읽기 전용_ 바인딩과

- `duration` (readonly) — 총 지속 시간(초)
- `buffered` (readonly) — `{start, end}` 객체 배열
- `seekable` (readonly) — 위와 동일
- `played` (readonly) — 위와 동일
- `seeking` (readonly) — 불리언 값
- `ended` (readonly) — 불리언 값
- `readyState` (readonly) — 0에서 4 사이의 숫자(포함)

이하 5개의 _양방향_ 바인딩입니다.

- `currentTime` — 재생 헤드의 현재 위치(초)
- `playbackRate` — 속도 조절 (`1`이 '기본 상태')
- `paused` — 이 바인딩은 설명이 필요 없습니다
- `volume` — 0에서 1 사이의 값
- `muted` — `true`는 음소거된 상태를 나타내는 불리언 값

비디오에는 추가로 `videoWidth` 및 `videoHeight` 읽기 전용 바인딩이 있습니다.
