---
title: 프롭 뿌리기
---

이번 연습은 `PackageInfo.svelte`에서 기대하는 `version` 프롭을 지정하는 것을 잊은 상황입니다. 그래서 'version undefined'가 표시됩니다.

`version` 프롭을 추가하여 이를 _해결할_ _수_ _도_ 있습니다.

```svelte
/// file: App.svelte
<PackageInfo
    name={pkg.name}
	speed={pkg.speed}
    +++version={pkg.version}+++
	website={pkg.website}
/>
```

하지만 `pkg`의 속성이 컴포넌트가 기대하는 프롭과 일치하므로, `뿌리기(spread)`를 사용할 수 있습니다.

```svelte
/// file: App.svelte
<PackageInfo +++{...pkg}+++ />
```

> 반대로, `export`로 선언되지 않은 것들을 포함해 컴포넌트에 전달된 모든 프롭을 참조해야 하는 경우 `$$props`와 같이 직접 접근하여 사용할 수 있습니다. 최적화가 어렵기 때문에 권장되지 않지만, 드물게 사용됩니다.
