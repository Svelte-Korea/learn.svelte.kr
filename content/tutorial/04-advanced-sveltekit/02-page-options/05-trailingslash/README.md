---
title: 후행 슬래시
---

두 개의 URL `/foo`와 `/foo/`는 동일해 보일 수 있지만 실제로는 다릅니다. `./bar`와 같은 상대적인 URL을 사용하는 경우 `/foo`는 `/bar`로 해석되고, `/foo/`는 `/foo/bar`로 해석됩니다. 검색 엔진은 이를 별개의 항목으로 처리하며, 이는 SEO에 부정적인 영향을 미칠 수 있습니다.

간단히 말해서, 후행 슬래시에 대해 느슨한 접근은 좋지 않습니다. 기본적으로 스벨트킷은 마지막 슬래시를 제거합니다. 즉, `/foo/` 요청이 `/foo`로 리다이렉션된다는 의미입니다.

후행 슬래시가 항상 존재하도록 하려면 `trailingSlash`에 옵션을 지정할 수 있습니다.

```js
/// file: src/routes/always/+page.server.js
export const trailingSlash = 'always';
```

두 경우를 모두 수용하려면 `'ignore'`를 사용하세요. (권장되지 않음)

```js
/// file: src/routes/ignore/+page.server.js
export const trailingSlash = 'ignore';
```

기본값은 `'never'` 입니다.

후행 슬래시 적용 여부는 사전 렌더링에 영향을 미칩니다. `/always/` 같은 URL은 디스크에 `always/index.html` 로 저장되는 반면, `/never` 같은 URL은 `never.html`로 저장됩니다.
