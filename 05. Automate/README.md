# 모듈 5: Quick Automate

이 실습에서는 Amazon Quick의 기능인 Amazon Quick Automate를 사용하여 엔터프라이즈급 자동화를 구축하는 방법을 배웁니다. 금융 서비스 예시를 통해 전문화된 AI 에이전트가 웹 페이지와 비즈니스 애플리케이션 전반에서 복잡한 상호작용을 처리하기 위해 어떻게 협력하는지 탐색합니다.

지식과 도구를 활용하는 커스텀 에이전트가 포함된 프로덕션 준비 자동화를 생성하여 가맹점 온보딩 프로세스를 혁신합니다. Quick Automate의 채팅 기반 저작 도구와 비주얼 스튜디오를 사용하여 여러 에이전트로 구성된 워크플로우를 구성하고, 여러 도구와 통합하고, 워크플로우를 테스트 및 디버그한 다음, 강력한 엔터프라이즈 제어를 사용하여 배포합니다.

1시간 이내에 실제 사용 사례를 위한 에이전트 기반 자동화를 개발하는 방법을 알고 돌아갈 수 있습니다.

[워크샵 자료 다운로드 (zip)]

아카이브를 로컬에 압축 해제합니다. `sample-kyc-documents/` 폴더에 다음 내용이 표시되어야 합니다:

| 파일 / 폴더 | 사용 모듈 | 목적 |
|-------------|----------|------|
| `deploy_connectors.sh` | 모듈 1.1 — AWS 서비스 커넥터 설정 | CloudFormation을 통해 S3 및 Textract 액션 커넥터를 배포하는 헬퍼 스크립트 |
| `connector_creation.yaml` | 모듈 1.1 — AWS 서비스 커넥터 설정 | 배포 스크립트가 호출하여 두 커넥터를 생성하는 CloudFormation 템플릿 |
| `12345/Janice Sample-DriverLicense.jpg` | 모듈 1.2.1 — Quick Automate 접근 | 샘플 고객 운전면허증 — KYC 워크플로우를 위해 S3에 업로드 |
| `12345/Janice Sample-StatementofAccount.pdf` | 모듈 1.2.1 — Quick Automate 접근 | 샘플 고객 은행 명세서 — KYC 워크플로우를 위해 S3에 업로드 |



[![Next](https://github.com/noenemy/kiro-cli/raw/main/03.mcp-server/images/next.png)](Lab1-configuring-connectors.md)

