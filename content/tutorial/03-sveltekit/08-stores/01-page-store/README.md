---
title: page
---

[이전](writable-stores)에 배웠듯이, 스벨트 스토어는 한 컴포넌트에만 속해있지 않은 값을 넣는 곳입니다.

스벨트킷은 `$app/stores` 모듈을 통해 기본 스토어를 제공합니다. 3가지 기본 스토어는 `page`, `navigating`, `updated`입니다. 가장 자주 사용하게 될 스토어는 page입니다. 이는 현재 페이지에 관한 정보를 제공하는 스토어입니다.

* `url` — 현재 페이지의 [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL)
* `params` — 현재 페이지의 [파라미터](params)
* `route` — 현재 라우트 정보를 표현하는 `id` 속성을 가진 오브젝트
* `status` — 현재 페이지의 HTTP 상태 코드
* `error` — 현재 페이지에 에러가 있는 경우에 에러 정보([나중에](error-basics) [배올 내용에서](handleerror) 더 자세히 다루겠습니다.)
* `data` — 모든 `load` 함수의 반환 값 정보가 결합된 현재 페이지를 위한 데이터
* `form` — [폼 액션](the-form-element)에서 반환된 데이터

다른 스토어와 마찬가지로, 이 값들은 `$` 접두어를 이름에 붙여서 참조할 수 있습니다. 예시로 현재 패스네임에 `$page.url.pathname`으로 접근할 수 있습니다.

```svelte
/// file: src/routes/+layout.svelte
+++<script>
	import { page } from '$app/stores';
</script>+++

<nav>
	<a href="/" +++aria-current={$page.url.pathname === '/'}+++>
		home
	</a>

	<a href="/about" +++aria-current={$page.url.pathname === '/about'}+++>
		about
	</a>
</nav>

<slot />
```
