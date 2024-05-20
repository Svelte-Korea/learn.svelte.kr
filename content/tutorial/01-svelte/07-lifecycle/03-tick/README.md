---
title: tick
---

`tick` 함수는 다른 생명주기 함수와 달리, 컴포넌트가 처음 초기화될 때뿐만 아니라 언제든지 호출할 수 있습니다. 이는 대기 중인 상태 변경이 DOM에 적용되자마자 해결되는 프로미스를 반환합니다. (대기 중인 상태 변경이 없는 경우 즉시 해결됩니다.)

스벨트에서 컴포넌트 상태를 업데이트할 때, DOM은 즉시 업데이트되지 않습니다. 대신 다음 _마이크로태스크_ 까지 기다리며 다른 컴포넌트에서를 포함해 적용해야 할 다른 변경 사항이 있는지 확인합니다. 이렇게 하면 불필요한 작업을 피하고 브라우저가 작업을 더 효과적으로 배치할 수 있습니다.

이 예제에서 이러한 동작을 확인할 수 있습니다. 텍스트의 범위를 선택하고 탭 키를 누르세요. `<textarea>` 값이 변경되면 현재 선택이 지워지고 커서가 끝으로 이동하게 되어 불편합니다. 이를 `tick`을 불러와서,

```js
/// file: App.svelte
+++import { tick } from 'svelte';+++

let text = `Select some text and hit the tab key to toggle uppercase`;
```

`handleKeydown`의 끝에서 `this.selectionStart`와 `this.selectionEnd`를 설정하기 직전에 실행하여 해결할 수 있습니다.

```js
/// file: App.svelte
+++await tick();+++
this.selectionStart = selectionStart;
this.selectionEnd = selectionEnd;
```
