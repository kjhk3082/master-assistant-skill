# Master Assistant for Claude Code

<div align="center">
  <img src="https://img.shields.io/badge/Claude_Code-Skill-7B61FF?style=for-the-badge&logo=anthropic&logoColor=white" alt="Claude Code Skill" />
  <img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="License: MIT" />
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge" alt="PRs Welcome" />
</div>

<br/>

**Master Assistant**는 Claude Code 에이전트가 자신의 모든 기능(Plan Mode, Subagents, Agent Teams, Hooks, MCP, Channels, Scheduled Tasks, Remote Control 등)을 100% 활용하여 사용자의 업무를 완벽히 보조하도록 강제하는 **완전 활용 운영 매뉴얼 스킬**입니다.

이 스킬은 베스트셀러 프롬프트 엔지니어링 가이드인 **'시키는 기술'**과 Anthropic의 **'Claude Code & Cowork Master Guide'**의 핵심 인사이트를 집대성했을 뿐만 아니라, **자동화 하네스(Auto-Harness), UI/UX 디자인 시스템, 보안 점검(Security Audit)** 기능까지 통합하여 제작되었습니다.

## 🌟 주요 기능 (Key Features)

### 1. 자율 학습 및 지식 축적 시스템 (Auto-Harness)
- **실수 학습 루프**: 에러 발생 시 원인을 분석하고 `docs/wiki/gotchas.md`에 기록하여 같은 실수를 반복하지 않습니다.
- **패턴 자동 추출**: 반복되는 코딩 패턴을 감지하여 `docs/wiki/patterns.md`에 모범 사례로 저장합니다.
- **세션 자동 복기**: 세션 종료 시 `retrospective.md`를 작성하여 "실수는 크게, 성공은 조용히" 기록합니다.

### 2. UI/UX 디자인 시스템 강제 (Design-Driven Generation)
- **전문가 수준의 UI 규칙**: 4px 배수 시스템, 명확한 타이포그래피 계층, 절제된 색상 사용(단일 포인트 컬러)을 강제합니다.
- **슬래시 커맨드 지원**:
  - `/ui-component`: 디자인 시스템을 완벽히 준수하는 컴포넌트 생성
  - `/ui-review`: 기존 코드의 여백, 색상, 타이포그래피 위반 사항 감사
  - `/ux-audit`: 사용성 휴리스틱(Nielsen) 기반 UX 감사

### 3. 보안 및 취약점 점검 (Security Assessment)
- **시큐어 코딩 원칙**: 입력값 검증, 안전한 인증/권한 관리, 에러 처리 가이드라인을 준수합니다.
- **보안 커맨드 지원**:
  - `/sec-audit`: OWASP Top 10 기반 취약점 분석
  - `/sec-fix`: 발견된 취약점을 안전한 코드로 자동 리팩토링

### 4. 3층 엔지니어링 (Three-Layer Engineering)
- **Prompt Engineering**: 짧고 구조적인 지시문 작성 (XML 구조 활용)
- **Context Engineering**: `@파일참조`, `!명령어` 주입, `/context`, `/compact`, `/clear`를 통한 문맥 오염 방지
- **Harness Engineering**: 권한 경계, Hooks, 검증 루프를 통한 실행 환경 설계

### 5. 4단계 워크플로우 (Plan → Execute → Verify → Handoff)
- **작업 전 필수 체크리스트 강제**: 요구사항 명확성, 작업 규모 판단, 완료 기준(Done When) 설정, 롤백 지점 설정을 강제합니다.
- **디버깅 5박자 루프**: 증상 기술 → 조사 → 테스트 작성 → 수정 → 검증의 체계적인 디버깅 프로세스를 따릅니다.

## 🚀 설치 방법 (Installation)

### Claude Code에서 직접 설치 (추천)

Claude Code 터미널에서 아래 명령어를 실행하여 스킬을 설치하세요:

```bash
# 스킬 디렉토리로 이동하여 설치
claude skill add https://github.com/YOUR_USERNAME/master-assistant-skill
```

### 수동 설치

1. 이 저장소를 클론하거나 다운로드합니다.
2. `SKILL.md` 파일을 프로젝트의 `.claude/skills/master-assistant/` 디렉토리에 복사합니다.

## 💡 사용 방법 (Usage)

스킬이 설치되면 Claude Code는 작업을 시작할 때 자동으로 이 매뉴얼을 참조합니다. 

명시적으로 스킬을 호출하거나 내장 커맨드를 사용하려면 다음과 같이 지시하세요:

```
@master-assistant 스킬의 체크리스트에 따라 이 프로젝트의 리팩토링 계획을 세워줘.
```
```
/ui-component 로그인 폼을 만들어줘.
```
```
/sec-audit src/auth/ 디렉토리의 보안 취약점을 점검해줘.
```

## 📁 프로젝트 구조 표준 (Harness 설계)

이 스킬은 프로젝트 내에 다음과 같은 구조를 유지할 것을 권장합니다:

```text
repo/
├── CLAUDE.md                    # 프로젝트 운영 매뉴얼 (80줄 이하 유지)
├── .claude/
│   ├── settings.json            # 권한 경계 및 Hooks 정의
│   └── rules/                   # 경로별 세부 규칙
├── docs/
│   └── wiki/                    # 자동 축적되는 지식 DB (patterns, gotchas, retrospective)
├── context/                     # 배경 지식, 업무 기준 문서
├── templates/                   # 반복 작업용 템플릿
├── outputs/                     # 최종 결과물 저장소
├── plan.md                      # 현재 작업 계획
└── handoff.md                   # 인수인계 노트
```

## 🤝 기여하기 (Contributing)

이 스킬을 개선하기 위한 기여를 환영합니다! 
버그 리포트, 기능 제안, 풀 리퀘스트 모두 환영합니다.

1. 이 저장소를 포크합니다.
2. 새 브랜치를 생성합니다 (`git checkout -b feature/amazing-feature`).
3. 변경 사항을 커밋합니다 (`git commit -m 'Add some amazing feature'`).
4. 브랜치에 푸시합니다 (`git push origin feature/amazing-feature`).
5. 풀 리퀘스트를 엽니다.

## 📄 라이선스 (License)

이 프로젝트는 MIT 라이선스에 따라 배포됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.
