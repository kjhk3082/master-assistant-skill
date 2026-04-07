# Master Assistant for Claude Code

<div align="center">
  <img src="https://img.shields.io/badge/Claude_Code-Skill-7B61FF?style=for-the-badge&logo=anthropic&logoColor=white" alt="Claude Code Skill" />
  <img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="License: MIT" />
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge" alt="PRs Welcome" />
</div>

<br/>

**Master Assistant**는 Claude Code 에이전트가 자신의 모든 기능(Plan Mode, Subagents, Agent Teams, Hooks, MCP, Channels, Scheduled Tasks, Remote Control 등)을 100% 활용하여 사용자의 업무를 완벽히 보조하도록 강제하는 **완전 활용 운영 매뉴얼 스킬**입니다.

이 스킬은 베스트셀러 프롬프트 엔지니어링 가이드인 **'시키는 기술'**과 Anthropic의 **'Claude Code & Cowork Master Guide'**의 모든 핵심 인사이트를 집대성하여 제작되었습니다.

## 🌟 주요 기능 (Key Features)

- **작업 전 필수 체크리스트 강제**: 요구사항 명확성, 작업 규모 판단, 완료 기준(Done When) 설정, 롤백 지점 설정을 강제합니다.
- **작업 유형별 스마트 라우팅**: 단순 질의부터 대규모 리팩토링, 병렬 구현까지 작업 성격에 맞는 최적의 모드(Plan/Normal/Auto Accept)와 도구를 선택합니다.
- **3층 엔지니어링 (Three-Layer Engineering)**:
  - **Prompt Engineering**: 짧고 구조적인 지시문 작성 (XML 구조 활용)
  - **Context Engineering**: `@파일참조`, `!명령어` 주입, `/context`, `/compact`, `/clear`를 통한 문맥 오염 방지
  - **Harness Engineering**: 권한 경계, Hooks, 검증 루프를 통한 실행 환경 설계
- **4단계 워크플로우 (Plan → Execute → Verify → Handoff)**: 계획 수립부터 인수인계까지 체계적인 작업 수행을 보장합니다.
- **디버깅 5박자 루프**: 증상 기술 → 조사 → 테스트 작성 → 수정 → 검증의 체계적인 디버깅 프로세스를 따릅니다.
- **반복 실패 패턴 방지**: 계획 없는 실행, 세션 오염, 검증 없는 자동화 등 흔한 실패 패턴을 원천 차단합니다.

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

명시적으로 스킬을 호출하려면 다음과 같이 지시하세요:

```
@master-assistant 스킬의 체크리스트에 따라 이 프로젝트의 리팩토링 계획을 세워줘.
```

## 📁 프로젝트 구조 표준 (Harness 설계)

이 스킬은 프로젝트 내에 다음과 같은 구조를 유지할 것을 권장합니다:

```text
repo/
├── CLAUDE.md                    # 프로젝트 운영 매뉴얼
├── .claude/
│   ├── settings.json            # 권한 경계 및 Hooks 정의
│   └── rules/                   # 경로별 세부 규칙
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
