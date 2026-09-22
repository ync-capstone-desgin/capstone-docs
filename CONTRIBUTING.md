# 협업 규칙

이 문서는 `capstone-docs` 저장소에서 사용하는 브랜치, 커밋, Pull Request와 Issue 규칙을 정의한다. 세 명의 팀원이 각자 기획 자료를 안전하게 공유하고, 통합 전까지 개인 초안의 변경 이력을 명확하게 유지하는 것이 목적이다.

## 1. 기본 브랜치 규칙

### main 브랜치

- `main`은 항상 팀원이 읽고 검토할 수 있는 상태로 유지한다.
- `main`에 직접 커밋하거나 강제 푸시하지 않는다.
- 모든 변경은 작업 브랜치에서 작성하고 Pull Request로 병합한다.
- Pull Request는 작성자를 제외한 팀원 1명 이상의 승인을 받은 뒤 병합한다.
- 병합 방식은 `Squash and merge`를 기본으로 사용한다.
- 충돌이 있거나 요청된 수정사항이 남아 있으면 병합하지 않는다.

### 권장 GitHub 보호 설정

`main`에 다음 규칙을 적용하는 것을 권장한다.

- Require a pull request before merging
- Required approvals: 1
- Dismiss stale pull request approvals when new commits are pushed
- Require conversation resolution before merging
- Block force pushes
- Block deletions

초기 문서 저장소에서는 상태 검사와 배포 승인은 필수로 두지 않는다. 자동 검사 도입 후 필요한 규칙을 추가한다.

## 2. 브랜치 이름 규칙

브랜치 이름은 영문 소문자와 숫자, 하이픈만 사용하며 다음 형식을 따른다.

```text
<type>/<github-id>-<short-description>
```

| 유형 | 용도 | 예시 |
|---|---|---|
| `docs` | 기획서와 문서 작성·수정 | `docs/jinsubae2-proposal` |
| `fix` | 잘못된 내용, 링크, 오탈자 수정 | `fix/rinhaze-broken-link` |
| `chore` | 템플릿과 저장소 설정 변경 | `chore/luluan8975-pr-template` |
| `feature` | 추후 서비스 기능 개발 | `feature/jinsubae2-expiry-alert` |

한 브랜치에서는 하나의 목적만 다룬다. 작업이 끝난 브랜치는 병합 후 삭제한다.

## 3. 커밋 규칙

커밋 메시지는 다음 형식을 사용한다.

```text
<type>: <summary>
```

- `summary`는 변경 결과를 짧게 작성한다.
- 영문 소문자를 권장하며 마침표를 붙이지 않는다.
- 한 커밋에는 하나의 논리적인 변경만 포함한다.
- `update`, `수정`, `작업`처럼 변경 내용을 알 수 없는 표현만 사용하지 않는다.

| 유형 | 용도 | 예시 |
|---|---|---|
| `docs` | 문서 추가·수정 | `docs: add supplier management proposal` |
| `fix` | 오류·오탈자·잘못된 링크 수정 | `fix: correct meeting schedule link` |
| `feat` | 서비스 기능 추가 | `feat: add contract expiry filter` |
| `refactor` | 동작 변경 없는 구조 개선 | `refactor: separate notification service` |
| `test` | 테스트 추가·수정 | `test: add expiry calculation cases` |
| `chore` | 설정, 템플릿, 도구 변경 | `chore: add pull request template` |

커밋 본문이 필요하면 제목 아래 한 줄을 비우고 변경 이유와 주의사항을 작성한다.

## 4. Pull Request 규칙

### 제목

PR 제목은 커밋 메시지와 동일한 형식을 사용한다.

```text
docs: add JinsuBae2 pre-meeting proposal
```

### 본문

PR 템플릿에 따라 다음 내용을 작성한다.

- 변경 목적과 배경
- 주요 변경사항
- 확인 방법
- 관련 Issue
- 리뷰어가 확인해야 할 부분

### 범위

- 개인 기획 문서는 원칙적으로 자신의 `docs/<이름>/` 폴더만 수정한다.
- 공통 README, 템플릿 또는 규칙 변경은 별도의 PR로 분리한다.
- 관련 없는 문서 정리나 표현 변경을 함께 포함하지 않는다.
- 기업의 민감정보와 실제 개인정보가 포함되지 않았는지 제출 전에 확인한다.

### 리뷰와 병합

- 작성자는 자신의 PR을 먼저 검토한 뒤 리뷰를 요청한다.
- 리뷰어는 내용의 명확성, 범위, 파일 위치, 민감정보 포함 여부를 확인한다.
- 수정 요청은 반영하거나 반영하지 않는 이유를 댓글로 남긴다.
- 승인 1개와 모든 대화 해결 후 `Squash and merge`로 병합한다.

## 5. Issue 규칙

### Issue를 만드는 경우

- 새 기획 또는 조사 작업
- 미팅 전 확인해야 할 질문
- 문서 오류 또는 누락
- 팀의 결정이 필요한 논점
- 추후 서비스 기능과 기술 작업

단순 오탈자를 즉시 수정하는 경우에는 Issue를 생략할 수 있다.

### 제목

Issue 제목은 다음 형식을 사용한다.

```text
[유형] 구체적인 작업 또는 문제
```

예시:

- `[기획] 계약 만료 알림 기준 조사`
- `[문서] 미팅 질문지 보완`
- `[결정] 팀원 폴더명 표기 방식 확정`
- `[버그] README 링크 오류 수정`

### 본문

- 배경 또는 문제
- 완료 조건
- 필요한 자료 또는 의존 작업
- 담당자와 목표일
- 관련 문서·PR 링크

### 라벨 권장안

| 라벨 | 의미 |
|---|---|
| `planning` | 기획과 요구사항 |
| `documentation` | 문서 작성·수정 |
| `meeting` | 기업 또는 팀 미팅 |
| `decision` | 팀 합의가 필요한 항목 |
| `bug` | 오류와 잘못된 정보 |
| `security` | 개인정보와 보안 |
| `blocked` | 외부 확인 또는 선행 작업 필요 |

## 6. 기본 작업 흐름

```bash
git switch main
git pull origin main
git switch -c docs/<github-id>-<description>

# 문서 작성 후
git add docs/<이름>/
git commit -m "docs: add supplier management proposal"
git push -u origin docs/<github-id>-<description>
```

푸시 후 GitHub에서 PR을 만들고 팀원에게 리뷰를 요청한다.

