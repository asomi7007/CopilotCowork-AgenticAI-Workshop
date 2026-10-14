# Lab 9: Knowledge Navigator Agent(내부 코파일럿) 구축하기

> 본 랩은 CloudLabs "Knowledge Navigator Agent (Internal Copilot) - High-Level Edition" 랩 가이드를 한국어로 정리한 교육용 자료입니다. 영문 원문은 [README.en.md](README.en.md)에서 확인할 수 있습니다. 원문 개요의 챌린지 3·4 명칭은 실제 챌린지 페이지 제목과 다르므로, 본 문서는 실제 페이지 제목을 따릅니다.

Knowledge Navigator Agent(내부 코파일럿) 해크 인 어 데이에 오신 것을 환영합니다! 이번 랩에서는 여러 부서에 흩어진 40개 이상의 Contoso 회사 문서를 직원이 검색하고 활용하도록 돕는 사내 지식 도우미를 만듭니다. 대화형 토픽과 에이전트 플로우를 갖춘 에이전트를 만들고 Microsoft Teams에 배포합니다.

## 시나리오

Contoso가 성장하면서 직원들은 인사, 재무, IT, 조달, 영업, 운영 등 여러 부서에 흩어진 정보를 찾는 일이 점점 어려워지고 있습니다. "경비 정산 정책은 어디서 볼 수 있나요?"나 "새 하드웨어를 요청하는 절차가 무엇인가요?" 같은 질문이 매달 수천 통의 사내 지원 이메일을 만들어 냅니다. 반복되는 질문을 줄이고 수작업 지원 의존도를 낮추기 위해 회사는 Knowledge Navigator Agent를 만들기로 결정합니다. 이 에이전트는 사내 문서를 검색하고 직원 질문에 답하며, 직원이 특정 문서에 대한 접근을 Outlook을 통해 요청할 수 있게 해 줍니다. 목표는 지식 접근 속도를 높이고 지원 팀의 부담을 덜어 주는 것입니다.

## 소개

이번 랩에서는 Contoso 문서 라이브러리, 즉 인사, 재무, IT, 조달, 영업, 지원, 운영을 망라하는 문서에서 직원들이 정보를 찾도록 돕는 **Knowledge Navigator Agent**를 만듭니다. Microsoft Copilot Studio를 사용해 회사 정책과 절차를 검색하고 지식 기반에서 답변을 제공하며 자동화된 작업까지 실행할 수 있는 대화형 AI 도우미를 만듭니다.

이 에이전트는 직원들이 인사 핸드북, 조달 정책, IT 거버넌스, 경비 정산, 영업 플레이북 등에 대해 질문할 수 있는 중앙 창구 역할을 합니다. 또한 에이전트 플로우를 만들어 문서 접근 요청 이메일을 Outlook을 통해 관리자 팀에 보내고, 관리자 팀이 검토 후 올바른 문서를 직원에게 공유하도록 합니다. 이 모든 작업은 코드 한 줄 없이 진행됩니다.

## 주요 도구 및 서비스

이번 랩에서 사용하는 도구는 다음과 같습니다.

- **Microsoft Copilot Studio**: 코드 없이 대화형 AI 에이전트를 만드는 플랫폼
- **SharePoint**: 40개 이상의 Contoso 회사 문서를 저장하고 색인화하는 공간
- **에이전트 플로우(Agent Flows)**: Power Automate 포털이 아닌 Copilot Studio 안에서 만드는 자동화 작업
- **생성형 AI 토픽(Generative AI Topics)**: 자연어 설명만으로 AI가 만들어 주는 대화 토픽
- **Microsoft Teams**: 에이전트를 배포하는 채널
- **Office 365 Outlook**: 에이전트 플로우를 통해 문서 접근 요청 이메일을 보내는 커넥터

## 학습 목표

이번 해크 인 어 데이를 마치면 다음을 수행할 수 있게 됩니다.

- Microsoft Copilot Studio에서 사내 지식 내비게이터 에이전트를 만들고 구성합니다.
- 40개 이상의 회사 문서가 담긴 SharePoint를 지식 원본으로 연결합니다.
- Copilot Studio 안에서 에이전트 플로우를 만들어 Outlook으로 문서 접근 요청을 보냅니다.
- 생성형 AI로 자연어 설명만으로 대화 토픽을 만듭니다.
- 토픽을 에이전트 플로우에 연결하고 변수를 매핑합니다.
- Microsoft Teams에 에이전트를 배포하고 테스트합니다.

## 랩 형식: 챌린지 기반

이 랩은 해크의 하이 레벨 에디션입니다. 각 챌린지는 목표와 반드시 지켜야 하는 요건(검증기가 확인하는 정확한 이름, ID, 값), 그리고 명확한 성공 기준만 제시하며 클릭 단위 안내는 제공하지 않습니다. 어떻게 도달할지는 여러분이 결정합니다.

이번 해크 인 어 데이는 완전한 내부 지식 내비게이터 에이전트를 만드는 5단계 챌린지로 구성되며, 각 챌린지는 특정 역량에 초점을 둡니다.

- **챌린지 1: 에이전트 및 SharePoint 사이트 만들기**: Copilot Studio 에이전트를 준비하고 SharePoint 사이트를 만들어 40개 이상의 Contoso 문서를 업로드합니다.
- **챌린지 2: SharePoint 지식 원본 연결**: SharePoint를 에이전트의 지식 원본으로 연결합니다.
- **챌린지 3: 문서 접근 요청용 에이전트 스킬과 에이전트 플로우 만들기**: Copilot Studio 안에서 Outlook으로 문서 접근 요청 이메일을 보내는 에이전트 플로우를 만듭니다.
- **챌린지 4: 토픽 연결과 엔드투엔드 테스트**: 토픽과 에이전트 플로우를 연결하고 지식 검색과 이메일 흐름을 엔드투엔드로 검증합니다.
- **챌린지 5: Microsoft Teams에 에이전트 게시**: 에이전트를 Teams에 배포하고 모든 토픽과 플로우를 테스트합니다.

