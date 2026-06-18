# 시민 서비스 운영 Space 탐색하기

이 모듈에서는 서비스 제공을 관리하고 개선하는 데 필요한 모든 정보를 하나로 모은 시민 서비스 운영 Space를 생성합니다. 이를 통해 조직이 적절한 접근 제어를 유지하면서 다양한 이해관계자 그룹을 위해 지식을 정리하는 방법을 시연합니다.

## 단계 1: 시민 서비스 운영 Space 생성

1. 왼쪽 내비게이션 패널에서 **Spaces**로 이동합니다.
2. **Create space** 버튼을 클릭합니다.
3. 연필 아이콘을 클릭하여 Space 정보를 편집합니다:
   - **Space name**: `Citizen Services Operations`
   - **Space description**: `Centralized knowledge hub for citizen services management, including policies, dashboards, and operational data`

이제 전략적 의사결정을 위해 정리된 여러 유형의 리소스를 포함할 전용 Space가 생성되었습니다:

- 서비스 표준을 정의하는 정책 문서
- 실시간 지표를 보여주는 성과 대시보드
- 재무 감독을 위한 예산 보고서
- 분석을 위한 운영 데이터

## 단계 2: Space에 문서 추가

서비스 제공 의사결정에 필요한 핵심 정책 및 운영 문서를 추가합니다:

1. 시민 서비스 운영 Space 내에서 우측 상단의 **Add knowledge**를 클릭합니다.
2. **File uploads**를 선택합니다.
3. 워크샵 자료에서 다음 문서를 추가합니다:
   - `service_request_policy.pdf`
   - `performance_standards.pdf`
   - `budget_guidelines.pdf`
   - `budget_allocation_data.csv`
   - `citizen_services_data.csv`

4. 모든 파일이 **Ready** 상태가 될 때까지 기다린 후 진행합니다.

이 문서들이 나타내는 내용:

| 문서 | 목적 | 핵심 내용 |
|------|------|-----------|
| Service Request Policy | 시가 시민 서비스 요청을 처리하는 방법 정의 | • 요청 유형별 응답 시간 표준<br>• 지연 및 예외 처리<br>• 품질 보증 프로세스 |
| Performance Standards | 부서별 성과 기대치 | • 서비스 수준 협약(SLA)<br>• 해결 시간 목표<br>• 시민 만족도 벤치마크 |
| Budget Guidelines | 재무 관리 정책 | • 예산 배분 방법론<br>• 지출 승인 프로세스<br>• 차이 보고 요구사항 |

> 💡 **전략적 가치**: 이 문서들을 한 곳에 모아두면 일선 직원부터 시의회까지 모든 이해관계자가 동일한 권위 있는 출처에서 작업할 수 있습니다.

## 단계 3: 웹 크롤러 지식 베이스 추가 (선택)

문서 업로드 외에도 웹 크롤러 지식 베이스를 사용하여 외부 웹 리소스를 Space에 연결할 수 있습니다. 공공 정보, 규제 지침, 외부 모범 사례를 통합하는 데 유용합니다.

1. Space에서 우측 상단의 **Add knowledge**를 클릭합니다.
2. **Knowledge bases**를 선택합니다.
3. **Create knowledge base**를 클릭합니다.
4. 지식 베이스 유형으로 **Webcrawler**를 선택합니다.
5. 새 통합의 이름을 입력하고(또는 기본값 유지) **No Authentication**을 선택합니다.
6. 지식 베이스를 구성합니다:
   - **Name**: `City Regulations and Guidelines`
   - **Description**: `External regulatory and best practice resources for citizen services`
   - **Content URLs**: 크롤링할 URL을 하나 이상 입력하고 (예: 시의 공공 규정 페이지 또는 관련 정부 지침 사이트) **Add**를 클릭합니다.
7. **Create**를 클릭합니다. 크롤러가 초기 크롤링을 완료하는 데 몇 분이 걸릴 수 있습니다.
8. 시민 서비스 운영 Space로 돌아갑니다.
9. **Add knowledge**를 클릭하고 **Knowledge bases**를 선택합니다.
10. 방금 생성한 **City Regulations and Guidelines** 지식 베이스를 선택합니다.
11. **Add**를 클릭합니다.

초기 크롤링이 완료될 때까지 기다리는 동안 단계 4로 이동할 수 있습니다.

> 💡 **전략적 가치**: 웹 크롤러 지식 베이스는 최신 외부 정보로 Space를 자동 업데이트하여 수동 문서 업데이트 없이도 팀이 항상 현행 규정과 모범 사례에 접근할 수 있도록 합니다.

## 단계 4: 접근 제어 구성

Spaces는 다양한 이해관계자 그룹에 대해 서로 다른 접근 수준을 지원합니다. 시민 서비스 운영 Space의 접근 권한을 구성해 봅시다:

