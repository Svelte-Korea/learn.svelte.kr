---
title: 스벨트킷이 뭔가요?
---

Svelte는 컴포넌트 프레임워크인 반면에, SvelteKit은 애플리케이션 프레임워크입니다(혹은 '메타프레임워크'로도 불립니다). SvelteKit은 제작 단계에서 발생하는 여러 어려운 문제를 해결하는데 중점을 두며 다음과 같은 기능을 제공합니다:

- 라우팅(Routing)
- 서버사이드 렌더링(Server-side rendering)
- 데이터 가져오기(Data fetching)
- 서비스 워커(Service workers)
- TypeScript 통합(TypeScript integration)
- 프리렌더링(Prerendering)
- 싱글 페이지 앱(Single-page apps)
- 라이브러리 패키징(Library packaging)
- 최적화된 프로덕션 빌드(Optimised production builds)
- 다양한 호스팅 제공 업체에 배포(Deploying to different hosting providers)
  ...등등

SvelteKit 앱은 처음 로드 시에 우수한 성능과 SEO 특성을 위해 주로 서버에서 렌더링됩니다. 이는 전통적인 '다중 페이지 앱' 또는 MPA의 접근과 유사합니다. 그러나 사용자가 탐색하는 동안 모든 것을 다시 로드하는 번거로운 상황을 피하기 위해 클라이언트 측 탐색을 지원하여, 현대적인 '싱글 페이지 앱' 또는 SPA의 특성도 채택할 수 있습니다. 이렇게 함으로써 사용자 경험을 향상시키고 성능을 최적화할 수 있습니다. SvelteKit 앱은 JavaScript가 실행되는 어디에서나 구동될 수 있지만, 사용자가 JavaScript를 실행하지 않아도 앱이 작동할 수 있는 환경도 지원합니다.

만약 이 개념이 복잡하게 느껴진다면 걱정하지 마세요. SvelteKit은 여러분과 함께 성장하는 프레임워크입니다! 간단히 시작하고 필요에 따라 점진적으로 기능을 추가해 나갈 수 있습니다.

## 프로젝트 구조

오른쪽에 있는 파일 트리 뷰어에서는 SvelteKit이 프로젝트에서 필요로 하는 몇 가지 파일들이 보입니다.

이전에 Node.js로 작업한 적이 있다면 `package.json`이 익숙할 것입니다. 이 파일은 프로젝트의 종속성을 나열합니다. 여기에는 `svelte` 및 `@sveltejs/kit`과 같은 종속성들과 SvelteKit CLI와 상호 작용하기 위한 다양한 `scripts`가 포함되어 있습니다. (현재 하단 창에서 `npm run dev`를 실행 중입니다.)

이 파일은 또한 `"type": "module"`을 지정합니다. 이는 `.js` 파일이 기본적으로, 전통적인 CommonJS 형식이 아닌, 네이티브 JavaScript 모듈로 처리된다는 것을 의미합니다.

`svelte.config.js`에는 프로젝트 설정이 들어 있습니다. 지금은 이 파일에 대해 걱정할 필요가 없지만, 궁금하다면 [문서](https://kit.svelte.dev/docs/configuration)를 참조하세요.

`vite.config.js`에는 [Vite](https://vitejs.dev/) 설정이 들어 있습니다. SvelteKit은 Vite를 사용하므로 [Vite 기능](https://vitejs.dev/guide/features.html)을 활용할 수 있습니다. 여기에는 핫 모듈 교체, TypeScript 지원, 정적 asset 처리 등이 포함됩니다.

`src`는 앱의 소스 코드가 들어가는 곳입니다. `src/app.html`은 페이지 템플릿이며 (SvelteKit은 `%sveltekit.head%` 및 `%sveltekit.body%`를 적절하게 대체합니다), `src/routes`는 앱의 [routes](/tutorial/pages)를 정의합니다.

마지막으로, static에는 앱을 배포할 때 함께 포함되어야 하는 에셋들(예: `favicon.png` 또는 `robots.txt`)이 들어 있습니다.