각 챌린지 전체에서 다음을 반복하게 됩니다.

- 코드 없는 도구로 AI 에이전트 역량을 만듭니다.
- Copilot Studio 안에서 토픽과 플로우를 구성합니다.
- 진행하면서 각 토픽과 플로우를 즉시 테스트합니다.
- 최종적으로 Teams에 배포된 동작하는 에이전트를 완성합니다.

## 챌린지 개요

Microsoft Copilot Studio에서 새 에이전트를 만들고, SharePoint 사이트를 준비하고, 인사, IT, 조달, 재무, 영업, 지원, 운영을 망라하는 40개 이상의 Contoso 회사 문서를 업로드하는 것부터 시작합니다. 그다음 이 SharePoint 사이트를 에이전트의 지식 원본으로 연결합니다.

다음으로 Copilot Studio 안에서(Power Automate 포털 없이) Office 365 Outlook 커넥터를 통해 문서 접근 요청 이메일을 보내는 에이전트 플로우를 만듭니다. 직원이 문서를 요청하면 에이전트가 문서 이름, 이메일 주소, 요청 사유를 수집해 관리자 팀에 검토와 공유를 요청하는 이메일을 보냅니다.

그다음 Copilot Studio의 생성형 AI 기능으로 원하는 바를 일상 언어로 설명해 대화 토픽 두 개를 만듭니다. AI가 트리거 구문, 대화 흐름, 변수 수집을 대신 생성해 줍니다. 문서 접근 요청 토픽과 신입 직원 온보딩 토픽을 만들고, 문서 접근 토픽은 에이전트 플로우를 호출합니다. 에이전트는 SharePoint 지식 원본을 활용해 문서 검색 질문에도 스스로 답합니다.

마지막으로 에이전트를 Microsoft Teams에 게시하고 모든 토픽과 플로우를 테스트한 뒤 조직 전체에 공개합니다.

## 시작하기: 랩 환경 준비하기

Hack in a Day: Knowledge Navigator Agent(내부 코파일럿)에 오신 것을 환영합니다! AI 기반 지식 도우미를 만들 수 있도록 40개 이상의 Contoso 회사 문서가 담긴 완전한 환경을 준비해 두었습니다. 먼저 작업 공간을 준비하겠습니다.

### 랩 환경 접근하기

준비가 되면 가상 머신과 챌린지 가이드를 웹 브라우저 안에서 바로 사용할 수 있습니다.

![](images/auto-it-gt-gr-g8.png)

### 랩 리소스와 자격 증명 확인하기

랩 리소스와 자격 증명을 확인하려면 **환경(Environment)** 탭으로 이동합니다.

![](images/gs-leave-2.png)

### 분할 창 기능 사용하기

오른쪽 위의 **분할 창(Split Window)** 버튼을 누르면 챌린지 가이드를 별도 창으로 열 수 있습니다.

![](images/gs-leave-3.png)

### 가상 머신 관리하기

**리소스(Resources)** 탭에서 가상 머신을 필요에 따라 시작, 중지, 다시 시작할 수 있습니다. 랩 경험은 여러분 손에 달려 있습니다!

![](images/gs-leave-4.png)

### Copilot Studio 시작하기

1. JumpVM 바탕 화면에서 **Microsoft Edge** 브라우저 바로 가기를 클릭합니다.

   ![](images/zgr-gt.png)

1. 새 브라우저 탭을 열고 다음 URL로 Power Platform 관리 센터에 접속합니다.

    ```
    https://admin.powerplatform.microsoft.com
    ```

1. **Microsoft에 로그인** 탭에서 다음 이메일(1)을 이메일 필드에 입력하고 **(2) 다음**을 클릭해 진행합니다.

    - **이메일:** <inject key="AzureAdUserEmail"></inject>

      ![](images/gs-lab3-g2.png)

1. **임시 액세스 패스 입력** 화면에서 다음 **임시 액세스 패스**를 입력하고 **(2) 로그인**을 클릭합니다.

    - **임시 액세스 패스:** <inject key="AzureAdUserPassword"></inject>

      ![](images/gs-lab3-g3.png)

1. **로그인 상태를 유지하시겠습니까?** 팝업이 표시되면 **아니요**를 클릭합니다.

   ![](images/gs-4.png)

1. **Power Platform 관리 센터**에서 **(1) 관리**(Manage)를 선택하고 **(2) 환경**(Environments)을 선택한 다음 **(3) ODL_User <inject key="DeploymentID" enableCopy="false"/>'s Environment**를 클릭합니다.

   ![](images/uppowadminimg1.png)

   > **참고:** 이 단계에서 일시적인 포털 오류가 보일 때가 있습니다. 이것은 Power Platform에서 알려진 동작이며 환경 생성 과정에는 영향을 주지 않습니다. 오류가 나타나면 Power Platform 브라우저 창을 닫기만 하면 됩니다.

   > 환경 프로비저닝은 사용량이 많은 시기에는 최대 15분까지 걸릴 수 있습니다. 진행되는 동안 챌린지 2로 넘어가 LabVM의 **C:\Users\demouser\Downloads**에 이미 준비된 데이터 세트를 살펴볼 수 있습니다. 살펴보기를 마치면 환경이 준비되어 있을 것입니다.

