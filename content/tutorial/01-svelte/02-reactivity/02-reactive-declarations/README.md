---
title: 선언
---

스벨트는 구성 요소의 상태가 변경되면 DOM을 자동으로 업데이트합니다. 종종 구성 요소 상태의 일부 부분은 _다른_ 부분에서 계산되고 변경될 때마다 다시 계산되어야 합니다.(예: `firstname` 및 `lastname`에서 파생된 `fullname`)

이를 위해 _반응적 선언_ 이 있습니다. 이는 다음과 같습니다.

```js
/// file: App.svelte
let count = 0;
+++$: doubled = count * 2;+++
```

반응문이 선언되지 않은 변수에 대한 할당으로만 구성된 경우 Svelte는 사용자를 대신하여 `let` 선언을 삽입합니다.

> 조금 낯설게 보이더라도 걱정하지 마세요. 이는 통상적이지 않지만 [유효한](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label) JavaScript이며, Svelte는 '언제든지 참조된 값이 변경될 때마다 이 코드를 다시 실행'한다는 의미로 해석합니다. 여기에 익숙해지면 다시 돌아가실 수 없을 겁니다.

마크업에 `doubled`를 사용해 보겠습니다.

```svelte
/// file: App.svelte
<button>...</button>

+++<p>{count} doubled is {doubled}</p>+++
```

물론, 마크업에 대신 `{count * 2}`를 쓸 수도 있습니다. 반드시 반응형 값을 사용할 필요는 없습니다. 반응형 값은 여러 번 참조해야 하거나 _다른_ 반응형 값에 의존하는 값이 있을 때 특히 유용합니다.

> 반응형 선언과 명령문은 다른 스크립트 코드 이후, 구성 요소 마크업이 렌더링되기 전에 실행됩니다.