---
title: <form> 요소
---

[데이터 로딩](page-data) 챕터에서는 서버에서 브라우저로 데이터를 가져오는 방법을 살펴보았습니다. 데이터를 반대 방향으로 보내는 경우도 있는데, 이 때 웹 플랫폼에서 데이터를 전송하는 방법으로 `<form>`을 사용합니다.

todo 앱을 만들어 봅시다. 이미 `src/lib/server/database.js`에 메모리 내 데이터베이스가 설정되어 있고, `src/routes/+page.server.js`의 load 함수는 [`cookies`](https://kit.svelte.dev/docs/load#cookies) API를 사용하여 각 사용자마다 할 일 목록을 가질 수 있도록 합니다. 하지만 새로운 할 일을 만들기 위해 `<form>`을 추가해야 합니다.

```svelte
/// file: src/routes/+page.svelte
<h1>todos</h1>

+++<form method="POST">
	<label>
		add a todo:
		<input
			name="description"
			autocomplete="off"
		/>
	</label>
</form>+++

<ul class="todos">
```

`<input>`에 무언가를 입력하고 엔터를 누르면, `method="POST"` 속성으로 브라우저가 현재 페이지로 POST 요청을 보냅니다. 그러나 POST 요청을 처리할 서버 측 *액션*을 만들지 않았기 때문에 오류가 발생합니다. 이제 만들어 봅시다.

```js
/// file: src/routes/+page.server.js
import * as db from '$lib/server/database.js';

export function load({ cookies }) {
	// ...
}

+++export const actions = {
	default: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}
};+++
```

`request`는 표준 [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) 객체입니다.따라서 `await request.formData()`는 [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData) 인스턴스를 반환합니다.
Enter를 누르면 데이터베이스가 업데이트되고, 페이지가 새 데이터로 리로드됩니다.

`fetch` 코드나 그와 유사한 코드를 작성할 필요가 없다는 점에 유의하세요. 데이터는 자동으로 업데이트됩니다. 그리고 `<form>` 요소를 사용하고 있기 때문에 JavaScript가 비활성화되거나 사용할 수 없는 경우에도 이 앱이 작동할 것입니다.