1. 환경 페이지에서 **S2S 앱(S2S apps)** 아래의 **모두 보기**(See all)를 클릭합니다.

   ![](images/pro-activ-gg-g3.png)

   > <span style="color:red"><strong>중요:</strong> <code>https://<inject key="domainid" enableCopy="false"/>/cloudlabs.ai</code>가 이미 추가되어 있는지 확인합니다. 이미 존재한다면 <strong>16번 단계로 건너뜁니다</strong>. 없다면 아래 단계를 계속 진행합니다.</span>

   ![](images/powerplat.png)

1. 다음 창에서 **+ 새 앱 사용자**(+ New app user)를 클릭합니다.

   ![](images/uppowadminimg3.png)

1. 새 앱 사용자 만들기 창의 **앱**(App)에서 **+ 앱 추가**(+ Add an app)를 클릭합니다.

   ![](images/pro-activ-gg-g4.png)

1. **Microsoft Entra ID에서 앱 추가** 창의 검색 상자(1)에 **https://<inject key="domainid" enableCopy="false"/>/cloudlabs.ai**를 입력하고, 결과에서 사용 가능한 앱을 아무거나 (2) 선택한 다음 **(3) 추가**를 클릭합니다.

   ![](images/pro-activ-gg-g5.png)

   > <span style="color:red"><strong>중요:</strong> 검색 결과에서 앱을 찾을 수 없다면 이미 추가되었을 가능성이 높습니다. <strong>8번 단계</strong>로 돌아가 앱이 목록에 있는지 확인합니다. 있다면 <strong>16번 단계로 건너뜁니다</strong>.</span>

1. **사업부**(Business unit) 아래에서 목록에 있는 사용 가능한 사업부를 선택합니다 **(2)**.

   ![](images/pro-activ-gg-g6.png)

1. **보안 역할**(Security roles) 옆의 **편집** 아이콘을 클릭합니다.

   ![](images/pro-activ-gg-g7.png)

1. **권한 동기화**(Sync Permissions) 창에서 **(1) System Administrator**를 선택하고 **(2) 저장**을 클릭합니다.

   ![](images/pro-activ-gg-g8.png)

1. 팝업 창에서 **저장**(save)을 선택합니다.

   ![](images/pro-activ-gg-g9.png)

1. 모든 세부 정보를 검토하고 **만들기**(Create)를 클릭합니다.

   ![](images/pro-activ-gg-g10.png)

1. 새 브라우저 탭을 열어 다음 URL로 **Microsoft Copilot Studio**로 이동합니다.

    ```
    https://copilotstudio.microsoft.com
    ```

1. Copilot Studio 포털에 도착합니다. 이 랩은 새 환경을 기준으로 만들어졌으므로 오른쪽 위의 **새 환경**(New experience) 토글이 켜져 있는지 확인합니다.

   ![](images/pro-activ-gg-g10-1.png)

1. Copilot Studio에서 환경 선택기(1)를 열고 펼친 다음 **(2) ODL_User <inject key="DeploymentID" enableCopy="false"></inject>'s Environment**를 선택해 전환합니다.

   ![](images/ex1-travel-g6.png)

1. 이제 Microsoft Copilot Studio로 **Knowledge Navigator Agent**를 만들 준비가 끝났습니다.

   ![](images/pro-activ-gg-g14.png)

## 챌린지 1: Copilot Studio에서 내부 지식 코파일럿 만들기

### 소개

조직의 직원들은 여러 부서에 흩어진 사내 정책, 절차, 가이드라인을 찾는 데 소중한 시간을 낭비합니다. 전통적인 문서 저장소와 파일 공유는 필요한 정보를 빠르게 찾기 어렵게 만들고, 관리자와 동료에게 같은 질문을 반복하게 만듭니다.

이 챌린지에서는 Microsoft Copilot Studio로 AI 기반 내부 지식 코파일럿을 만듭니다. 이 코파일럿은 직원들이 인사, 재무, IT, 조달 부서의 정보에 접근하도록 돕는 지능형 도우미 역할을 합니다.

### 데이터 세트 접근하기

이 챌린지에 필요한 데이터 세트는 이미 LabVM에 준비되어 있으므로 별도의 다운로드가 필요 없습니다.

데이터 세트는 파일 탐색기의 다음 위치에 있습니다.

```
C:\Users\demouser\Downloads\knowledge-dataset\documents
```

이 폴더에는 인사, 재무, IT, 조달을 망라하는 Word, Excel, PowerPoint, CSV, 이미지 파일로 구성된 Contoso Corp 지식 문서가 담겨 있습니다. 이 문서들은 이 챌린지의 뒤쪽에서 SharePoint **문서(Documents)** 라이브러리에 업로드합니다.

> **참고:** `documents` 폴더가 보이지 않으면 계속 진행하기 전에 강사에게 알리세요.

### 챌린지 목표

- Microsoft Copilot Studio에 로그인합니다.
- 내부 지식 탐색용 새 에이전트를 만듭니다.
- 에이전트의 기본 설정과 ID를 구성합니다.
- 다음 챌린지의 지식 기반 업로드를 준비합니다.

### 완료 단계

#### 1단계: SharePoint 사이트 만들기

1. Microsoft 365에 로그인하고 Contoso 지식 기반이 될 SharePoint 사이트를 만듭니다.

    ```
    https://myapps.microsoft.com
    ```

   - **이메일/사용자 이름:** <inject key="AzureAdUserEmail"></inject>
   - **암호:** <inject key="AzureAdUserPassword"></inject>

