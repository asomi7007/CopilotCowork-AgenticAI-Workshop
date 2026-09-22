# 코파일럿 코워크 및 코파일럿 스튜디오로 에이전틱 AI 대화 주도하기

> Microsoft Cloud Sandbox (CloudLabs by Spektra Systems) 랩 세션 가이드 모음입니다.
> 소매 회사 **자바 리테일(Zava Retail)** 시나리오 기반으로, Microsoft 365 코파일럿 · 코파일럿 코워크 · 코파일럿 스튜디오를 활용한 에이전틱 AI 실습 7개 랩으로 구성됩니다.

## 전체 구성

| # | 섹션 | 내용 | 예상 소요 시간 |
|---|------|------|--------------|
| 1 | [01-Windows-한국어-설정](./01-Windows-%ED%95%9C%EA%B5%AD%EC%96%B4-%EC%84%A4%EC%A0%95/) | Windows 표시 언어를 한국어로 변경하는 랩 VM 사전 설정 | - |
| 2 | [02-워크숍-개요](./02-%EC%9B%8C%ED%81%AC%EC%88%8D-%EA%B0%9C%EC%9A%94/) | 워크숍 개요, 목표, 필수 요구사항, 랩 환경 사용법 | 8시간 |
| 3 | [03-Lab1-마케팅-운영-에이전트](./03-Lab1-%EB%A7%88%EC%BC%80%ED%8C%85-%EC%9A%B4%EC%98%81-%EC%97%90%EC%9D%B4%EC%A0%84%ED%8A%B8/) | Microsoft 365 코파일럿으로 엔터프라이즈 마케팅 운영 에이전트 구축 | 40분 |
| 4 | [04-Lab2-코파일럿-코워크-일정-최적화](./04-Lab2-%EC%BD%94%ED%8C%8C%EC%9D%BC%EB%9F%BF-%EC%BD%94%EC%9B%8C%ED%81%AC-%EC%9D%BC%EC%A0%95-%EC%B5%9C%EC%A0%81%ED%99%94/) | 코파일럿 코워크(Copilot Cowork)로 AI 기반 일정 최적화 | 30분 |
| 5 | [05-Lab3-인력-역량-강화-에이전트](./05-Lab3-%EC%9D%B8%EB%A0%A5-%EC%97%AD%EB%9F%89-%EA%B0%95%ED%99%94-%EC%97%90%EC%9D%B4%EC%A0%84%ED%8A%B8/) | Microsoft 365 코파일럿으로 인력 역량 강화 에이전트 구축 | 30분 |
| 6 | [06-Lab4-코파일럿-스튜디오-보안-거버넌스](./06-Lab4-%EC%BD%94%ED%8C%8C%EC%9D%BC%EB%9F%BF-%EC%8A%A4%ED%8A%9C%EB%94%94%EC%98%A4-%EB%B3%B4%EC%95%88-%EA%B1%B0%EB%B2%84%EB%84%8C%EC%8A%A4/) | 코파일럿 스튜디오(Copilot Studio) 에이전트 보안 및 거버넌스 | 30분 |
| 7 | [07-Lab5-재무-에이전트](./07-Lab5-%EC%9E%AC%EB%AC%B4-%EC%97%90%EC%9D%B4%EC%A0%84%ED%8A%B8/) | Microsoft 365 코파일럿 재무 에이전트로 재무 보고 및 인수 모델링 최적화 | 30분 |
| 8 | [08-Lab6-에이전트-365-거버넌스-모니터링](./08-Lab6-%EC%97%90%EC%9D%B4%EC%A0%84%ED%8A%B8-365-%EA%B1%B0%EB%B2%84%EB%84%8C%EC%8A%A4-%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81/) | 에이전트 365(Agent 365)로 자바 리테일 에이전트 생태계 거버넌스 및 모니터링 | - |
| 9 | [09-Lab7-퀴즈-생성-프롬프트-액션](./09-Lab7-%ED%80%B4%EC%A6%88-%EC%83%9D%EC%84%B1-%ED%94%84%EB%A1%AC%ED%94%84%ED%8A%B8-%EC%95%A1%EC%85%98/) | 퀴즈 생성 에이전트의 토픽을 위한 프롬프트 액션 구현 | 40분 |

## 학습 목표 요약

- Workflows Agent(Frontier)와 Work IQ를 활용한 휴먼 인 더 루프 승인 기반 이메일 운영 도우미 구축
- Microsoft 365 코파일럿 챗을 활용한 엔터프라이즈 데이터 분석 및 다양한 형식의 결과물 생성 (Excel, Word, PowerPoint, Outlook, Teams)
- 코파일럿 코워크로 파일 분류·이름 변경, 거버넌스 감사, 앱 간 보고 조율
- 코파일럿 스튜디오에서 SharePoint 기반 코파일럿 에이전트 구축 및 다중 에이전트 오케스트레이션 설계
- 컴퓨터 사용 에이전트(CUA)로 API 없는 레거시 시스템과의 상호 작용 자동화
- 파워 앱스, 데이터버스, 파워 오토메이트와 통합된 자율 IT 지원 에이전트 구축

## 폴더 구조

```
CopilotCowork-AgenticAI-Workshop/
├── README.md            ← 이 파일 (세션 인덱스)
├── labfiles/            ← 공용 랩 자료 (Zava Retail 반품 정책)
└── 01~09 섹션 폴더/
    ├── README.md        ← 해당 섹션 랩 가이드 (전체 본문)
    ├── labfiles/         ← 해당 랩 실습 자료 파일
    └── images/           ← 섹션에 포함된 스크린샷
```

---

*본 문서는 CloudLabs 랩 가이드(원본: CloudLabsAI-Azure 워크숍 저장소)의 한국어 버전을 정리한 교육용 자료입니다.*
