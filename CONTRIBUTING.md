# 기여하기

스벨트 코리아는 여러분의 기여를 환영합니다!
기여 전 본 문서를 꼭 읽어주세요.

## 기여 방법

### 번역 참여 방법

1. 이슈 등록 혹은 이슈 선택
    - 번역이 필요한 문서를 선택해 이슈를 등록합니다.
    - 혹은 등록된 이슈 중 아직 번역하겠다는 사람이 없는 이슈를 선택합니다.
    - 번역이 필요한 문서는 대부분 `content/tutorial` 디렉토리 아래에 있습니다.
2. 이슈 할당
    - 아직 번역할 사람이 없는 이슈에 댓글을 달아 작업을 시작하겠다는 것을 알립니다.
3. 저장소 포크
4. 번역
    - 자세한 내용은 [번역 규칙](#번역-규칙)과 [번역 팁](#번역-팁)을 참고하세요.
5. 풀 리퀘스트 생성
6. 리뷰 반영

리뷰가 모두 반영되고 나면 메인테이너는 해당 풀 리퀘스트를 병합합니다.

### 번역 규칙

#### 1. 기존 원본 문장과 어순이 다르더라도 한국어 문장기호를 사용하기

- 과도한 괄호 사용 피하기
- `:`(colon)과 `—`(dash) 사용 피하기

<details>
<summary>예시</summary>

- `:`(colon)을 사용하는 대신 나열을 통해 자연스러운 문장을 만든 예시입니다.
- 원문
  - > SvelteKit allows you to create more than just pages. We can also create API routes by adding a +server.js file that exports functions corresponding to HTTP methods: GET, PUT, POST, PATCH and DELETE.
- 번역
  - > 스벨트킷을 이용하면 페이지를 만드는 것 말고도, API 라우트를 만들 수 있습니다. GET, PUT, POST, PATCH, DELETE 등의 HTTP 메소드에 대응하는 함수를 내보내는 +server.js 파일을 만들면 됩니다.

</details>

#### 2. 주어와 복수형 표기가 생략이 가능한 경우 생략해서 자연스러운 문장 만들기

#### 3. 'Svelte' 와 'SvelteKit'은 각각 '스벨트', '스벨트킷'으로 쓰기

#### 4. 스벨트에서 만든 조어의 경우 음차 표기

- 단, 처음 쓰이거나 강조가 되어 있는 경우 `음차(원본)` 형식으로 표기
- 예시: `라우팅(routing)`, `로딩(loading)`

#### 5. 예시 코드 내부에 있는 주석을 번역하기

### 번역 팁

- 어순 구상에 어려움이 있을 경우, [learn.svelte.jp](https://learn.svelte.jp) 참고
- 외래어 표기를 통해 한국어로 번역 가능한 단어가 있을 경우 읽기에 자연스러울 수 있도록 가능한 한 한글 표기를 사용하도록 함
  - 예: `<input>에 무언가를 입력하고 Enter를 누르면` -> `<input>에 무언가를 입력하고 엔터를 누르면`

## 원본 저장소에서 가져오기 가이드

메인테이너는 다음과 같이 원본 저장소에서 커밋을 가져와 최신화합니다.

```text
git remote add source https://github.com/sveltejs/learn.svelte.dev.git
git fetch source
git merge source/main
```

충돌이 있으면 수동 병합이 필요할 수 있습니다.
