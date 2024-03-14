---
title: 사전 로딩
---

이 예제에서 `/slow-a` 와 `/slow-b` 경로는 모두 `load` 함수가 인위적으로 지연되어 있어 해당 경로로 이동하는 데 오랜 시간이 걸립니다.

항상 데이터를 빠르게 로드할 수는 없으나, 사용자가 특정 링크로 이동하려는 행동을 사전에 예측하고 해당 페이지에 필요한 데이터를 미리 로드하여 페이지 전환 속도를 높일 수 있습니다. `<a>` 요소에 `data-sveltekit-preload-data` 속성이 있는 경우, 데스크탑에서 사용자가 해당 링크 위로 마우스를 올리거나 모바일에서 탭하는 즉시 해당 링크와 관련된 데이터를 백그라운드에서 가져오고 로드하여 클라이언트 측 탐색 성능을 향상시킵니다. 첫 번째 링크에 이 속성을 추가해보세요.

```svelte
/// file: src/routes/+layout.svelte
<nav>
	<a href="/">home</a>
	<a href="/slow-a" +++data-sveltekit-preload-data+++>slow-a</a>
	<a href="/slow-b">slow-b</a>
</nav>
```

이제 `/slow-a`의 이동 속도가 눈에 띄게 빨라졌습니다. 링크를 클릭할 때가 아닌, 호버 또는 탭에서 내비게이션을 시작하는 것이 큰 차이가 없어 보일 수 있으나 실제로는 일반적으로 200ms 이상 차이가 납니다. 이는 충분히 빠르다고 느낄 수 있습니다.

`data-sveltekit-preload-data` 속성은 개별 링크에 추가하거나 링크 요소를 포함하고 있는 부모 요소에도 추가할 수 있습니다. 기본 프로젝트 템플릿에는 `<body>` 요소에 속성이 포함되어 있습니다.

```html
/// no-file
<body data-sveltekit-preload-data>
	%sveltekit.body%
</body>
```

속성에 다음 값 중 하나를 지정하여 동작을 사용자 정의할 수 있습니다.

- `"hover"` — 마우스가 링크 위에 올라갈 때 사전 로딩 시작(기본값, 모바일에서는 `"tap"` 으로 대체)
- `"tap"` — 탭할 때만 사전 로딩 시작
- `"off"` — 사전 로딩 비활성화

`data-sveltekit-preload-data`를 사용하면 페이지의 모든 내용이 로드되지만, 때로는 데이터 로드를 원치 않을 수도 있습니다(예를 들어, 경로 탐색이 발생하지 않을 것으로 예상하여 데이터를 로드하는 경우). `data-sveltekit-preload-code` 속성을 사용하면 데이터를 로드하지 않고 특정 경로에 필요한 JavaScript만 미리 로드할 수 있습니다. 이 속성은 다음 값을 가집니다.

- `"eager"` — 페이지의 모든 내용 미리 로드
- `"viewport"` — 뷰포트에 나타나는 모든 것을 미리 로드
- `"hover"` — 마우스가 링크 위에 올라갈 때 사전 로딩 시작(기본값, 모바일에서는 `"tap"` 으로 대체)
- `"tap"` — 탭할 때만 사전 로딩 시작
- `"off"` — 사전 로딩 비활성화

또한 프로그래밍적으로도 `$app/navigation`에서 가져온 `preloadCode` 와 `preloadData`를 사용하여 사전 로딩을 할 수도 있습니다.
```js
/// no-file
import { preloadCode, preloadData } from '$app/navigation';

// /foo로 이동하는 데 필요한 코드와 데이터를 미리 로드합니다
preloadData('/foo');

// /bar로 이동하는 데 필요한 코드를 미리 로드하지만 데이터는 로드하지 않습니다
preloadCode('/bar');
```