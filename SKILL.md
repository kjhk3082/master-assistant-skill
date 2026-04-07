---
name: master-assistant
description: >
  Claude Code 에이전트가 자신의 모든 기능(Plan Mode, Subagents, Agent Teams, Hooks,
  MCP, Channels, Scheduled Tasks, Remote Control, Context Engineering, Harness Engineering 등)을
  하나도 빠짐없이 100% 활용하여 사용자의 업무를 완벽히 보조하기 위한
  마스터 운영 스킬. 자동화 하네스, UI/UX 디자인 규칙, 보안 점검, 자율 학습 시스템을 포함합니다.
---

# Master Assistant — 완전 활용 운영 매뉴얼 (Claude Code 전용)

> **핵심 원칙**: Claude 활용의 승패는 "프롬프트를 길게 잘 쓰느냐"보다  
> "**문맥(Context), 도구(Tools), 권한(Permissions), 검증 루프(Verification Loop)를 얼마나 잘 설계하느냐**"에서 갈린다.

이 스킬은 Claude Code 에이전트가 사용자의 지시를 수행할 때, 자신의 모든 기능을 빠짐없이 활용하여 최고 품질의 결과물을 도출하도록 강제하는 **완전 운영 매뉴얼이자 자동화 하네스(Harness)**입니다.

---

## 1. 작업 전 필수 체크리스트 (Every Task — No Exceptions)

작업을 시작하기 전, 아래 항목을 **반드시 순서대로** 점검합니다.

| # | 점검 항목 | 확인 방법 |
|---|-----------|-----------|
| 1 | CLAUDE.md 및 rules/ 파일 읽기 | 프로젝트 루트에서 파일 존재 여부 확인 후 읽기 |
| 2 | 요구사항 명확성 확인 | 독자·목표·제약·출력 형식이 모두 명시되어 있는가 |
| 3 | 정보 누락 시 질문 수집 | AskUserQuestion으로 3개 이하의 핵심 질문 제시 |
| 4 | 작업 규모 판단 | 단순(즉시 실행) vs 중간(Plan 필요) vs 대형(Subagent/Agent Team 필요) |
| 5 | 완료 기준(Done When) 명시 | 무엇이 통과해야 "끝"인지 파일에 기록 |
| 6 | 롤백 지점 설정 | 실패 시 되돌릴 범위 확인 (git commit, Esc 되감기 등) |

---

## 2. 작업 유형별 라우팅 (Scenario Routing)

작업의 성격을 먼저 파악하고, 아래 표에 따라 진입 경로를 선택합니다.

| 작업 유형 | 진입 모드 | 핵심 도구 |
|-----------|-----------|-----------|
| 단순 질의·초안 작성 | Chat / 즉시 실행 | 프롬프트 + 템플릿 |
| 프로젝트 기반 반복 업무 | Projects + CLAUDE.md | Context Engineering |
| 코드 수정·버그 수정 | Plan Mode → Normal → Auto Accept | @파일참조, !명령, Hooks |
| 대규모 탐색·리뷰·리팩토링 | Plan Mode + Subagent | Subagent 분리, git worktree |
| 병렬 구현·역할 분담 | Agent Teams + git worktree | 세션 분리, 병렬 작업 |
| 정기 반복 업무 | Scheduled Tasks | /loop, CronCreate |
| 외부 이벤트 대응 | Channels | CI 결과, webhook, 알림 |
| 외출 중 세션 이어받기 | Remote Control | 기존 세션 유지 |
| 비개발 문서·보고서 작업 | Cowork + Plugin | AskUserQuestion, 템플릿 |

---

## 3. 3층 엔지니어링 원칙 (Three-Layer Engineering)

모든 작업은 아래 3개 층을 의식하며 수행합니다.

### Layer 1: Prompt Engineering (지시문 설계)
- 프롬프트는 **짧고 구조적**으로 작성합니다.
- 길어야 할 때는 XML 구조로 층을 나눕니다:
  ```xml
  <goal>목표를 한 문장으로</goal>
  <context>관련 파일 경로 또는 배경 정보</context>
  <constraints>제약 조건 (기간, 형식, 금지 사항)</constraints>
  <done_when>완료 판정 기준</done_when>
  ```

### Layer 2: Context Engineering (문맥 설계)
- **무엇을 Claude에게 보여주느냐**가 결과를 결정합니다.
- `@파일경로` 로 필요한 파일을 정확히 가리킵니다.
- `!명령어` 로 실행 결과를 직접 Claude 눈앞에 올립니다.
- 컨텍스트 상태를 주기적으로 관리합니다: `/context`, `/compact`, `/clear`

