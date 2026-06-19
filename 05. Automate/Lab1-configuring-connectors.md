# 1. AWS 서비스 커넥터 설정

이 섹션에서는 자동화 워크플로우에 필요한 AWS 서비스 커넥터를 배포합니다. 이 커넥터를 통해 Quick이 이전 단계에서 생성한 IAM 역할을 사용하여 Amazon S3 및 Amazon Textract와 안전하게 상호작용할 수 있습니다.

콘솔에서 하나씩 클릭하는 대신, CloudFormation 템플릿과 헬퍼 스크립트를 사용하여 두 커넥터를 한 번에 배포한 다음 Quick 콘솔에서 확인합니다.

## 단계 1: 배포 파일 찾기

소개 → 워크샵 자료 다운로드 섹션에서 `sample-kyc-documents.zip`을 다운로드하고 압축 해제했습니다. 이 모듈에서는 해당 폴더의 두 파일이 필요합니다:

- `deploy_connectors.sh` — 스택을 배포하는 헬퍼 스크립트
- `connector_creation.yaml` — S3 및 Textract 커넥터를 생성하는 CloudFormation 템플릿

아직 번들을 다운로드하지 않았다면 [워크샵 자료 다운로드](./00-download-workshop-materials.md) 페이지에서 받고 여기로 돌아오세요.

## 단계 2: CloudShell에서 커넥터 배포

AWS 콘솔을 열고 **us-west-2** 리전에서 **AWS CloudShell**(상단 내비게이션 바의 터미널 아이콘)을 실행합니다.

**Actions → Upload file**을 사용하여 두 배포 파일을 하나씩 CloudShell에 업로드합니다:

- `deploy_connectors.sh`
- `connector_creation.yaml`

두 파일이 동일한 디렉토리에 있어야 합니다(기본 CloudShell 홈 디렉토리면 됩니다).

스크립트를 실행 가능하게 만듭니다:

```bash
chmod a+x deploy_connectors.sh
```

스크립트를 실행합니다:

```bash
./deploy_connectors.sh
```

스크립트는 이메일로 Quick 사용자를 조회한 다음, 두 액션 커넥터를 생성하는 CloudFormation 스택을 배포합니다.

## 단계 3: 커넥터 ARN 확인

스크립트가 완료되면 두 커넥터의 ARN을 포함한 CloudFormation 스택 출력을 출력합니다:

- **S3ActionConnectorArn** — Amazon S3 커넥터의 ARN
- **TextractActionConnectorArn** — Amazon Textract 커넥터의 ARN

출력 예시:

```
==> Done. Stack outputs:
-----------------------------------------------------------------------------------
|                                 DescribeStacks                                  |
+---------------------------+-----------------------------------------------------+
|      OutputKey            |                     OutputValue                     |
+---------------------------+-----------------------------------------------------+
|  S3ActionConnectorArn     |  arn:aws:quicksight:us-west-2:...:actionConnector/  |
|  TextractActionConnectorArn|  arn:aws:quicksight:us-west-2:...:actionConnector/ |
+---------------------------+-----------------------------------------------------+
```

두 ARN이 모두 표시되면 배포가 성공한 것입니다.

## 단계 4: Quick 콘솔에서 커넥터 확인

커넥터가 등록되어 있고 사용자에게 표시되는지 확인합니다.

### 4.1 Quick 관리 접근

대시보드에서 **Manage Quick** 페이지로 이동합니다.

### 4.2 AWS Actions 열기

**AWS Actions**를 클릭하여 커넥터 목록을 확인합니다.

S3 커넥터와 Textract 커넥터가 모두 나열되고 사용 가능한 상태여야 합니다.

## 다음 단계

두 커넥터가 배포되고 확인되었으면, 모듈 1.2로 진행하여 이 커넥터를 사용하는 자동화 워크플로우를 구축합니다.


[![Next](https://github.com/noenemy/kiro-cli/raw/main/03.mcp-server/images/next.png)](Lab2-accessing-quick-automate.md)

