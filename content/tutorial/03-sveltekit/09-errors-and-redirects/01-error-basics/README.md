---
title: 기초
---

스벨트킷에는 _예상된_ 오류와 _예기치 않은_ 오류, 이렇게 두 가지 종류의 오류가 있습니다.

예상된 오류는 `src/routes/expected/+page.server.js`에서처럼 `@sveltejs/kit`의 [`error`](https://kit.svelte.dev/docs/modules#sveltejs-kit-error) 헬퍼로 생성된 오류입니다.

```js
/// file: src/routes/expected/+page.server.js
import { error } from '@sveltejs/kit';

export function load() {
	throw error(420, 'Enhance your calm');
}
```

`src/routes/unexpected/+page.server.js`의 오류와 같은 다른 모든 오류는 예기치 않은 오류로 간주됩니다.

\```js
/// file: src/routes/unexpected/+page.server.js
export function load() {
	throw new Error('Kaboom!');
}
\```

예상된 오류를 던지는 건, 스벨트킷에게 '걱정하지 마세요, 저는 여기서 무엇을 하고 있는지 알고 있습니다'라고 말하는 것입니다. 반대로, 예기치 않은 오류는 앱의 버그입니다. 예기치 않은 오류가 발생하면 해당 메시지와 스택 추적이 콘솔에 기록됩니다.

> 이후 장에서 `handleError` 훅을 사용하여 사용자 정의 오류 처리를 추가하는 방법에 대해 배울 것입니다.

이 앱에서 링크를 클릭하면 중요한 차이점을 알 수 있습니다. 예상된 오류 메시지는 사용자에게 표시되지만, 예기치 않은 오류 메시지는 편집되어 일반적인 'Internal Error' 메시지와 500 상태 코드로 대체됩니다. 이는 오류 메시지에 민감한 데이터가 포함될 수 있기 때문입니다.

