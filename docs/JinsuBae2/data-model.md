# 협력업체 통합관리 PoC 데이터 모델 초안

- 작성자: JinsuBae2
- 최종 수정일: 2026-09-22
- 상태: 초안

## 1. 모델링 원칙

- 협력업체를 계약, 인증, 발주·납기의 기준 엔티티로 둔다.
- 계약과 인증은 갱신 이력을 보존할 수 있도록 별도 레코드로 관리한다.
- 만료 상태는 날짜로 계산하되, 담당자의 처리상태는 별도로 기록한다.
- 기업 확인 전 필드명과 필수 여부는 확정하지 않는다.

## 2. 관계 초안

```text
Supplier 1 --- N Contract
Supplier 1 --- N Certification
Supplier 1 --- N PurchaseOrder
Contract 1 --- N Notification
Certification 1 --- N Notification
User 1 --- N Supplier 담당 관계 선택
FileMetadata N --- 1 Contract 또는 Certification
```

## 3. 핵심 엔티티

### Supplier 협력업체

| 필드 | 설명 | 필수 초안 | 확인사항 |
|---|---|---:|---|
| id | 내부 식별자 | 예 | 식별 방식 |
| name | 업체명 | 예 | 정식명·약칭 구분 |
| business_number | 사업자번호 | 협의 | 저장 허용 여부 |
| status | 거래상태 | 예 | 상태 종류 |
| contact_name | 담당자명 | 협의 | 개인정보 정책 |
| contact_phone | 연락처 | 협의 | 개인정보 정책 |
| contact_email | 이메일 | 협의 | 알림 수신 여부 |
| created_at | 등록일시 | 예 |  |
| updated_at | 수정일시 | 예 |  |

### Contract 계약

| 필드 | 설명 | 필수 초안 | 확인사항 |
|---|---|---:|---|
| id | 내부 식별자 | 예 |  |
| supplier_id | 협력업체 ID | 예 | 다수 업체 공동계약 여부 |
| contract_number | 계약번호 | 협의 | 번호 체계 |
| title | 계약명 | 예 |  |
| start_date | 시작일 | 협의 | 시작일 없는 계약 여부 |
| end_date | 종료일 | 협의 | 자동연장·무기한 계약 여부 |
| status | 계약상태 | 예 | 상태 종류 |
| owner_id | 내부 담당자 | 협의 | 담당 부서 포함 여부 |
| renewal_status | 갱신 처리상태 | 협의 | 처리 단계 |
| file_id | 첨부파일 참조 | 아니오 | 원본 저장 허용 여부 |

### Certification 인증

| 필드 | 설명 | 필수 초안 | 확인사항 |
|---|---|---:|---|
| id | 내부 식별자 | 예 |  |
| supplier_id | 협력업체 ID | 예 |  |
| type | 인증 종류 | 예 | 종류 목록 |
| certificate_number | 인증번호 | 협의 | 중복 허용 여부 |
| issued_date | 발급일 | 협의 |  |
| expiry_date | 만료일 | 협의 | 무기한 인증 여부 |
| status | 인증상태 | 예 | 자동·수동 상태 구분 |
| renewal_status | 갱신 처리상태 | 협의 | 처리 단계 |
| file_id | 첨부파일 참조 | 아니오 | 원본 저장 허용 여부 |

### Notification 알림

| 필드 | 설명 | 필수 초안 | 확인사항 |
|---|---|---:|---|
| id | 내부 식별자 | 예 |  |
| target_type | 계약 또는 인증 | 예 | 향후 대상 확장 여부 |
| target_id | 대상 ID | 예 |  |
| rule_days | 만료 전 기준일 수 | 예 | 90·30·7일 확정 여부 |
| scheduled_at | 알림 예정시각 | 예 | 시간대·휴일 처리 |
| recipient | 수신 대상 | 협의 | 사용자·부서·업체 |
| channel | 화면·이메일 등 | 협의 | 채널 종류 |
| delivery_status | 발송상태 | 예 | 상태 종류 |
| action_status | 업무 처리상태 | 협의 | 확인·진행·완료 구분 |

### PurchaseOrder 발주·납기 선택

| 필드 | 설명 | 필수 초안 | 확인사항 |
|---|---|---:|---|
| id | 내부 식별자 | 예 |  |
| supplier_id | 협력업체 ID | 예 |  |
| order_number | 발주번호 | 예 | 기존 번호 체계 |
| item_name | 품목명 | 예 | 품목 마스터 연동 여부 |
| quantity | 수량 | 협의 | 단위 관리 |
| order_date | 발주일 | 협의 |  |
| due_date | 납기예정일 | 협의 | 변경 이력 필요 여부 |
| completed_at | 납기완료일 | 아니오 | 부분 납품 여부 |
| status | 진행상태 | 예 | 상태 종류 |

## 4. 상태 계산 초안

```text
expiry_date 없음        -> 확인 필요
expiry_date < 오늘      -> 만료
오늘 <= expiry_date <= 기준일 -> 만료 예정
expiry_date > 기준일    -> 정상
```

만료 예정 구간과 갱신 처리상태는 별개로 관리한다. 예를 들어 만료 30일 전이면서 갱신 진행중일 수 있다.

## 5. 미팅 후 결정할 모델링 쟁점

- 하나의 계약이 여러 협력업체와 연결될 수 있는가
- 계약과 인증의 이전 버전을 별도 이력으로 보존해야 하는가
- 담당자는 개인, 부서 또는 둘 다인가
- 만료일이 없거나 자동 연장되는 항목을 어떻게 표현하는가
- 발주·납기는 직접 저장하는가, 기존 시스템에서 조회하는가
- 파일 원본을 저장하는가, 기존 위치 링크만 관리하는가