1. Space에서 우측 상단의 **Share** 버튼을 클릭합니다.
2. 사용 가능한 Space 제어 옵션을 검토합니다.
3. `jane_doe@example.com`에게 **Viewer** 접근 권한으로 Space를 공유합니다. 이를 통해 Jane이 Space의 콘텐츠를 조회하고 사용할 수 있습니다.

Space는 두 가지 일반적인 접근 패턴을 지원합니다:

| 사용자 역할 | 접근 수준 | 권한 |
|------------|-----------|------|
| 부서장 | Owner 접근 | • Space 생성<br>• Space에 파일 업로드<br>• 다른 사람과 Space 공유<br>• Amazon Quick 리소스(토픽, 대시보드, 지식 베이스, 애플리케이션 액션) 연결/해제<br>• Space 삭제<br>• 다른 사용자를 공동 소유자로 지정 |
| 시의회 위원 | Viewer 접근 | • Space에 업로드된 파일 다운로드<br>• Space 내 데이터에 질문<br>• 에이전트의 컨텍스트로 특정 Space 사용<br>• 이름으로 Space 검색<br>• 직접 URL로 Space 접근<br>• 사전 설정된 샘플 질문 목록 보기 |

> 💡 **전략적 가치**: 접근 제어를 통해 각 이해관계자 그룹이 필요한 것만 관리하거나 조회할 수 있어 투명성과 보안을 모두 지원합니다.

## 단계 5: 자연어로 Space에 쿼리하기

Space에 문서가 포함되었으므로 모든 통합 리소스에 걸쳐 질문할 수 있습니다:

1. 우측 상단의 **채팅 아이콘**을 클릭합니다.
2. **All data and apps**를 선택합니다.
3. **Add**를 클릭하고 **Spaces**를 선택합니다.
4. 방금 생성한 **Citizen Services Operations** Space를 선택합니다.
5. **Web Search**를 선택 해제하여 Space의 문서와 지식 베이스만 포함합니다.

```
What are the response time standards for high-priority service requests?
```

```
Which neighborhoods have the highest service request volumes?
```

```
How does our actual spending compare to budget allocations this quarter?
```

```
What are the key performance metrics for the Public Works department?
```

### 웹 크롤러 질문

단계 3에서 웹 크롤러 지식 베이스를 생성한 경우, 추가한 Content URL에서 콘텐츠를 추출해야 하는 질문도 할 수 있습니다. 시도해 보세요.

AI가 업로드된 문서와 웹 크롤러 지식 베이스 모두에서 정보를 가져와 외부 규제 맥락을 포함한 포괄적인 답변을 제공하는 것을 확인하세요.

## 단계 6: 조직에서의 활용 방안 고려

이 Space를 탐색하면서 유사한 지식 관리가 조직에 어떤 이점을 줄 수 있는지 생각해 보세요:

### 투명성과 책임성
- 시의회에 성과 데이터에 대한 실시간 접근 제공
- 적절한 접근 제어로 공공 투명성 이니셔티브 지원
- 통합된 정책과 데이터로 의사결정 과정 문서화

### 운영 효율성
- 여러 시스템에서 문서를 검색하는 시간 제거
- 모든 직원이 현행의 권위 있는 정보로 작업하도록 보장
- 중복 데이터 입력 및 보고 감소

### 전략적 의사결정
- 정보에 입각한 결정을 위해 정책 맥락과 운영 데이터 결합
- 통합 데이터 소스에서 트렌드와 패턴 식별
- 증거 기반 예산 배분 및 리소스 계획 지원

### 협업과 지식 공유
- 부서 간 정보 사일로 해체
- 교차 기능 팀이 공유 지식에 접근할 수 있도록 지원
- 직원 전환 시 제도적 지식 유지

## 핵심 요점

Spaces는 조직에 다음을 제공합니다:

- **중앙화된 지식 관리**: 모든 관련 정보를 하나의 안전한 위치에
- **유연한 접근 제어**: 역할에 따라 각 이해관계자가 필요한 것만 조회
- **통합 인텔리전스**: 문서와 데이터가 원활하게 함께 작동
- **자연어 접근**: 기술적 전문성 없이 모든 리소스에 질문
- **거버넌스와 보안**: 투명성을 제공하면서 컴플라이언스 유지

시민 서비스 운영 Space는 이러한 기능이 서비스 제공 개선, 투명성 강화, 데이터 기반 의사결정과 같은 전략적 목표를 지원하는 방법을 보여줍니다.

**다음**: 모듈 4에서는 Quick Sight 분석 기능을 더 깊이 탐색하여 시민 서비스 데이터에서 실행 가능한 인사이트를 도출하는 방법을 배웁니다. 그 전에 모듈 3: Research Agent를 살펴보겠습니다.