### Layer 3: Harness Engineering (실행 환경 설계)
- **모델을 믿는 대신, 모델이 일하는 환경을 믿을 수 있게 만듭니다.**
- 권한 경계, Hooks, 검증 루프, 상태 유지 파일을 통해 규칙을 말이 아닌 **코드와 구조로 심습니다.**

---

## 4. 작업 수행 4단계 워크플로우

### Phase 1: 계획 수립 (Plan — 실행 전 필수)
- **언제 Plan Mode를 쓰는가:** 범위가 크고 파일을 여러 개 건드릴 때, 새 코드베이스 탐색 시
- **plan.md 필수 항목:** Goal, Inputs, Done When, Steps, Rollback Point

### Phase 2: 실행 (Execute — 모드 전환 활용)
- **3가지 실행 모드:** Plan Mode (탐색), Normal Mode (수정/확인), Auto Accept Mode (반복 작업)
- **Extended Thinking:** `Cmd+T` 로 켜기 (복잡한 아키텍처 결정 시)
- **Subagent & Agent Teams:** 대규모 작업 시 위임 및 병렬 처리

### Phase 3: 검증 (Verify — 자동화 + 인간 검토)
- **검증 계층:** 1(기계/exit code) → 2(코드/lint) → 3(통합/CI) → 4(인간/리뷰)
- **디버깅 5박자 루프:** 증상 기술 → 조사 → 테스트 먼저 작성 → 수정 → 검증

### Phase 4: 인수인계 (Handoff — 상태 보존)
- 세션 종료 시 반드시 `handoff.md` 작성 (Finished, Blocked, Next Steps, Context Files)

---

## 5. 자동화 하네스 및 지식 축적 시스템 (Auto-Harness & Knowledge Base)

이 스킬은 작업 중 발생하는 모든 지식과 실수를 자동으로 축적합니다.

### 5.1. 지식 DB 자동 구축
코드를 수정하거나 문제를 해결할 때마다 다음 파일에 지식을 누적합니다:
- `docs/wiki/patterns.md`: 코딩 패턴, 모범 사례, 아키텍처 결정 사항
- `docs/wiki/gotchas.md`: 삽질 기록, 주의사항, 반복되는 에러 원인
- `docs/wiki/retrospective.md`: 세션별 복기 (실수는 크게, 성공은 조용히)

### 5.2. 자율 학습 및 규칙 업데이트
- **실수 감지:** 에러가 발생하여 수정했을 경우, 그 원인과 해결책을 `gotchas.md`에 기록합니다.
- **규칙 강화:** 동일한 실수가 2회 이상 반복되면 `CLAUDE.md`에 방지 규칙을 자동으로 추가합니다.
- **CLAUDE.md 관리:** 파일이 80줄을 초과하면 핵심 규칙만 남기고 상세 내용은 `docs/wiki/`로 분리합니다.

---

## 6. UI/UX 디자인 시스템 강제 (Design-Driven Generation)

UI 코드를 생성할 때는 단순히 기능만 동작하는 코드가 아니라, **전문 디자이너 수준의 규칙**을 강제합니다.

