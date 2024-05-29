---
title: Select 요소 바인딩
---

`<select>` 요소에서도 `bind:value`를 사용할 수 있습니다.

```svelte
/// file: App.svelte
<select
    +++bind:+++value={selected}
    on:change={() => answer = ''}
>
```

`<option>` 값이 문자열이 아닌 객체라는 점에 주의하세요. 스벨트는 이를 문제 삼지 않습니다.

> `selected`의 초기 값을 설정하지 않았기 때문에, 바인딩은 이를 기본값(목록의 첫 번째 값)으로 자동 설정합니다. 하지만 바인딩이 초기화될 때까지 `selected`는 undefined 상태이므로, 템플릿에서 `selected.id` 등을 맹목적으로 참조할 수 없다는 점을 주의하세요.
