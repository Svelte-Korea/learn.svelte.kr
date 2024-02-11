---
title: 쿠키 읽고 쓰기
---

[`setHeaders`](headers) 함수는 `Set-Cookie` 헤더를 다루는 데 사용할 수 없습니다. 그 대신에, `cookies` API를 사용해야 합니다..

`load` 함수 안에서, `cookies.get(name, options)`을 이용해 쿠키를 읽을 수 있습니다.

```js
/// file: src/routes/+page.server.js
export function load(+++{ cookies }+++) {
	+++const visited = cookies.get('visited');+++

	return {
		visited: visited === 'true'
	};
}
```

쿠키를 설정할 때는 `cookies.set(name, value, options)`를 사용합니다. 쿠키를 세팅할 때, `path`를 명시적으로 설정하는 것을 강력하게 권장합니다. 왜냐하면 브라우저의 기본 정책이, 조금 불편하게 쿠키를 현재 경로의 부모에 설정하기 때문입니다.

```js
/// file: src/routes/+page.server.js
export function load({ cookies }) {
	const visited = cookies.get('visited');

	+++cookies.set('visited', 'true', { path: '/' });+++

	return {
		visited: visited === 'true'
	};
}
```

이제, iframe을 다시 불러오면, `Hello stranger!`는 `Hello friend!`가 되어 있을 것입니다.

`cookies.set(name, ...)`를 호출하는 것은 `Set-Cookie` 헤더를 변경하게 하지만, 쿠키의 내부 맵 _또한_ 업데이트 됩니다. 이후 같은 요청에서는 업데이트 된 값을 반환됩니다. 내부적으로는, `cookies` API는 유명한 `cookie` 패키지를 사용하며, `cookies.get`과 `cookies.set` 에 전달되는 옵션들은 `cookie` [문서](https://github.com/jshttp/cookie#api)의 `serialize`와 `cookie`에 대응됩니다. 스벨트킷은 쿠키 보안을 위해 다음 값을들 기본값으로 설정해 놓았습니다.

```js
/// no-file
{
	httpOnly: true,
	secure: true,
	sameSite: 'lax'
}
```
