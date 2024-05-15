---
title: 컴포넌트 처음 알아보기
---

스벨트에서 어플리케이션은 한 개 이상의 _컴포넌트 (components)_ 로 이루어져 있습니다. 컴포넌트는 재사용 가능한 독립적인 코드 블록으로, 함께 속해 있는 HTML, CSS 및 JavaScript를 '.svelte' 파일로 캡슐화하여 작성합니다. 오른쪽 코드 에디터에 열려 있는 `App.svelte`파일은 단순 컴포넌트입니다.

## 데이터 추가하기

정적 마크업만 렌더링하는 컴포넌트는 단순합니다. 데이터를 추가해 보겠습니다.

먼저, 컴포넌트에 스크립트 태그를 추가하고 `name` 변수를 선언합니다.

```svelte
/// file: App.svelte
+++<script>
	let name = 'Svelte';
</script>+++

<h1>Hello world!</h1>
```

그러면, 마크업에서 `name`을 참조할 수 있습니다.

```svelte
/// file: App.svelte
<h1>Hello +++{name}+++!</h1>
```

중괄호 안에는 우리가 원하는 어떤 자바스크립트든 추가할 수 있습니다. 더 큰 소리로 인사하기 위해 `name` 을 `name.toUpperCase()`로 바꿔 보세요.

```svelte
/// file: App.svelte
<h1>Hello {name+++.toUpperCase()+++}!</h1>
```
