---
title: 오류 메시지 사용자 정의하기
---

이전 연습의 오류 페이지는 다소 정적입니다. 지원 채널에 도착한 사람들을 더 빨리 도울 수 있도록 오류 메시지를 표시하고 싶을 수 있습니다.

이를 위해 스벨트킷은 오류 및 상태 코드에 대한 정보를 포함하는 `$page.error`와 `$page.status`를 제공합니다. 이걸 `+error.svelte`에 추가해 봅시다.

```svelte
/// file: src/routes/+error.svelte
<script>
	+++import { page } from '$app/stores';+++

	let online = typeof navigator !== 'undefined'
		? navigator.onLine
		: true;
</script>

+++{#if $page.status === 404}
	<h1>Not found</h1>
{:else if !online}
	<h1>You're offline</h1>
{:else}
	<h1>Oops!</h1>
	<p>{$page.error.message}</p>
{/if}+++
```

이제 오류 메시지가 더 나아졌지만, `$page.error.message`는 항상 "Internal Error"를 포함합니다. 왜 그럴까요? 이는 스벨트킷이 실수로 오류 메시지의 일부로 민감한 정보를 표시하지 않도록 막아주기 때문입니다.

서버나 클라이언트의 데이터 로드 중에 예기치 않은 오류가 발생했을 때 실행되는 `hooks.server.js` 및 `hooks.client.js`에 `handleError` 훅을 구현하면 이를 사용자 정의할 수 있습니다.

```js
// hooks.server.js
export function handleError(+++{ error }+++) {
    return { message: error instanceof Error ? error.message : 'Internal Error' };
}
```

```js
// hooks.client.js
export function handleError(+++{ error }+++) {
    return { message: error instanceof Error ? error.message : 'Internal Error' };
}
```

이러한 훅에서 오류 보고 서비스를 호출할 수도 있습니다.

원하는 경우 오류 메시지 이상을 반환할 수 있습니다. 반환된 객체 형태가 어떻든 `message` 속성만 있으면 `$page.error`에서 사용할 수 있습니다. 이에 대한 자세한 내용과 이를 타입 안전하게 만드는 방법에 대해서는 [오류 문서](https://kit.svelte.dev/docs/errors)를 참조하십시오.

> 오류를 처리할 때, `Error` 객체라고 가정하지 않도록 주의하세요. 어떤 것이든 던져질 수 있습니다. 또한 너무 많은 정보를 전달하여 민감한 데이터를 노출하지 않도록 주의하십시오.
