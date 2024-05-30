---
title: 기본
---

스벨트킷에는 _예상된(expected)_ 에러와 _예상치 못한(unexpected)_ 에러, 두 종류의 에러가 있습니다.

`@sveltejs/kit`에서 제공하는 [`error`](https://kit.svelte.dev/docs/modules#sveltejs-kit-error) 헬퍼 함수를 이용하면 예상된 에러를 만들 수 있습니다. `src/routes/expected/+page.server.js`를 살펴봅시다.

```js
/// file: src/routes/expected/+page.server.js
import { error } from '@sveltejs/kit';

export function load() {
	throw error(420, 'Enhance your calm');
}
```

다른 모든 에러는 예상치 못한 에러로 취급됩니다. `src/routes/unexpected/+page.server.js` 에 예시가 있습니다.

```js
/// file: src/routes/unexpected/+page.server.js
export function load() {
	throw new Error('Kaboom!');
}
```

예상된 에러 발생을 사용하면 "무슨 일을 하는지 알고 있으니 걱정할 필요가 없어."라 스벨트킷에게 알려주게 됩니다. 반면에, 스벨트킷은 예상치 못한 에러를 의도하지 않은 버그의 존재로 처리합니다. 예상치 못한 에러가 발생하면, 에러 메시지와 스택 트레이스는 콘솔에 출력됩니다

> 나중 챕터에서 `handleError` 훅을 이용한 커스텀 에러 처리법을 배워보겠습니다.

앱 안의 링크들을 클릭해 봅시다. 중요한 차이가 있습니다. 예상된 에러는 메시지가 사용자에게 보입니다. 반면에, 예상치 못한 에러의 메시지는 일반적인 `Internal Error` 500 상태코드 메세지로 대체됩니다. 에러 정보에 담길 수 있는 민감한 정보를 감추기 위해서입니다.
