# 3. Automate 만들기

이 섹션에서는 Amazon Quick Automate를 사용하여 포괄적인 KYC(Know Your Customer) 자동화 워크플로우를 생성합니다. 이 5단계 워크플로우는 문서 처리, 불일치 분석, 부정적 미디어 스크리닝, 보고서 생성을 자동화합니다.

## 워크플로우 개요

이 자동화는 다음 단계를 통해 고객 문서를 처리합니다:

1. **문서 분류 및 데이터 추출** - 고객 문서 추출 및 분류
2. **불일치 분석** - 교차 문서 일관성 검증
3. **부정적 미디어 스크리닝** - 고객에 대한 부정적 뉴스 검색
4. **요약 생성** - 발견사항을 포괄적 보고서로 통합
5. **PDF 생성 및 저장** - 최종 보고서 생성 및 저장

---

## Step 1: 문서 분류 및 데이터 추출

**목적**: S3 버킷에서 고객 문서를 추출하고 분류

### 구성

**Add - Process Step:**
- **Title**: `Document Classification and Data Extraction`
- **Description**: `Step process to extract and classify customer documents`

### Agent 1 구성

**Add Node - Save Value (변수 1)**: 고객 식별자
- Action title: `Save customer_id`
- Value to Save: `"12345"`
- Variable Name: `customer_id`

**Add Node - Save Value (변수 2)**: S3 버킷 식별자
- Action title: `Save s3_bucket`
- Value to Save: `"workshop-bucket-{accountId}"`
- Variable Name: `s3_bucket`

**Add Node - Custom Agent:**

Agent Instructions:
```
"List all the files in the folder " + customer_id + " in the bucket " + s3_bucket+ ". Then extract all the text data from the documents using Amazon Textract and Classify the document into one of the following categories: CustomerDriverLicense, CustomerBankStatement, CustomerUtilityBill or Unknown. If unknown, create a human in the loop task and ask the human to provide the document category. Return a list of JSONs where each entry of the list is the extracted information for a document."
```

- **Agent Mode**: Pro

**Actions - Add Link:**
- General: `Create user task`
- Amazon S3: `DownloadFile`, `ListObjects`
- Amazon Textract: `ReadDocument`

**Structured Output:**
- Field1 - Type: `List`, Output name: `document_list`, Description: `List of document metadata`
- Field2 - Type: `String`, Output name: `customer_name`, Description: `Extracted name of the customer from the driver license`

**Agent Response**: (추출된 문서 정보 - document_list와 customer_name 포함)

→ 변수: `document_data`

### 오류 처리

**목적**: 견고한 문서 처리를 위해 이 단계를 try-catch 블록으로 감쌉니다.

**Add Node - Exception flow:**

**Add Node - Write log message:**
- message: `"Error"`

---

## Step 2: 불일치 분석

**목적**: 교차 문서 일관성 검증 및 불일치 감지

### 구성

**Add - Process Step:**
- **Title**: `Discrepancy Analysis`
- **Description**: `Agent to perform a cross document discrepancy analysis`

### Agent 2 구성

**Add Node - Custom Agent:**

- **Agent Mode**: Fast

Agent Instructions:
```
"You are a discrepancy analysis agent that helps US financial institutions onboard customers and perform KYC due diligence. You will analyze the information from the categorized customer documents and perform a cross document discrepancy analysis between these documents. Generate the final output in no more than 200 words. Follow the below steps in the given sequential order to accomplish your workflow objectives: * Review the Extracted Fields from these documents and compare the responses to identify discrepancies (if it exists) in the extracted content. * If discrepancies are detected: - Start the response as 'Discrepancy analysis has completed and discrepancies have been found'. - Summarize the discrepancies in a bullet list. If there are discrepancies identified in customer name or customer address mismatch happens, indicate with the label 'Customer Name or Address mismatch:'. * If there are no discrepancies - Start the response as 'Discrepancy analysis has completed and NO discrepancies have been found'. - Summarize the findings in a bullet list." +" " + str(document_data["document_list"])
```

- **Actions**: None (빈 배열)

**Agent Response**: (불일치 분석 보고서)

→ 변수: `discrepancy_analysis`

---

## Step 3: 부정적 미디어 스크리닝

**목적**: 고객에 대한 부정적 뉴스 및 위험 지표 검색

### 구성

**Add - Process Step:**
- **Title**: `Adverse Media Screening`
- **Description**: `Agent to perform comprehensive search on Customer name`

### Agent 3 구성

**Add Node - Save Value (변수 3)**: 추출된 고객 이름
- Action title: `Save customer_name`
- Value to Save: `document_data["customer_name"]`
- Variable Name: `customer_name`

**UI Agent**: Browser Automation (Custom Agent 아님)

