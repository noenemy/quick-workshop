# 1. Quick Automate 접근하기

KYC 자동화 워크플로우를 생성하기 전에 필요한 커넥터가 구성되어 있고 샘플 문서가 S3에 업로드되어 있는지 확인합니다.

## 사전 준비 사항

시작하기 전에 다음이 구성되어 있는지 확인하세요:

- **Amazon S3 커넥터** - 문서 저장 및 검색
- **Amazon Textract 커넥터** - 문서 텍스트 추출
- **샘플 문서** - S3 버킷에 업로드된 고객 문서

## Part A: 샘플 문서 설정

### 단계 1: 샘플 문서 찾기

시작하기 → 워크샵 자료 다운로드 섹션에서 `sample-kyc-documents.zip`을 다운로드하고 압축 해제했습니다. 압축 해제된 `sample-kyc-documents/12345/` 폴더 안에 고객 ID 12345에 대한 두 개의 샘플 고객 문서가 있습니다:

- `Janice Sample-DriverLicense.jpg` — 운전면허증
- `Janice Sample-StatementofAccount.pdf` — 은행 명세서

아직 번들을 다운로드하지 않았다면 [워크샵 자료 다운로드](./00-download-workshop-materials.md) 페이지에서 받고 여기로 돌아오세요.

### 단계 2: S3에 문서 업로드

1. **S3 콘솔 접근**: AWS 계정에서 Amazon S3 콘솔로 이동합니다.

2. **S3 버킷 찾기**: 워크샵에 사용할 S3 버킷을 찾습니다.
   - 예: `workshop-bucket-{accountId}`

3. **문서 업로드**:
   - 압축 해제된 zip 파일에서 `12345` 폴더를 업로드합니다.
   - 문서가 원래 파일 이름을 유지하는지 확인합니다.

### 예상 S3 구조

```
workshop-bucket-{accountId}/
└── 12345/
    ├── Janice Sample-DriverLicense.pdf
    └── Janice Sample-StatementofAccount.pdf
```

> ℹ️ **참고**: 자동화 워크플로우는 문서가 고객 ID로 명명된 폴더에 있을 것으로 예상합니다. 폴더 이름이 자동화의 `customer_id` 변수와 일치하는지 확인하세요.

## Part B: Quick Automate 접근

문서가 준비되었으므로 Quick Automate에서 자동화 인프라를 생성합니다.

### 단계 1: Quick Automate 접근

1. [Quick Automate 홈 페이지](https://quickautomate.aws.amazon.com)로 이동합니다.
2. 프롬프트가 표시되면 AWS 자격증명으로 로그인합니다.

### 단계 2: Automation Group 생성

Automation Group은 공유 커넥터와 권한이 포함된 자동화 프로젝트를 위한 관리 환경을 제공합니다.

1. **"Create group"**을 클릭합니다.

2. 그룹 설정을 구성합니다:
   - **Name**: 설명적인 이름을 입력합니다.
     ```
     KYC-Workshop-Group
     ```
   - **Description**:
     ```
     Workshop automation group for KYC processing
     ```

### 단계 3: 필요한 Actions 추가

그룹 설정에서 필요한 AWS 서비스 커넥터를 추가합니다:

- **Amazon S3** - 문서 저장 및 검색용
- **Amazon Textract** - 문서 텍스트 추출용

### 단계 4: 그룹 설정 완료

1. **자격증명 구성 건너뛰기**: 이 워크샵에서는 자격증명 설정을 건너뜁니다.
2. **"Done"**을 클릭하여 Automation Group을 생성합니다.

### 단계 5: Automation Project 생성

이제 그룹 내에 특정 KYC 자동화 프로젝트를 생성합니다:

1. **새 프로젝트 시작**: 새 자동화 프로젝트 생성을 클릭합니다.

2. **프로젝트 구성**:
   - **Project Name**:
     ```
     KYC-Document-Processing
     ```
   - **Description**:
     ```
     Automated KYC document processing and analysis
     ```

3. **빌드 시작**: Start building을 선택합니다.

4. **템플릿 설정 건너뛰기**: 사전 구성된 템플릿을 건너뜁니다.

5. **에디터 진입**: 빈 프로젝트가 생성되고 Canvas 에디터에 진입합니다.

## 확인사항

이 단계들을 완료한 후 다음이 준비되어야 합니다:

- ✅ **Automation Group**: S3 및 Textract 커넥터와 함께 생성됨
- ✅ **Automation Project**: 워크플로우 구성 준비 완료
- ✅ **샘플 문서**: 올바른 폴더 구조로 S3에 업로드됨

## 다음 단계

사전 준비 사항, 문서 설정, Automation Group 생성을 완료했으면 다음 섹션에서 자동화 워크플로우 단계를 구성합니다.


[![Next](https://github.com/noenemy/kiro-cli/raw/main/03.mcp-server/images/next.png)](Lab3-authoring-quick-automate.md)
