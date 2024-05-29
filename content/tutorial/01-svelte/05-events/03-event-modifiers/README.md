---
title: 이벤트 수정자
---

DOM 이벤트 핸들러에는 동작을 변경하는 _수정자_ 를 사용할 수 있습니다. 예를 들어, `once` 수정자가 있는 핸들러는 한 번만 실행됩니다:

```svelte
/// file: App.svelte
<button on:click+++|once+++={() => alert('clicked')}>
	Click me
</button>
```

수정자의 전체 목록은 다음과 같습니다.

- `preventDefault` — 핸들러를 실행하기 전에 `event.preventDefault()`를 호출합니다. 클라이언트 측 폼 처리에 유용합니다.
- `stopPropagation` — `event.stopPropagation()`을 호출하여 이벤트가 다음 요소에 도달하지 못하게 합니다.
- `passive` — 터치/휠 이벤트의 스크롤 성능을 향상시킵니다(이렇게 해도 안전한 경우 스벨트가 자동으로 추가합니다).
- `nonpassive` — 명시적으로 `passive: false`를 설정합니다.
- `capture` — [_버블링_](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling) 단계 대신 [_캡처_](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_capture) 단계에서 핸들러를 실행합니다.
- `once` — 처음 실행된 후 핸들러를 제거합니다.
- `self` — event.target이 요소 자체인 경우에만 핸들러를 실행합니다.
- `trusted` — `event.isTrusted`가 `true`인 경우, 즉, 어떤 JavaScript가 `element.dispatchEvent(...)`를 호출해서가 아니라 사용자 작업에 의해 이벤트가 실행된 경우에만 핸들러를 실행합니다.

수정자를 함께 연결할 수 있습니다. 다음이 그 예시입니다. `on:click|once|capture={...}`
