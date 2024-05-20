---
title: Spread props
---

이번 연습에서는 `PackageInfo.svelte`에서 기대하는 `version` prop을 지정하는 것을 잊어버렸습니다. 그래서 'version undefined'가 표시됩니다.

`version` prop을 추가하여 이를 해결할 수 _있습니다_...

```svelte
/// file: App.svelte
<PackageInfo
    name={pkg.name}
	speed={pkg.speed}
    +++version={pkg.version}+++
	website={pkg.website}
/>
```

...하지만 `pkg`의 속성이 컴포넌트의 기대 props와 일치하므로, 이들을 컴포넌트에 대신 '뿌릴(spread)' 수 있습니다.

```svelte
/// file: App.svelte
<PackageInfo +++{...pkg}+++ />
```

> 반대로, `export`로 선언되지 않은 것들을 포함해 컴포넌트에 전달된 모든 props를 참조해야 하는 경우 `$$props`에 직접 접근하여 할 수 있습니다. 일반적으로 스벨트가 최적화하기 어렵기 때문에 권장되지 않지만, 드문 경우에 유용할 수 있습니다.