1. "로그인 상태를 유지하시겠습니까?" 프롬프트가 나타나면 **아니요**로 닫습니다.

1. 앱 아이콘으로 **SharePoint**를 실행합니다.

   > **참고:** 페이지에 SharePoint 아이콘이 보이지 않으면 `https://<inject key="tenantname" enableCopy="false"/>.sharepoint.com/`으로 바로 이동합니다.

1. 왼쪽 창에서 **만들기**(Build)를 선택하고 **만들기 시작**(Start building) 아래의 **사이트**(Site)를 선택합니다.

1. **사이트 템플릿 선택** 화면에서 **팀 사이트**(Team site)를 유지하고 **표준 팀**(Standard team)을 선택한 다음 **템플릿 사용**(Use template)을 선택합니다.

1. **사이트 설정** 화면에서 아래 설정을 입력하고 **사이트 만들기**를 선택합니다.

   | 설정 | 값 |
   |---|---|
   | 사이트 이름 | **contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>** |
   | 사이트 설명 | "Internal knowledge base for company policies and procedures" |
   | 그룹 이메일 주소 / 사이트 주소 | 자동으로 채워진 값 유지 |
   | 개인 정보 설정 | **공개**(Public, 조직의 모든 구성원이 접근 가능) |

   > **참고:** SharePoint 사이트 이름이나 사이트 별칭이 이미 존재한다는 메시지가 나타나면 다른 고유한 사이트 이름을 입력하고 사이트 만들기를 계속합니다.

1. 사이트 만들기를 마칩니다(구성원을 추가하거나 건너뛰어도 됩니다). 그다음 사이트의 **문서(Documents)** 라이브러리를 열고 LabVM 데이터 세트 폴더의 모든 파일을 업로드합니다.

    ```
    C:\Users\demouser\Downloads\knowledge-dataset\documents
    ```

   문서가 40개 이상이므로 업로드가 끝날 때까지 몇 분 기다립니다.

1. 업로드가 끝나면 주소 표시줄에서 사이트 URL을 복사해 메모장에 적어 둡니다. 다음 챌린지에서 필요합니다.

   > 예시 형식: `https://<inject key="tenantname" enableCopy="false"/>.sharepoint.com/sites/contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>`

1. 마지막으로 Microsoft Copilot Studio를 열고 **ODL_User<inject key="DeploymentID" enableCopy="false"></inject>** 환경에 있는지 확인합니다.

    ```
    https://copilotstudio.microsoft.com
    ```

#### 2단계: 새 에이전트 만들기

1. **새 에이전트**(New agent) 드롭다운에서 **비즈니스 프로세스 최적화**(Optimize your business processes) 아래의 **에이전트**(Agent)를 선택합니다.

1. 에이전트 이름을 다음과 같이 지정합니다.

    ```
    Internal Knowledge Navigator
    ```

1. 에이전트가 만들어지면 에이전트의 **빌드**(Build) 탭에 있는 모델 드롭다운(1)에서 AI 모델을 **GPT-5 Chat**으로 변경합니다. 이 랩 전체에서 Copilot Credit 문제를 피하기 위해 **GPT-5 Chat**(2)을 사용합니다.

   ![](images/gs-model-gpt5.png)

1. 에이전트에 다음 **지시**(Instructions)를 추가한 다음 저장합니다. 아직 게시할 필요는 없으며 저장만 하면 됩니다.

   > **팁:** 이 화면에는 **저장**이라고 적힌 버튼이 없습니다. 위쪽 도구 모음의 작은 저장 아이콘을 찾아 클릭하세요.

    ```
    - Respond only to queries related to Contoso internal company policies, procedures, business operations, and department-specific guidelines.
    - Retrieve knowledge from the uploaded Contoso company documents stored in SharePoint, including HR handbooks, IT governance policies, procurement procedures, support policies, sales playbooks, business reports, and operational data.
    - When answering questions:
      - Provide clear, accurate information based strictly on official Contoso documents
      - Always cite the source document name (e.g., Contoso_HR_Handbook.docx)
      - Use professional, helpful language appropriate for internal employees
      - If information isn't in the knowledge base, direct users to the appropriate department contact
    - For common scenarios, guide users through step-by-step processes based on documented procedures
    - Offer to email policy documents or create support tickets when appropriate
    - Maintain employee privacy and confidentiality at all times
    - Focus on providing information from official Contoso documents rather than general knowledge
    ```

#### 3단계: 에이전트 기본 인사 테스트하기

1. 테스트 패널을 열고 에이전트가 올바르게 인사하는지 확인합니다. "Hello"와 "What can you help me with?"를 입력해 보고, 에이전트가 적절한 인사로 응답하는지 확인합니다.

1. 지식 관련 질문은 아직 동작하지 않습니다. 지식 원본은 다음 챌린지에서 추가합니다.

<validation step="f0a7a622-73af-4e80-8f84-13cda3f2e28e" />

> **축하합니다.** 챌린지를 완료했습니다. 이제 검증할 차례입니다. 단계는 다음과 같습니다.
> - 해당 챌린지의 검증(Validate) 버튼을 누릅니다. 성공 메시지가 나타나면 다음 챌린지로 진행할 수 있습니다.
> - 성공하지 못하면 오류 메시지를 자세히 읽고 랩 가이드의 지시에 따라 해당 단계를 다시 시도합니다.
> - 도움이 필요하면 cloudlabs-support@spektrasystems.com으로 문의하세요. 연중무휴 24시간 지원됩니다.

### 성공 기준

