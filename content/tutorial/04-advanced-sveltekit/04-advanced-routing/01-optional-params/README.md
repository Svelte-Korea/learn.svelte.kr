---
title: 선택적 매개변수
---

[라우팅](/tutorial/pages)에 대한 첫 번째 장에서 [동적 매개변수](/tutorial/params)를 사용하여 경로를 생성하는 방법을 배웠습니다.

때로는 매개변수를 선택적으로 만드는 것이 도움이 됩니다. 전형적인 예로는 `/fr/...`, `/de/...`와 같이 경로명을 사용하여 로케일을 결정하면서 기본 로케일도 가지려는 경우입니다.

이를 위해 이중 대괄호를 사용합니다. 디렉토리 `[lang]`의 이름을 `[[lang]]`로 변경하세요.

이제 앱은 빌드되지 않습니다.`src/routes/+page.svelte` 와 `src/routes/[[lang]]/+page.svelte` 둘 다 `/`와 일치하기 때문입니다. `src/routes/+page.svelte`를 삭제하세요. (에러 페이지를 복구하려면 앱을 다시 로드해야 할 수도 있습니다.)

마지막으로, `src/routes/[[lang]]/+page.server.js` 를 수정하여 기본 로케일을 지정하세요.

```js
/// file: src/routes/[[lang]]/+page.server.js
const greetings = {
	en: 'hello!',
	de: 'hallo!',
	fr: 'bonjour!'
};

export function load({ params }) {
	return {
		greeting: greetings[params.lang +++?? 'en'+++]
	};
}
```