Agent Instructions:
```
"ROLE: You are an adverse media screening agent responsible for conducting comprehensive negative news searches. Ensure searches match the exact full customer name '{customer_name}' rather than partial first or last name matches. TARGET: Perform adverse media screening for:" + customer_name + ". SEARCH STEPS: Use Brave website and execute searches across general web. SEARCH RESTRICTIONS: Only perform ONE search and access no more than one website from the search. SEARCH FOCUS AREA: financial misconduct. OUTPUT FORMAT: 200 word summary including overall risk assessment, key findings overview, timeline of major incidents, pattern analysis, severity assessment, current status, and total number of significant findings. Include detailed findings section with clear summaries, source links, dates, and credibility assessments. If no findings, provide a brief 200 word breakdown of search coverage, period, verification steps, and conclusion that no negative findings were identified."
```

**Agent Response**: (미디어 스크리닝 보고서)

→ 변수: `websearchresult`

---

## Step 4: 포괄적 요약 생성

**목적**: 모든 발견사항을 최종 KYC 보고서로 통합

### 구성

**Add - Process Step:**
- **Title**: `Summarize Findings`
- **Description**: `Agent to create a comprehensive summary from above outputs`

### Agent 4 구성

**Add Node - Custom Agent:**

Agent Instructions:
```
"Create a 200 word KYC (Know Your Customer) summary report formatted in HTML. Structure the report as follows:\
\
1. DOCUMENT HEADER: Include HTML header tags with 'KYC Analysis Summary Report', customer name '" + customer_name + "', customer ID '" + customer_id + "', and current date\
\
2. DISCREPANCY ANALYSIS SECTION: Present the discrepancy findings: " + discrepancy_analysis + ". Organize this into HTML subsections using appropriate header tags covering data inconsistencies, documentation gaps, verification issues, and risk implications\
\
3. WEB SEARCH ANALYSIS SECTION: Present the web search results: " + websearchresult + ". Structure this using HTML headers and paragraphs to cover external verification findings, public records analysis, adverse media screening, and additional intelligence gathered\
\
4. CONCLUSION: Summarize the overall KYC assessment and final determination using HTML paragraph tags\
\
Format the entire report using proper HTML structure with <h1>, <h2>, <h3> headers, <p> paragraphs, and <div> sections for better PDF formatting. Ensure all content is wrapped in appropriate HTML tags."
```

- **Agent Mode**: Pro
- **Actions**: None (빈 배열)

**Structured Output:**
- Field1 - Type: `String`, Output name: `summary`, Description: `The full summary report`

**Agent Response**: (완전한 HTML 형식의 KYC 보고서)

→ 변수: `KYC_Summary`

---

## Step 5: PDF 생성 및 저장

**목적**: PDF 보고서를 생성하고 S3 버킷에 저장

### 구성

**Add - Process Step:**
- **Title**: `Save the summary in S3 bucket`
- **Description**: `Step process to create & store a Summary PDF`

### Agent 5 구성

**Add Node - Create PDF**: HTML을 PDF로 변환하는 함수
- PDF Contents: `KYC_Summary["summary"]`
- Output Variable: `kyc_summary_pdf`

**Add Node - UploadFile S3**: S3에 파일을 업로드하는 함수
- Q action connector id: `"KYC-S3-Connector"` 선택
- File: `kyc_summary_pdf`
- Bucket: `s3_bucket`
- Key: `"Results/" + customer_id + "/kyc_summary.pdf"`

---

## Step 6: 워크플로우 전체 검토

전체 워크플로우가 올바르게 구성되었는지 확인합니다.

## Step 7: 워크플로우 테스트

**Run Workflow**를 실행합니다.

### 예상 출력

| 변수 | 설명 |
|------|------|
| `document_data` | document_list 배열과 customer_name이 포함된 JSON |
| `discrepancy_analysis` | 완료 상태로 시작하는 보고서 |
| `websearchresult` | HTML 형식의 부정적 미디어 결과 |
| `KYC_Summary` | 모든 분석을 결합한 완전한 HTML 보고서 |
| `kyc_summary_pdf` | S3에 저장된 최종 PDF 파일 (`workshop-bucket-{accountId}/Results/12345`) |

## 핵심 성공 요소

- ✅ **HTML 포맷**: Step 4가 마크다운이 아닌 올바른 HTML을 반환하는지 확인
- ✅ **오류 처리**: 견고한 처리를 위해 Step 1에 try-catch 포함
- ✅ **커넥터 구성**: 모든 액션 커넥터 ID가 올바르게 설정되었는지 확인
- ✅ **Agent Instructions**: 위에 제공된 정확한 프롬프트 지침 사용
- ✅ **변수 흐름**: 단계 간 적절한 변수 전달 확인

## 다음 단계

워크플로우를 구성한 후:

1. 샘플 고객 데이터로 테스트
2. 각 단계의 출력 검토
3. 필요에 따라 구성 조정
4. 프로덕션 사용을 위해 배포


수고 많으셨습니다!