- **Internal Knowledge Navigator**라는 이름의 새 에이전트를 만들었습니다.
- 에이전트를 구성했습니다.

### 추가 리소스

- [Microsoft Copilot Studio Overview](https://learn.microsoft.com/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)
- [Create your first copilot](https://learn.microsoft.com/microsoft-copilot-studio/fundamentals-get-started)

## 챌린지 2: SharePoint 지식 원본 연결하기

### 소개

챌린지 1에서 내부 지식 내비게이터 코파일럿을 만들고 모든 Contoso 회사 문서를 SharePoint에 업로드했습니다. 이제 그 SharePoint 사이트를 코파일럿의 지식 원본으로 연결할 차례입니다. 이렇게 하면 코파일럿이 40개 이상의 회사 문서를 모두 검색해 직원 질문에 정확한 답변을 제공할 수 있게 됩니다.

이 챌린지에서는 SharePoint 사이트를 Copilot Studio에 연결하고, 지식 원본이 올바르게 색인화되었는지 확인하고, 기본 지식 검색을 테스트해 에이전트가 Contoso 문서로 질문에 답할 수 있는지 확인합니다.

### 챌린지 목표

- SharePoint 사이트를 Copilot Studio의 지식 원본으로 연결합니다.
- 지식 원본 설정을 구성합니다.

### 필수 조건

이 챌린지를 시작하기 전에 다음을 확인합니다.

- 챌린지 1에서 **Internal Knowledge Navigator** 에이전트를 만들었습니다.
- 챌린지 1에서 SharePoint 사이트 **contoso-documents**-<inject key="DeploymentID" enableCopy="false"></inject>를 만들었습니다.
- 챌린지 1에서 40개 이상의 Contoso 문서를 SharePoint 사이트에 업로드했습니다.
- SharePoint 사이트 URL을 저장해 두었습니다.

### 완료 단계

#### 1단계: SharePoint 지식 원본 추가하기

1. Microsoft Copilot Studio에서 **Internal Knowledge Navigator** 에이전트를 열고 **ODL_User<inject key="DeploymentID" enableCopy="false"></inject>** 환경에 있는지 확인합니다.

    ```
    https://copilotstudio.microsoft.com
    ```

1. 챌린지 1에서 만든 SharePoint 사이트를 지식 원본으로 추가합니다.

    ```
    https://<inject key="tenantname" enableCopy="false"/>.sharepoint.com/sites/contoso-documents-<inject key="DeploymentID" enableCopy="false"></inject>
    ```

   > **팁:** 다른 탭에서 SharePoint 사이트를 열어 주소 표시줄에서 복사한 뒤 붙여 넣습니다.

1. 사이트가 추가되었다는 확인을 기다립니다.

   > **지금 일어나는 일:** Copilot Studio가 SharePoint 사이트에 연결하고 챌린지 1에서 업로드한 40개 이상의 문서를 자동으로 색인화합니다.

1. 지식 원본을 추가한 뒤 에이전트를 저장합니다.

#### 2단계: 지식 원본 연결 확인하기

1. **지식**(Knowledge) 창에서 사이트가 지식 원본으로 표시되는지 확인하고 열어 상태가 **준비**(Ready)에 도달하는지 검증합니다.

   > **참고:** SharePoint 커넥터가 문서 라이브러리의 모든 문서를 자동으로 색인화합니다. 파일을 개별적으로 업로드할 필요는 없습니다.

1. 상태가 **실패**(Failed)나 **오류**(Error)로 표시되면 SharePoint 사이트 URL을 다시 확인합니다.

### 성공 기준

- SharePoint 지식 원본이 Copilot Studio에 연결되었습니다.

### 추가 리소스

- [Add knowledge sources to your copilot](https://learn.microsoft.com/microsoft-copilot-studio/nlu-boost-conversations)
- [Generative answers with uploaded files](https://learn.microsoft.com/microsoft-copilot-studio/nlu-boost-node)

## 챌린지 3: 에이전트 스킬과 이메일 작업용 에이전트 플로우 만들기

### 소개

내부 지식 내비게이터 코파일럿이 이제 Contoso SharePoint 지식 기반을 검색해 직원 질문에 답할 수 있습니다. 그러나 진정으로 유용한 엔터프라이즈 코파일럿은 답변 제공을 넘어 직원을 대신해 실제 작업을 수행할 수 있어야 합니다. 흔한 업무 시나리오 중 하나는 직원이 특정 문서를 자신의 받은 편지함으로 받거나 제한된 콘텐츠에 대한 정식 접근 요청을 제출하려는 경우입니다.

이 챌린지에서는 에이전트 스킬과 에이전트 플로우를 만들어 이메일을 통한 문서 접근 요청 기능을 추가합니다. Copilot Studio의 스킬로 직원이 요청 절차를 따르도록 안내하는 구조화된 동작을 정의하고, 그다음 관리자 팀에 구조화된 이메일을 보내는 Power Automate 플로우를 연결합니다. 이 플로우는 챌린지 4에서 에이전트 스킬과 통합할 수 있도록 미리 만들어 둡니다.

### 챌린지 목표

- Copilot Studio에서 에이전트 스킬 2개(New Employee Onboarding와 Email Document)를 만듭니다.
- Power Automate로 Office 365 Outlook을 통해 문서 접근 요청 이메일을 보내는 에이전트 플로우를 만듭니다.
- 플로우 입력(직원 이메일, 문서 이름, 설명)과 출력(이메일 상태)을 구성합니다.
- 플로우가 게시되어 다음 챌린지의 에이전트 스킬과 통합할 준비가 되었는지 확인합니다.

### 필수 조건

이 챌린지를 시작하기 전에 다음을 확인합니다.

- 챌린지 1을 완료했습니다(**Internal Knowledge Navigator** 에이전트 생성).
- 챌린지 2를 완료했습니다(SharePoint 지식 원본 연결).
- **Microsoft Copilot Studio**와 **Power Automate**에 접근 가능합니다.

### 완료 단계

#### 1단계: 스킬 섹션 열기

1. **Internal Knowledge Navigator** 에이전트를 엽니다.

1. 오른쪽 패널에서 **스킬**(Skills) 항목을 찾고 더하기(+) 아이콘을 선택합니다.

1. **스킬 추가**(Add skill) 대화 상자에서 **빈 항목에서 만들기**(Create from blank)를 선택합니다.

#### 2단계: 스킬 1 만들기, New Employee Onboarding

1. **스킬 추가** 대화 상자(**빈 항목에서 만들기**)에서 다음을 입력합니다.

   - **이름**(Name):

     ```
     new-employee-onboarding
     ```

   - **설명**(Description):

     ```
     Use this skill when a new employee asks about company policies, procedures, organizational structure, benefits, workplace resources, or onboarding requirements.
     ```

   - **지시**(Instructions): 자리 표시자 텍스트를 다음으로 바꿉니다.

     ```
     When this skill is activated:

     1. Assist new employees who are learning about the company. Help them understand company policies, procedures, organizational structure, benefits, workplace resources, and onboarding requirements.
     2. Search the SharePoint knowledge base for information from documents such as the HR Handbook, Onboarding Checklist, IT Governance Policy, Employee Travel Reimbursement guidelines, and other relevant company documents.
     3. Always cite the source document name in your answer.
     4. If the information is not in the knowledge base, tell the employee to contact the HR team instead of guessing.
     ```

1. **만들기**(Create)를 선택합니다. 스킬이 이제 에이전트 페이지의 **스킬**(Skills) 아래에 나타납니다.

#### 3단계: 스킬 2 만들기, Email Document

1. **스킬**(Skills) 옆의 더하기(+) 아이콘을 다시 선택하고 **빈 항목에서 만들기**를 고른 다음 다음을 입력합니다.

   - **이름**(Name):

     ```
     email-document
     ```

   - **설명**(Description):

     ```
     Use this skill when an employee wants to submit a document access request, request access to a document, or have a document emailed to them.
     ```

   - **지시**(Instructions):

     ```
     When this skill is activated:

     1. Recognize requests such as "submit a document request", "request document access", "email me a document", "send me a document", or "I want to request a document".
     2. Collect the following details from the employee, asking one question at a time:
        - The name of the document they need.
        - Their email address.
        - A brief description of why they need the document.
     3. Confirm the collected values back to the employee before continuing.
     4. Tell the employee their request has been submitted and the admin team will review it.
     ```

1. **만들기**(Create)를 선택합니다.

1. 에이전트를 저장합니다.

> **참고:** 챌린지 4에서 **Email Document Flow**를 이 스킬에 연결하면 에이전트가 요청을 인지하기만 하는 것이 아니라 실제로 요청 이메일을 보내게 됩니다.

#### 4단계: 에이전트 플로우 만들기

1. 에이전트 페이지에서 **도구**(Tools) 옆의 더하기(+) 아이콘을 선택합니다.

1. **+ 추가**(+ Add) > **워크플로우**(workflow)를 선택합니다.

1. 플로우 디자이너가 열리며 두 노드가 이미 배치되어 있습니다. **에이전트가 플로우를 호출할 때**(When an agent calls the flow)와 **에이전트에게 응답**(Respond to the agent)입니다.

1. **에이전트가 플로우를 호출할 때** 트리거 노드에서 입력 추가를 클릭하고 유형은 **텍스트**(Text)로 선택한 뒤 이름을 지정합니다. 세 번 반복해 다음 입력을 만듭니다.

   - `EmployeeEmail`
   - `DocumentName`
   - `DocumentDescription`

<validation step="1036963f-93f7-4fc9-9b6f-77084c6a3c0d" />

> **축하합니다.** 챌린지를 완료했습니다. 이제 검증할 차례입니다. 단계는 다음과 같습니다.
> - 해당 챌린지의 검증(Validate) 버튼을 누릅니다. 성공 메시지가 나타나면 다음 챌린지로 진행할 수 있습니다.
> - 성공하지 못하면 오류 메시지를 자세히 읽고 랩 가이드의 지시에 따라 해당 단계를 다시 시도합니다.
> - 도움이 필요하면 cloudlabs-support@spektrasystems.com으로 문의하세요. 연중무휴 24시간 지원됩니다.

#### 5단계: 이메일 작업 추가하기

1. 두 노드 사이의 더하기(+) 아이콘을 선택하고 **Office 365 Outlook**에서 **이메일 보내기**(Send an email)를 추가합니다.

1. 로그인하라는 메시지가 나타나면 <inject key="AzureAdUserEmail"></inject>을 사용합니다.

1. 작업을 구성합니다.

   - **받는 사람**(To): <inject key="AzureAdUserEmail"></inject>
   - **제목**(Subject): `Document Access Request - `에 이어 **DocumentName** 동적 콘텐츠
   - **본문**(Body): 아래 텍스트에서 표시된 위치에 동적 콘텐츠를 삽입합니다.

     ```
     Hello Admin,

     An employee has submitted a request for access to the following document.

     Requested Document: [Add DocumentName dynamic content]
     Reason: [Add DocumentDescription dynamic content]
     Requested By: [Add EmployeeEmail dynamic content]

     Please review the request and share the document with the employee.

     Thank you,
     Internal Knowledge Navigator
     ```

     > **참고:** 동적 콘텐츠를 추가하려면 커서를 끝에 두고 슬래시(/)를 입력합니다.

1. **에이전트에게 응답**(Respond to the agent) 노드에 출력 하나를 추가합니다. 값이 `Email sent successfully`인 **텍스트**(Text) 유형의 `EmailStatus`입니다.

#### 6단계: 플로우 이름 바꾸기와 게시하기

1. 저장하기 전에 디자이너 위쪽의 플로우 이름을 선택해 **Email Document Flow**로 바꿉니다.

   > **참고:** 플로우 이름은 저장하고 게시하기 전에 바꿉니다. 게시한 뒤에 바꾸지 않습니다.

1. **저장**(Save)을 선택한 다음 **게시**(Publish)를 선택합니다.

1. 에이전트로 돌아갑니다. 이제 플로우가 **도구**(Tools) 아래에 나타나며 챌린지 4에서 **email-document** 스킬에 연결할 준비가 되었습니다. 위쪽 도구 모음에서 에이전트를 저장합니다.

<validation step="47541ff8-bef9-48b3-9ab6-1b46d31b2fe2" />

> **축하합니다.** 챌린지를 완료했습니다. 이제 검증할 차례입니다. 단계는 다음과 같습니다.
> - 해당 챌린지의 검증(Validate) 버튼을 누릅니다. 성공 메시지가 나타나면 다음 챌린지로 진행할 수 있습니다.
> - 성공하지 못하면 오류 메시지를 자세히 읽고 랩 가이드의 지시에 따라 해당 단계를 다시 시도합니다.
> - 도움이 필요하면 cloudlabs-support@spektrasystems.com으로 문의하세요. 연중무휴 24시간 지원됩니다.

### 성공 기준

- **new-employee-onboarding** 스킬을 만들었습니다.
- **email-document** 스킬을 만들었습니다.
- 입력 매개변수 3개(EmployeeEmail, DocumentName, DocumentDescription)를 갖춘 **Email Document Flow** 에이전트 플로우를 만들었습니다.
- 플로우에 Office 365 Outlook을 통한 **Send an email (V2)** 작업이 구성되어 있습니다.
- 플로우에 이메일 전송 성공을 확인하는 출력 매개변수(EmailStatus)가 있습니다.
- 플로우가 게시되어 Copilot Studio에서 사용할 준비가 되었습니다.

### 추가 리소스

- [Create flows for Microsoft Copilot Studio](https://learn.microsoft.com/microsoft-copilot-studio/advanced-flow)
- [Office 365 Outlook connector](https://learn.microsoft.com/connectors/office365/)

## 챌린지 4: 토픽을 에이전트 플로우에 연결하고 엔드투엔드 테스트하기

### 소개

이전 챌린지에서 대화형 스킬 두 개(EmailDocument와 NewEmployeeOnboarding)를 만들고 문서 접근 요청 이메일을 보내는 Power Automate 에이전트 플로우를 만들었습니다.

이 챌린지에서는 엔드투엔드 테스트를 실행해 지식 검색 경험과 이메일 작업 플로우를 모두 검증합니다. 코파일럿이 직원 질문에 답하는 것과 직원을 대신해 실제 작업을 수행하는 것을 모두 확인하는 단계입니다.

### 챌린지 목표

- 지식 검색 경험을 테스트해 SharePoint 지식 기반에서 생성형 답변이 동작하는지 확인합니다.
- EmailDocument 토픽을 엔드투엔드로 테스트하고 문서 접근 요청 이메일이 받은 편지함에 도착하는지 검증합니다.

### 필수 조건

이 챌린지를 시작하기 전에 다음을 확인합니다.

- 챌린지 3을 완료했습니다(스킬 두 개와 **Email Document Flow** 생성).
- **Email Document Flow**가 Power Automate에서 게시되고 활성화되어 있습니다.
- 받은 이메일을 확인할 수 있도록 랩 이메일 받은 편지함에 접근 가능합니다.

### 완료 단계

#### 토픽 테스트하기

**미리 보기**(Preview) 버튼으로 테스트 패널을 엽니다.

##### 테스트 1. 지식 검색:

1. `Where can I find information about employee benefits?`를 물어보고, 에이전트가 SharePoint 지식 기반에서 온 관련성 높은 생성형 답변을 돌려주는지 확인합니다.

1. 두 번째 질의로 `What are the expense reimbursement policies?`를 시도하고, 같은 방식으로 플로우를 호출하지 않고 답변하는지 확인합니다.

   > **참고:** 에이전트는 챌린지 2에서 연결한 SharePoint 지식 원본을 활용해 지식 검색 질의에 자동으로 답변합니다.

##### 테스트 2. EmailDocument:

1. **새 테스트 세션**을 시작하고 `Raise a email document request`를 입력합니다. 대화를 진행하며 문서 이름(예: "HR Handbook"), 랩 이메일 주소, 간단한 사유(예: "Need to review HR policies")를 제공하고, 에이전트가 요청이 접수되었다고 보고하는지 확인합니다.

1. <inject key="AzureAdUserEmail"></inject> 받은 편지함에서 문서 이름, 사유, 요청자 이메일이 담긴 문서 접근 요청 이메일을 확인합니다.

### 성공 기준

- 지식 검색 테스트 질의가 SharePoint 지식 기반에서 온 정확한 생성형 답변을 돌려줍니다.
- EmailDocument 도구 테스트가 플로우를 트리거해 문서 접근 요청 이메일을 보냅니다.
- 이메일이 올바른 문서 이름, 사유, 요청자 정보와 함께 랩 받은 편지함에 도착합니다.

### 추가 리소스

- [Create topics with Copilot](https://learn.microsoft.com/microsoft-copilot-studio/nlu-authoring)
- [Call flows from topics](https://learn.microsoft.com/microsoft-copilot-studio/advanced-flow)
- [Work with variables](https://learn.microsoft.com/microsoft-copilot-studio/authoring-variables)

## 챌린지 5: Microsoft Teams에 에이전트 게시하기

### 소개

마지막 단계는 내부 지식 내비게이터 에이전트를 Microsoft Teams에 배포해 조직의 직원들이 사용할 수 있게 하는 것입니다. Teams는 직원들이 이미 협업하고 소통하는 자리에서 바로 도움을 받을 수 있어 지식 공유에 가장 적합한 채널입니다.

이 챌린지에서는 에이전트를 게시하고 Teams에 추가한 뒤 완전한 사용자 경험을 테스트합니다.

### 챌린지 목표

- Microsoft Teams에 에이전트를 게시합니다.
- Teams에서 토픽과 플로우를 테스트합니다.

### 완료 단계

#### 1단계: Microsoft Teams에 에이전트 게시하기

1. **Copilot Studio**에서 **Internal Knowledge Navigator** 에이전트의 **게시**(Publish) 드롭다운 페이지를 열고 **Teams and Microsoft 365 Copilot**을 선택합니다.

1. **Teams + Microsoft 365** 미리 보기에서 에이전트를 **저장 및 게시**(Save and Publish)합니다.

1. 미리 보기에서 Microsoft Teams로 에이전트를 엽니다(프롬프트가 나타나면 **Teams 웹 앱**을 계속 사용합니다). **Internal Knowledge Navigator** 앱을 설치하고 엽니다.

   > **참고:** 설치 옵션이 나타나지 않으면 이전 단계로 돌아가 채널을 다시 추가합니다.

#### 2단계: Teams에서 에이전트 테스트하기

챌린지 4에서 만든 토픽과 에이전트의 지식 검색을 이번에는 Teams 안에서 테스트합니다.

##### 지식 검색 테스트:

1. 에이전트 채팅에서 다음을 물어봅니다.

    ```
    Where can I find information about employee benefits?
    ```

1. 에이전트가 SharePoint 지식 기반을 검색해 관련성 높은 생성형 답변을 돌려주는지 확인합니다.

##### EmailDocument 토픽 테스트:

1. **새 테스트 세션**을 시작하거나 같은 세션을 계속 진행하며 다음을 보냅니다.

    ```
    Raise a email document request
    ```

1. 요청받으면 문서 이름, 자신의 이메일 주소, 간단한 사유를 제공하고, 에이전트가 요청이 접수되었다고 보고하는지 확인합니다.

1. <inject key="AzureAdUserEmail"></inject> 받은 편지함에서 문서 이름, 사유, 요청자 이메일이 담긴 문서 접근 요청 이메일을 확인합니다.

<validation step="d885b7bf-4f05-447b-b64b-8a412515d94d" />

> **축하합니다.** 챌린지를 완료했습니다. 이제 검증할 차례입니다. 단계는 다음과 같습니다.
> - 해당 챌린지의 검증(Validate) 버튼을 누릅니다. 성공 메시지가 나타나면 다음 챌린지로 진행할 수 있습니다.
> - 성공하지 못하면 오류 메시지를 자세히 읽고 랩 가이드의 지시에 따라 해당 단계를 다시 시도합니다.
> - 도움이 필요하면 cloudlabs-support@spektrasystems.com으로 문의하세요. 연중무휴 24시간 지원됩니다.

### 성공 기준

- Microsoft Teams에 에이전트를 게시했습니다.
- Teams에서 토픽과 플로우를 테스트했습니다.

### 추가 리소스

- [Publish your agent](https://learn.microsoft.com/microsoft-copilot-studio/publication-fundamentals-publish-channels)
- [Deploy to Microsoft Teams](https://learn.microsoft.com/microsoft-copilot-studio/publication-add-bot-to-microsoft-teams)
- [Analyze agent performance](https://learn.microsoft.com/microsoft-copilot-studio/analytics-overview)
- [Share your agent](https://learn.microsoft.com/microsoft-copilot-studio/admin-share-bots)

## 축하합니다!

Microsoft Copilot Studio로 **AI 기반 내부 지식 내비게이터 에이전트**를 성공적으로 만들었습니다.

### 실무 적용 분야

이 솔루션은 다음 영역의 지식 관리를 개선할 수 있습니다.

- **인사와 직원 서비스**: 온보딩, 정책, 복리후생 문의
- **IT 지원**: 셀프서비스 헬프데스크, 문서 접근
- **컴플라이언스와 교육**: 정책 배포, 절차 안내
- **영업 지원**: 플레이북, 제품 정보, 가격 가이드라인
- **운영**: 프로세스 문서화, 공급업체 관리, 조달 워크플로

이 챌린지를 완료하신 것을 축하합니다!

## 지원 연락처

CloudLabs 지원팀은 연중무휴 24시간 이메일과 라이브 챗으로 도움을 드립니다. 학습자와 강사를 위한 전용 지원 채널을 운영하여 모든 요청을 신속하고 효율적으로 처리합니다.

학습자 지원 연락처:

- 이메일 지원: cloudlabs-support@spektrasystems.com
- 라이브 챗 지원: https://cloudlabs.ai/labs-support

## Happy Hacking!!

![](images/auto-it-gt-gr-g2.png)
