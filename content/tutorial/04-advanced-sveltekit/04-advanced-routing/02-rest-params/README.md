---
title: 나머지 매개변수
path: /how
focus: /src/routes/[path]/+page.svelte
---

경로 세그먼트의 수를 알 수 없다면 자바스크립트의 [나머지 매개변수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters)와 비슷한 형태인 `[...rest]` 매개변수를 사용할 수 있습니다.

`src/routes/[path]`를 `src/routes/[...path]`로 변경하세요. 이렇게 하면 해당 라우트가 모든 경로와 일치하게 됩니다.

> 다른 경로들이 먼저 테스트되고, 그 경로들에 일치하지 않을 경우에 이 라우트가 사용됩니다. 이는 나머지 매개변수가 모든 경우를 처리하여 'catch-all' 역할을 한다는 뜻입니다. 예를 들어, `/categories/...`내의 페이지에 사용자 정의 404 페이지가 필요한 경우 다음과 같은 파일을 추가할 수 있습니다.
>
> ```diff
> src/routes/
> ├ categories/
> │ ├ animal/
> │ ├ mineral/
> │ ├ vegetable/
> +│ ├ [...catchall]/
> +│ │ ├ +error.svelte
> +│ │ └ +page.server.js
> ```
>
> `+page.server.js` 파일의 `load` 함수 안에 `throw error(404)`를 추가하세요.

나머지 파라미터가 끝에 위치할 필요는 없습니다. 예를 들어 `/items/[...path]/edit` 또는 `/items/[...path].json` 과 같이 위치할 수도 있습니다.