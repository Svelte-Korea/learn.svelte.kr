---
title: 스벨트킷이란?
---

스벨트는 _컴포넌트 프레임워크_ 인 반면, 스벨트킷은  _앱 프레임워크_ (또는 '메타 프레임워크')로, 프로덕션에 바로 사용할 수 있는 것을 만들 때 발생하는 복잡한 문제를 해결합니다.

- 라우팅
- 서버 사이드 렌더링
- 데이터 페칭
- 서비스 워커
- TypeScript 통합
- 사전 렌더링
- 싱글 페이지 앱
- 라이브러리 패키징
- 최적화된 페이지 빌드
- Deploying to different hosting providers
- ...그리고 더 많은 문제들.

스벨트킷 앱은 초기 로딩 속도와 SEO 특성 개선을 위해 기본적으로 서버에서 렌더링 됩니다. (전통적인 멀티 페이지 앱(`multi-page-app`) `MPA`처럼 작동합니다.) 하지만 써드파티 분석 쿠기 같은 걸 포함한 모든 것을  불편하게 다시 리로딩하는 걸 방지하기 위해 첫 번째 로딩 후에는 클라이언트 사이드 내비게이션으로 전환할 수 있습니다(현대적인 싱글 페이지 앱(`single-page-app`), `SPA`처럼 작동합니다). JavaScript가 작동하는 어느 곳에서든 돌아갈 수 있습니다. 다만, 나중에 설명하겠지만, 유저가 JavaScript를 전혀 실행할 필요가 없을 수도 있습니다.

듣기에 복잡해 보여도, 걱정하지 마세요. 스벨트킷은 여러분과 같이 성장하는 프레임워크입니다! 간단한 것부터 시작해 보고, 필요에 따라 새 기능을 추가해보세요.

## Project structure

오른쪽에 있는 파일 뷰어에서, 스벨트킷이 프로젝트에서 찾는 몇 파일들을 볼 수 있습니다.

`package.json` 은 여러분이 Node.js를 다뤄봤다면 익숙하겠죠. 프로젝트의 의존성을 명시합니다. — including `svelte` and `@sveltejs/kit` — 그리고 스벨트킷 CLI와 상호 작용하기 위한 다양한 `scripts`도 있습니다. (아래쪽 창에는 `npm run dev` 가 돌아가고 있습니다.)

> `"type": "module"`이라고 명시된 것에 주목하세요. 이건 `.js` 파일이 레거시 CommonJS 포맷이 아니라, 네이티브 Javascript 모듈로 취급된다는 것을 의미합니다.

`svelte.config.js` 은 프로젝트 세팅을 담은 파일입니다. 이 파일에 대해 당장 신경 쓸 필요는 없지만, 궁금하다면 [문서를 참고해 보세요.](https://kit.svelte.dev/docs/configuration).

`vite.config.js` 는 [Vite](https://vitejs.dev/) 설정을 담고 있습니다 스벨트킷은 Vite를 사용하기 때문에, HMR, TypeScript 지원, 정적 에셋 처리와 같은 [Vite 기능](https://vitejs.dev/guide/features.html)을 사용할 수 있습니다.

`src` 는 여러분 앱의 소스코드가 위치한 곳입니다. `src/app.html` 은 여러분 페이지의 템플릿입니다. (스벨트킷이 `%sveltekit.head%` 와 `%sveltekit.body%` 를 적절하게 바꿔줍니다.) 그리고 `src/routes` 는 앱의 [라우트](/tutorial/pages)를 정의합니다.

마지막으로, `static` 은 여러분 앱이 배포될 때 포함되어야 하는 아무 애셋(`favicon.png`, `robots.txt` 등)이나 넣을 수 있습니다.