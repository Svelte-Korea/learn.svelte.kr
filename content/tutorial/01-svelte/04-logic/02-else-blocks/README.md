---
title: Else 블록
---

자바스크립트에서와 마찬가지로, `if` 블록에는 `else` 블록을 추가할 수 있습니다.

```svelte
/// file: App.svelte
{#if count > 10}
	<p>{count} is greater than 10</p>
+++{:else}
	<p>{count} is between 0 and 10</p>+++
{/if}
```

> `#` 문자는 항상 _블록 시작_ 태그를 나타냅니다. `/` 문자는 항상 _블록 종료_ 태그를 나타냅니다. `:` 문자는 `{:else}`에서와 같이 _블록 계속_ 태그를 나타냅니다. 걱정하지 마세요. 스벨트가 HTML에 추가한 문법을 거의 다 배웠습니다.
