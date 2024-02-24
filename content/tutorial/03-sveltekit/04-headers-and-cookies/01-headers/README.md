---
title: 헤더 설정하기
---

`load` 함수 안, 그리고 이후에 다룰 [폼 액션](the-form-element), [훅](handle) 과 [API 라우트](get-handlers) 에서, `setHeaders` 함수를 통해 당연하게도 응답에 대한 헤더를 설정할 수 있습니다.

가장 흔한 사용법은 이걸 이용해서 [캐싱 컨트롤(`Cache-Control`)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) 응답 헤더를 통한 캐싱 동작 변경입니다. 그렇지만 여기서는 덜 유익하지만, 더 드라마틱한 걸 해보겠습니다.

```js
/// file: src/routes/+page.server.js
export function load(+++{ setHeaders }+++) {
+++	setHeaders({
		'Content-Type': 'text/plain'
	});+++
}
```

(iframe을 다시 불러와야 적용될 수도 있습니다.)
