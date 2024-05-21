---
title: <svelte:self>
---

스벨트는 다양한 내장 요소를 제공합니다. 그 중 첫 번째인 `<svelte:self>`는 컴포넌트가 자신을 재귀적으로 포함할 수 있게 합니다.

이는 이 폴더 트리 뷰와 같이 폴더가 _다른_ 폴더를 포함할 수 있는 경우에 유용합니다. `Folder.svelte`에서 다음과 같이 하기를 원하더라도,

```svelte
/// file: Folder.svelte
{#if file.files}
	<Folder {...file}/>
{:else}
	<File {...file}/>
{/if}
```

모듈은 자신을 import할 수 없기 때문에 이는 불가능합니다. 대신, `<svelte:self>`를 사용할 수 있습니다.

```svelte
/// file: Folder.svelte
{#if file.files}
	+++<svelte:self {...file}/>+++
{:else}
	<File {...file}/>
{/if}
```