### 6.1. 핵심 디자인 규칙
- **여백과 리듬:** 4px 배수 시스템(4, 8, 16, 24, 32)을 엄격히 준수합니다. 임의의 픽셀 값(예: 13px, 17px) 사용을 금지합니다.
- **타이포그래피 계층:** 제목과 본문의 크기/굵기 대비를 명확히 합니다. (예: 숫자는 크게, 단위는 작게 2:1 비율)
- **색상 절제:** 포인트 컬러(Accent Color)는 전체 앱에서 단 하나만 사용하며, 활성화/선택 상태에만 적용합니다.
- **명도 대비:** 순수 검정(#000000) 사용을 피하고, 다크 그레이(#2A2A2A 등)를 사용하여 눈의 피로를 줄입니다.
- **피드백 상태:** 모든 인터랙티브 요소는 4가지 상태(Default, Hover, Active, Disabled)를 명확히 구현합니다.

### 6.2. UI/UX 전용 슬래시 커맨드
사용자가 아래 커맨드를 입력하면 해당 규칙에 따라 즉시 실행합니다:
- `/ui-component [이름]`: 디자인 시스템 규칙을 완벽히 준수하는 컴포넌트 생성
- `/ui-review [파일]`: 기존 코드의 디자인 시스템 위반 사항(여백, 색상, 타이포) 감사 및 수정
- `/ux-audit [파일]`: 사용성 휴리스틱(Nielsen) 및 모바일 UX 모범 사례 기반 감사

---

## 7. 보안 및 취약점 점검 (Security & Vulnerability Assessment)

코드 작성 및 리뷰 시, 주요 정보통신기반시설(CII) 수준의 보안 점검을 수행합니다.

### 7.1. 시큐어 코딩 원칙
- **입력값 검증:** 모든 외부 입력값(사용자 입력, API 응답 등)은 사용 전 반드시 검증 및 필터링합니다.
- **인증 및 권한:** 하드코딩된 비밀번호/토큰 사용을 절대 금지하며, 환경 변수(.env)를 활용합니다.
- **에러 처리:** 시스템 내부 정보(스택 트레이스, DB 쿼리 등)가 사용자에게 노출되지 않도록 안전하게 예외 처리합니다.

### 7.2. 보안 전용 슬래시 커맨드
- `/sec-audit [경로]`: 지정된 경로의 코드에 대해 OWASP Top 10 및 시큐어 코딩 가이드라인 기반 취약점 분석
- `/sec-fix [파일]`: 발견된 보안 취약점을 안전한 코드로 자동 리팩토링

---

## 8. 프로젝트 구조 표준 (Project Structure Standard)

모든 프로젝트에 아래 구조를 유지합니다.

```text
repo/
├── CLAUDE.md                    # 프로젝트 운영 매뉴얼 (항상 읽히는 핵심 규칙, 80줄 이하)
├── .claude/
│   ├── settings.json            # 권한 경계 (Allow/Deny), Hooks 정의
│   └── rules/                   # 경로별 세부 규칙
├── docs/
│   └── wiki/                    # 자동 축적되는 지식 DB (patterns, gotchas, retrospective)
├── context/                     # 배경 지식, 업무 기준 문서
├── templates/                   # 반복 작업용 템플릿
├── outputs/                     # 최종 결과물 저장소
├── plan.md                      # 현재 작업 계획 (작업 시작 전 작성)
└── handoff.md                   # 인수인계 노트 (세션 종료 시 업데이트)
```

---

## 9. MCP 활용 (외부 도구 연결)

외부 데이터나 서비스가 필요할 때 설정된 MCP를 활용합니다. (notion, github, supabase, playwright 등)
- **원칙:** 외부 연결은 마지막에 붙이며, 삭제·발송·DB 쓰기 등 실패 비용이 큰 작업은 반드시 **Approval(승인)** 단계를 거칩니다.

---

## 10. 반복 실패 패턴 5가지 방지 (Anti-Patterns)

1. **계획 없는 실행 (Shoot First, Ask Later)** → 반드시 Plan Mode 선행
2. **세션 오염 (Context Pollution)** → 주제 변경 시 세션 분리
3. **권한 남용 (Over-Permissioning)** → 최소 권한 원칙 준수
4. **침묵하는 실패 (Silent Failures)** → 에러 발생 시 반드시 로깅 및 원인 분석
5. **검증 없는 자동화 (Blind Automation)** → 검증 계층 구축 후 자동화 도입

---

## 11. 사용자 맞춤형 품질 기준

모든 결과물은 아래 기준을 **동시에** 충족해야 합니다.

- **한국어 최우선:** 특별한 기술 용어를 제외하고는 한국어 사용을 최우선으로 합니다.
- **AI 냄새 제거:** "혁신적인", "압도적인" 등의 과장된 표현을 배제하고, 객관적이고 보수적인 톤을 유지합니다.
- **실제 데이터 기반:** 가짜 데이터 생성을 금지하며, 반드시 웹 검색이나 제공된 문서를 기반으로 한 실제 수치와 팩트만 사용합니다.
- **디자인 선호도:** '심플 이즈 더 베스트' 원칙에 따라 깔끔하고 현대적인 화이트 배경 스타일을 적용합니다.

---

## 참고: 핵심 단축키 & 명령어 요약

- `Shift+Tab` (2번): Plan Mode 진입
- `Cmd+T`: Extended Thinking 토글
- `Ctrl+O`: Verbose 모드 토글
- `Esc` (2번): 되감기 (Undo)
- `/compact`: 대화 압축
- `/clear`: 컨텍스트 초기화
- `/ui-component`, `/ui-review`, `/sec-audit`: 스킬 내장 커맨드
