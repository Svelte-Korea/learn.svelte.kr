---
title: <svelte:options>
---

`<svelte:options>` 요소를 사용하여 컴파일러 옵션을 지정할 수 있습니다.

예제로 `immutable` 옵션을 사용해 보겠습니다. 이 앱에서 `<Todo>` 컴포넌트는 새 데이터를 받을 때마다 깜빡입니다. 항목을 클릭하면 `done` 상태가 토글되며 업데이트된 `todos` 배열이 생성됩니다. 이는 _다른_ `<Todo>` 항목도 깜빡이게 하지만, 실제로는 DOM에 아무런 변경도 일어나지 않습니다.

`<Todo>` 컴포넌트가 _불변_ 데이터를 기대하도록 하면 이를 최적화할 수 있습니다. 이는 `todo` 프롭(prop)을 절대로 _변경_ 하지 않겠다고 약속하는 것을 의미하며, 대신 변경 사항이 있을 때마다 새로운 todo 객체를 생성할 것입니다.

다음을 `Todo.svelte`의 맨 위에 추가하십시오.

```svelte
/// file: Todo.svelte
<svelte:options immutable={true} />
```

> 원하는 경우 `<svelte:options immutable/>`로 줄일 수 있습니다.

이제 항목을 클릭하여 todos를 토글할 때, 업데이트된 컴포넌트만 깜빡입니다.

여기서 설정할 수 있는 옵션은 다음과 같습니다:

- `immutable={true}` — 불변 데이터를 사용하므로, 컴파일러가 값이 변경되었는지 여부를 단순 참조 동등성 검사로 확인할 수 있습니다.
- `immutable={false}` — 기본값입니다. 스벨트는 가변 객체가 변경되었는지 여부에 대해 더 신중하게 판단합니다.
- `accessors={true}` — 컴포넌트의 프롭(props)에 대한 getter와 setter를 추가합니다.
- `accessors={false}` — 기본값입니다.
- `namespace="..."` — 이 컴포넌트가 사용될 네임스페이스, 가장 일반적으로 `"svg"`입니다.
- `customElement="..."` — 이 컴포넌트를 사용자 정의 요소로 컴파일할 때 사용할 이름입니다.

이 옵션에 대한 자세한 내용은 [API 참조](https://svelte.dev/docs)를 참조하십시오.
