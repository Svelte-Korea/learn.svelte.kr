# learn.svelte.kr

스벨트로 앱을 빌드하는 방법을 설명하는 대화형 튜토리얼 (번역 주: 원본 저장소는 [learn.svelte.dev](https://github.com/sveltejs/learn.svelte.dev/tree/main)입니다. 번역 기여를 원하신다면 [CONTRIBUTING.md](CONTRIBUTING.md)를 읽어주세요.)

## 설치

이 저장소는 [pnpm](https://pnpm.io/)을 사용합니다.

## 개발

먼저, `node scripts/create-common-bundle`을 실행합니다. 실행하면 스벨트킷 앱을 실행하는 데에 필요한 모든 것(Vite, esbuild, SvelteKit, Svelte compiler, etc.)을 패키지화하며, 이후 서버에서 압축을 풀어서 스벨트킷 애플리케이션 인스턴스를 생성하고 실행할 수 있습니다(튜토리얼의 출력 창을 구동합니다). 그리고 `dev`를 실행합니다.:

```bash
node scripts/create-common-bundle
pnpm dev
```

프로덕션용으로 빌드하고 로컬에서 실행하려면 다음처럼 합니다:

```bash
pnpm build
pnpm preview
```

## 새 튜토리얼 만들기

튜토리얼은 `content` 안에 있습니다. 각 튜토리얼은 화면 왼쪽에 있는 `README.md`와, 튜토리얼 코드 초기 상태인 `app-a`, 해결 상태인 `app-b` 폴더로 구성됩니다. 두 상태가 동일하게 유지되는 파일은 `app-b`에서 생략할 수 있습니다. `app-b`에서 `__delete`로 시작하는 파일은 삭제된 것으로 표시됩니다. 또한 `app-b`에서 `__delete`를 포함한 이름의 폴더는 삭제된 것으로 표시됩니다.

## 튜토리얼의 종속성 버전 올리기

루트와  `content/common` `package.json` 의 디펜던시(예를 들어 스벨트)의 버전을 올리세요. 루트에서 `pnpm i` 를 실행하고 (`pnpm-lock.yaml`를 업데이트하기 위해서), `content/common`에서 `npm i`를 실행하세요(`package-lock.json`를 업데이트하기 위해서).