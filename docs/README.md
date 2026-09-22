# 기획 문서 작성 규칙

이 폴더는 한국농산 협력업체 통합관리 PoC의 기획 자료를 관리합니다.

## 폴더 구조

팀원은 자신의 GitHub ID로 폴더를 만든 뒤 기획서를 작성합니다.

```text
docs/
  plans/
    github-id/
      proposal.md
```

예시:

```text
docs/plans/JinsuBae2/proposal.md
```

## 작성 방법

1. `docs/templates/proposal-template.md`를 복사합니다.
2. `docs/plans/<GitHub-ID>/proposal.md`로 저장합니다.
3. 템플릿의 안내 문구를 자신의 기획 내용으로 교체합니다.
4. 본인 브랜치에서 커밋한 뒤 Pull Request를 생성합니다.

## 파일 작성 규칙

- 파일과 폴더 이름에는 영문 소문자, 숫자, 하이픈 사용을 권장합니다.
- 이미지가 필요하면 개인 폴더 아래 `images` 폴더에 저장합니다.
- 기업이 제공한 원본 계약서, 인증서 또는 개인정보는 저장소에 올리지 않습니다.
- API 키, 비밀번호, 토큰 등 보안정보는 커밋하지 않습니다.

## 권장 브랜치와 커밋

- 브랜치: `docs/<GitHub-ID>-proposal`
- 커밋: `docs: add <GitHub-ID> proposal`

