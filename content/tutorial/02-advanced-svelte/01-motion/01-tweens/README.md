---
title: 트윈(Tweens)
---

기본적인 내용을 다 다뤘으니, 고급 스벨트 기술을 다뤄볼 차례입니다. 먼저 _모션(motion)_ 부터 시작하겠습니다.

값을 정하고 자동으로 DOM이 업데이트 되는 걸 보는 건 멋진 일입니다. 더 멋진 것도 있습니다. 그 값을 트위닝(Tweening) 하는 것입니다. 스벨트에는 애니메이션을 이용해 변화를 보여주는 부드러운 사용자 인터페이스를 만들기 위한 도구가 포함되어 있습니다.

`progress` 스토어를 `tweened` 스토어로 바꾸는 것부터 해봅시다.

```svelte
/// file: App.svelte
<script>
	import { +++tweened+++ } from 'svelte/+++motion+++';

	const progress = +++tweened+++(0);
</script>
```

버튼을 클릭하면 진행 바가 새로운 값으로 애니메이션과 함께 바뀝니다. 약간 딱딱하고 만족스럽지 않습니다. 이징(easing) 함수를 추가해야겠네요.

```svelte
/// file: App.svelte
<script>
	import { tweened } from 'svelte/motion';
	+++import { cubicOut } from 'svelte/easing';+++

	const progress = tweened(0, +++{
		duration: 400,
		easing: cubicOut
	}+++);
</script>
```

> `svelte/easing` 모듈은 [Penner easing equations](https://web.archive.org/web/20190805215728/http://robertpenner.com/easing/)을 내장하고 있습니다. 그 대신 직접 작성한 `p => t` 함수를 제공해도 됩니다. `p` 와 `t` 는 둘 다 0과 1 사이의 값입니다.

`tweened` 에 사용할 수 있는 모든 옵션은 다음과 같습니다.

- `delay` — 트윈(tween)이 시작하기 까지 걸리는 시간(milliseconds 단위)
- `duration` — 트윈 사이의 시간(milliseconds 단위)을 지정하거나 `(from, to) => milliseconds` 함수를 넣을 수 있습니다. 예를 들어, 더 큰 값 변화에 대해 더 긴 트윈(tween)이 지속되게 할 수 있습니다.
- `easing` — `p => t` 함수
- `interpolate` — 커스텀 `(from, to) => t => value` 함수로 임의의 값 사이를 보간하는 데 사용합니다. 기본적으로 Svelte 는 숫자, 날짜, 그리고 동형으로 생긴 배열과 오브젝트 값 사이를 보간할 것입니다  숫자, 날짜, 아니면 다른 유효한 배열과 오브젝트만 가지고 있는 한 말이죠. 만약 당신이, 예를 들어, 색깔 문자열이나, 변환 행렬을 다룬다면, 커스텀 보간을 입력할 수 있습니다.

이 옵션들을 `progress.set` 와 `progress.update`에 2번째 파라미터값으로 넣어줄 수 있습니다. 그 경우 기본값을 덮어 쓰게 됩니다. `set` 과 `update` 메쏘드는 프로미스(promise)를 반환하고, 이 프로미스는 트윈이 완료되는 시점에 resolve 됩니다.
