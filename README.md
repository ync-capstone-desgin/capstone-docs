# 한국농산 캡스톤 디자인 문서

영남이공대학교 캡스톤디자인 **404팀**(배진수, 박준영, 조대성)의 한국농산 협력업체 통합관리 프로젝트 **기획·관리 문서 저장소**다.
코드와 개발 문서(API 명세, ERD, 배포·사용 설명서)는 개발 저장소 [hkagri-supplier](https://github.com/ync-capstone-desgin/hkagri-supplier)에 있다.

## 1. 문서 구조

```text
docs/
  team/
    README.md            팀 문서 목차
    requirements.md      요구사항 정의서
    meetings/            기업 미팅 회의록
    reference/           통합 전 개인 초안 중 참고 문서
```

문서 목록과 상태는 [docs/team/README.md](docs/team/README.md)에서 본다.
통합 전 개인 초안 전체는 [`personal-drafts` 태그](https://github.com/ync-capstone-desgin/capstone-docs/tree/personal-drafts/docs)에 보존되어 있다.

## 2. 운영 원칙

- 기획, 일정, 회의 결과, 주요 결정은 구두로만 남기지 않고 이 저장소에 기록한다.
- 중요한 결정은 관련 이슈, PR 또는 회의록 링크를 남긴다.
- 파일을 통째로 교체하기보다 Git 변경 이력이 남도록 수정한다.
- 팀 문서를 크게 바꿀 때는 팀원에게 먼저 공유한다.
- **기업 민감정보, 개인정보, 계정정보와 비밀번호는 저장하지 않는다.** (기업이 준 실제 계약서·인증서·엑셀 원본 포함)

### 문서 상태

중요 문서 상단에 다음 정보를 쓴다.

```text
작성: 이름
최종 수정일: YYYY-MM-DD
상태: 초안 | 검토중 | 확정
```

| 상태 | 의미 |
|---|---|
| `초안` | 작성 중이며 팀 합의 전 |
| `검토중` | 팀 또는 기업 피드백을 받는 중 |
| `확정` | 팀이 합의했거나 기업 확인을 마친 기준 문서 |

`확정` 문서를 바꿀 때는 문서 하단 "변경 이력"과 커밋에 이유를 남긴다.

## 3. 작업 흐름

문서 저장소는 개발 저장소보다 가볍게 운영한다.

- 작은 수정(오탈자, 회의록 추가, 표 갱신)은 최신 `main`을 받은 뒤 바로 커밋·푸시해도 된다.
- 여러 문서를 바꾸거나 팀 검토가 필요하면 브랜치를 만들어 PR로 올린다.
- 강제 푸시(`--force`)는 하지 않는다.

```bash
git switch main
git pull origin main
# 문서 작성 후
git add docs/team/
git commit -m "docs(요구사항): 메일 알림 시점 결정 반영"
git push origin main
```

브랜치 이름과 커밋 메시지는 개발 저장소와 같은 규칙을 쓴다. 자세한 방법은 [hkagri-supplier 협업 가이드](https://github.com/ync-capstone-desgin/hkagri-supplier/blob/develop/CONTRIBUTING.md)를 따른다.

```text
브랜치: docs/<짧은-영문-설명>        예) docs/requirements-update
커밋:   docs(<범위>): <한국어 요약>   예) docs(회의록): 10/20 한국농산 미팅 회의록 추가
```
