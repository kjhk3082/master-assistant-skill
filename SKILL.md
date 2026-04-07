---
name: master-assistant
description: >
  Claude Code 에이전트가 자신의 모든 기능(Plan Mode, Subagents, Agent Teams, Hooks,
  MCP, Channels, Scheduled Tasks, Remote Control, Context Engineering, Harness Engineering 등)을
  하나도 빠짐없이 100% 활용하여 사용자의 업무를 완벽히 보조하기 위한
  마스터 운영 스킬. '시키는 기술'과 'Claude Code & Cowork Master Guide'의 모든 인사이트를 집대성.
---

# Master Assistant — 완전 활용 운영 매뉴얼 (Claude Code 전용)

> **핵심 원칙**: Claude 활용의 승패는 "프롬프트를 길게 잘 쓰느냐"보다  
> "**문맥(Context), 도구(Tools), 권한(Permissions), 검증 루프(Verification Loop)를 얼마나 잘 설계하느냐**"에서 갈린다.

이 스킬은 Claude Code 에이전트가 사용자의 지시를 수행할 때, 자신의 모든 기능을 빠짐없이 활용하여 최고 품질의 결과물을 도출하도록 강제하는 **완전 운영 매뉴얼**입니다.

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
- 나쁜 예: `"회원가입 에러 좀 고쳐줘"`
- 좋은 예:
  ```
  먼저 CLAUDE.md와 src/features/signup/을 읽어.
  빈 값 제출 버그를 바로 고치지 말고,
  1. 재현 경로 2. 원인 가설 3. 수정 범위 4. 테스트 계획을 6줄 이하로 먼저 요약해.
  승인 후 구현하고 pnpm test -- signup 결과까지 남겨.
  ```
- 길어야 할 때는 XML 구조로 층을 나눕니다:
  ```xml
  <goal>목표를 한 문장으로</goal>
  <context>관련 파일 경로 또는 배경 정보</context>
  <constraints>제약 조건 (기간, 형식, 금지 사항)</constraints>
  <done_when>완료 판정 기준</done_when>
  ```

### Layer 2: Context Engineering (문맥 설계)
- **무엇을 Claude에게 보여주느냐**가 결과를 결정합니다.
- `@파일경로` 로 필요한 파일을 정확히 가리킵니다. (예: `@src/auth/middleware.ts`, `@config.ts#10-20`)
- `!명령어` 로 실행 결과를 직접 Claude 눈앞에 올립니다. (예: `!npm run test`, `!git log --oneline -10`)
- 컨텍스트 상태를 주기적으로 관리합니다:
  - `/context` — 현재 컨텍스트 사용량 확인 (70% 초과 시 정리)
  - `/compact` — 작업 단위 완료 후 대화 압축 (핵심만 남기기)
  - `/clear` — 완전히 다른 작업으로 전환 시 초기화
- 컨텍스트 오염 방지: **작업 성격이 바뀌는 순간 = 세션을 끊어야 하는 순간**

### Layer 3: Harness Engineering (실행 환경 설계)
- **모델을 믿는 대신, 모델이 일하는 환경을 믿을 수 있게 만듭니다.**
- 권한 경계, Hooks, 검증 루프, 상태 유지 파일을 통해 규칙을 말이 아닌 **코드와 구조로 심습니다.**

---

## 4. 작업 수행 4단계 워크플로우

### Phase 1: 계획 수립 (Plan — 실행 전 필수)

**언제 Plan Mode를 쓰는가:**
- 범위가 크고 파일을 여러 개 건드릴 때
- 새 코드베이스를 처음 탐색할 때
- 정답이 없는 아키텍처 결정을 내릴 때

**Plan Mode 진입 방법:** `Shift+Tab` 두 번 눌러 Plan 모드 진입 (파일에 손 대지 않고 탐색만)

**plan.md 필수 항목:**
```markdown
# Plan
## Goal
(한 문장으로 목표 기술)

## Inputs
- 관련 파일 목록
- 참고 문서

## Done When
- [ ] 완료 조건 1
- [ ] 완료 조건 2
- [ ] 테스트 통과 조건

## Steps
1. 단계 1
2. 단계 2
...

## Rollback Point
- 되돌릴 범위 (예: src/features/signup/ 하위 파일만)
```

**승인 후 실행:** 계획을 사용자에게 제시하고 승인을 받은 뒤 실행에 돌입합니다.

---

### Phase 2: 실행 (Execute — 모드 전환 활용)

**3가지 실행 모드 (Shift+Tab으로 순환):**

| 모드 | 용도 | 전환 타이밍 |
|------|------|-------------|
| **Plan Mode** | 탐색·분석·이해 (파일 수정 없음) | 작업 시작 시, 새 코드베이스 탐색 시 |
| **Normal Mode** | 수정·확인·승인 (변경 전 검토) | 원인 파악 후 수정 시 |
| **Auto Accept Mode** | 반복·일괄 작업 (자동 승인) | 테스트 파일 일괄 업데이트 등 반복 작업 |

**@참조와 !명령 활용:**
- `@src/cart/` — 폴더 단위 참조
- `@config.ts#10-20` — 라인 범위 지정 참조
- `!npm run test --reporter=verbose` — 테스트 결과 직접 주입
- `!git log --oneline -10` — 최근 커밋 이력 주입

**Extended Thinking 활용:**
- `Cmd+T` 로 켜기 — 복잡한 아키텍처 결정, 의존성 분석, 마이그레이션 전략 시 사용
- 프롬프트에 `ultrathink` 포함 — 추론 강도 최대화 (시스템 전체 재설계 등 최고 난이도 작업 시)
- 단순 작업에는 끄기 (불필요한 토큰 낭비 방지)

**Verbose 모드 활용:**
- `Ctrl+O` 로 켜기 — Claude의 작업 과정 실시간 관찰
- 결과가 이상할 때 원인 파악 및 지시 개선에 활용

**Subagent 활용 (메인 세션 문맥 보호):**
- 대규모 코드 탐색, 독립적 리뷰, 리스크 점검은 Subagent에게 위임
- 예시 지시: `"이 변경 사항의 보안 리스크를 Subagent가 독립적으로 검토해 줘"`
- Subagent는 도구 권한, 출력 형식, 컨텍스트를 분리하여 운영

**Agent Teams 활용 (병렬 대형 작업):**
- 완료 기준과 역할 분리가 이미 선명한 경우에만 사용
- git worktree와 세션 분리 조합:
  ```bash
  git worktree add /app-auth -b feature/auth main
  git worktree add /app-perf -b fix/performance main
  # 각 디렉토리에서 독립 세션 실행
  claude -n "인증-기능"
  claude -n "성능-개선"
  ```

**되감기 활용 (실패를 워크플로의 일부로):**
- `Esc` 두 번 — 파일과 대화를 이전 시점으로 되돌리기
- 되감기는 실수가 아니라 **계획된 실험**입니다. 첫 시도의 정보를 활용해 두 번째 지시를 더 정확하게 합니다.

---

### Phase 3: 검증 (Verify — 자동화 + 인간 검토)

**검증 계층 (낮은 비용부터 순서대로 쌓기):**

| 계층 | 내용 | 방법 |
|------|------|------|
| 1 (기계) | 명령 exit code | Hooks 자동 실행 |
| 2 (코드) | lint, typecheck, unit test | PostToolUse Hook |
| 3 (통합) | integration, e2e, screenshot | CI 연동 |
| 4 (인간) | human review + rollback plan | 사용자 최종 확인 |

**Hooks 설정 (`.claude/settings.json`):**
```json
{
  "permissions": {
    "allow": ["Read", "Edit", "Write", "Glob", "Grep",
              "Bash(pnpm test)", "Bash(pnpm lint)"],
    "deny": ["Read(./.env)", "Read(./.env.*)", "Bash(rm -rf *)"]
  },
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [{"type": "command", "command": "pnpm lint"}]
      }
    ],
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [{"type": "command", "command": ".claude/hooks/block-dangerous.sh"}]
      }
    ],
    "Stop": [
      {
        "hooks": [{"type": "command", "command": ".claude/hooks/save-session-log.sh"}]
      }
    ],
    "Notification": [
      {
        "hooks": [{"type": "command", "command": "osascript -e 'display notification \"Claude 작업 완료\" with title \"Claude Code\"'"}]
      }
    ]
  }
}
```

**Hooks 4가지 시점:**
- `PostToolUse` — 도구 사용 직후 (prettier 자동 실행, 린트 검사)
- `PreToolUse` — 도구 사용 직전 (위험 명령 차단: rm -rf, curl | bash 등)
- `Stop` — 세션 종료 시 (활동 로그 저장)
- `Notification` — Claude 알림 발생 시 (macOS 알림으로 비동기 작업 완료 통보)

**디버깅 5박자 루프:**
1. **증상 기술** — "장바구니에 3개 넣으면 총액이 2개 값만 나와요" (구체적으로)
2. **조사** — Plan Mode에서 `@src/cart/` 참조하며 원인 후보 탐색
3. **테스트 먼저 작성** — 증상을 재현하는 테스트 코드 작성
4. **수정** — 원인 파악 후 Normal Mode에서 수정
5. **검증** — `!npm run test` 로 테스트 통과 확인 → 실패 시 3번으로 복귀

---

### Phase 4: 인수인계 (Handoff — 상태 보존)

**세션 종료 또는 작업 완료 시 반드시 `handoff.md` 작성:**

```markdown
# Handoff — [날짜] [작업명]

## Finished
- 완료된 작업 목록

## Blocked / Risks
- 미해결 이슈
- 잠재적 위험 요소

## Next Steps
- 다음 권장 단계 (우선순위 순)

## Context Files
- 참고한 주요 파일 목록

## Test Status
- 통과한 테스트
- 실패 중인 테스트 (있다면)
```

**세션 관리:**
- `claude -n "작업명"` — 새 세션에 이름 붙여 시작
- `claude -c` — 가장 최근 세션 이어가기
- `/resume` — 세션 목록에서 선택하여 복귀
- **작업 성격이 바뀌면 반드시 세션을 분리합니다** (기능 구현 → 버그 수정 → 리팩토링은 각각 별도 세션)

---

## 5. 프로젝트 구조 표준 (Harness 설계)

모든 프로젝트에 아래 구조를 유지합니다.

```text
repo/
├── CLAUDE.md                    # 프로젝트 운영 매뉴얼 (항상 읽히는 핵심 규칙)
├── .claude/
│   ├── settings.json            # 권한 경계 (Allow/Deny), Hooks 정의
│   ├── hooks/
│   │   ├── block-dangerous.sh   # 위험 명령 차단 (PreToolUse)
│   │   └── save-session-log.sh  # 세션 로그 저장 (Stop)
│   └── rules/                   # 경로별 세부 규칙
│       ├── api.md               # API 관련 규칙
│       ├── testing.md           # 테스트 규칙
│       └── frontend.md          # 프론트엔드 규칙
├── context/                     # 배경 지식, 회사 소개, 업무 기준 문서
│   ├── company-profile.md       # 회사 정보
│   ├── brand-guidelines.md      # 브랜드 가이드라인
│   └── working-rules.md         # 현장 운영 규칙
├── templates/                   # 반복 작업용 템플릿
│   ├── weekly-brief.md          # 주간 브리프 템플릿
│   ├── meeting-notes.md         # 회의록 템플릿
│   ├── client-report.md         # 고객 보고서 템플릿
│   └── prd-template.md          # PRD 템플릿
├── outputs/                     # 최종 결과물 저장소 (날짜-목적 형식)
│   └── 2026-04-08-weekly-brief.md
├── plan.md                      # 현재 작업 계획 (작업 시작 전 작성)
└── handoff.md                   # 인수인계 노트 (세션 종료 시 업데이트)
```

**CLAUDE.md 작성 원칙:**
- **짧게 유지** — 항상 지켜야 할 핵심만 (긴 참고 문서는 context/로 분리)
- **경로별 규칙 분리** — 프론트엔드/백엔드/인프라 규칙을 한 장에 몰지 않기
- **파일명 규칙** — `2026-03-23-meeting-notes.md` 처럼 날짜+목적+대상 포함

**CLAUDE.md 기본 템플릿:**
```markdown
# 프로젝트명 — 운영 매뉴얼

## 이 프로젝트는
(한 문장으로 목적 기술)

## 핵심 규칙
- 코드 수정 전 반드시 plan.md 작성
- 세션 종료 전 handoff.md 업데이트
- 삭제/배포/발송 전 반드시 승인 요청

## 기술 스택
(사용 언어, 프레임워크, 주요 라이브러리)

## 금지 사항
- .env 파일 직접 수정 금지
- rm -rf 명령 금지
- 프로덕션 DB 직접 쓰기 금지

## 참고 문서
- context/company-profile.md
- context/brand-guidelines.md
```

---

## 6. MCP 활용 (외부 도구 연결)

외부 데이터나 서비스가 필요할 때 설정된 MCP를 활용합니다.

| MCP 서버 | 활용 상황 |
|----------|-----------|
| `notion` | 회사 문서 읽기/쓰기, 데이터베이스 관리 |
| `github` | 코드 저장소 관리, PR 생성, 이슈 트래킹 |
| `supabase` | 데이터베이스 조회, KPI 데이터 수집 |
| `gmail` | 이메일 초안 작성, 발송 (승인 후) |
| `instagram` | SNS 콘텐츠 발행 (승인 후) |
| `firecrawl` | 웹 스크래핑, 경쟁사 조사 |
| `playwright` | 브라우저 자동화, UI 테스트 |
| `cloudflare` | 배포, KV 저장소, R2 스토리지 |

**MCP 활용 원칙:**
- 외부 연결은 **마지막에 붙입니다** (규칙과 검증이 없으면 연결이 더 위험해짐)
- 삭제·발송·DB 쓰기 등 실패 비용이 큰 작업은 반드시 **Approval(승인)** 단계 포함

---

## 7. Scheduled Tasks & Channels 활용

### Scheduled Tasks (예약 실행)
**언제 사용하는가:** 정해진 시간에 반복 실행이 필요한 업무

```bash
# 매주 월요일 경쟁사 브리프 자동 생성
/schedule "매주 월요일 오전 9시, context/competitors/를 읽고 weekly-brief 템플릿으로 초안 생성 후 outputs/에 저장"

# CronCreate 활용
CronCreate("0 9 * * 1", "주간 경쟁사 브리프 생성")
```

**적합한 업무:** 주간 경쟁사 브리핑, 매일 아침 업무 요약, 정기 KPI 보고, 반복 리뷰

### Channels (외부 이벤트 대응)
**언제 사용하는가:** CI 결과, 모니터링 경보, 채팅 메시지 등 외부 사건이 발생했을 때

- CI 실패 → 기존 디버깅 세션으로 자동 전달
- 모니터링 경보 → 즉시 세션에서 대응
- Telegram/Discord 메시지 → Claude 세션과 연결

### Remote Control (원격 이어받기)
**언제 사용하는가:** 외출 중 이미 실행 중인 세션을 이어받아 짧은 승인·지시가 필요할 때

- 장기 실행 작업의 중간 승인
- 이동 중 간단한 방향 조정
- 사무실 컴퓨터의 기존 세션을 폰에서 이어받기

---

## 8. 자동화 경계선 (안전한 자동화의 기준)

자동화는 편리하지만, **구조 없이 자동화하면 어지러운 방에서 더 빨리 물건을 쌓는 것**과 같습니다.

**자동화 도입 순서 (반드시 이 순서로):**
1. CLAUDE.md와 rules/로 기본 규칙 고정
2. 검증(Hooks, CI)으로 안전망 구축
3. plan.md, handoff.md로 상태 외부화
4. Skill과 Plugin으로 반복 절차 재사용
5. MCP로 외부 연결 추가
6. Scheduled Tasks, Channels로 자동화

**Auto Accept 모드 사용 기준:**
- CLAUDE.md가 충분히 잘 짜여 있을 때
- 테스트가 있고 되감기 가능한 상황일 때
- 반복적인 작업(테스트 파일 일괄 업데이트 등)일 때
- **보안 민감 코드, 프로덕션 영향 변경은 반드시 Normal Mode 사용**

**위험 작업 3종 (반드시 승인 요청):**
- 삭제 (파일, DB 레코드, 배포 롤백)
- 배포 (프로덕션 환경 변경)
- 발송 (이메일, SNS 게시, 외부 API 쓰기)

---

## 9. 직무별 활용 패턴 (사용자 업무 맞춤)

### CEO / 전략 기획 업무
```
context/에 회사 소개, 시장 분석, 경쟁사 자료 보관
→ "이번 분기 전략 방향을 context/market-analysis.md 기반으로 정리해줘"
→ Scheduled Tasks로 주간 경쟁사 브리프 자동화
```

### 마케팅 / 콘텐츠 업무
```
context/에 브랜드 가이드라인, 고객 페르소나 보관
→ Projects 모드에서 브랜드 톤 유지하며 콘텐츠 생성
→ instagram MCP로 승인 후 자동 발행
```

### 개발 / 제품 기획 업무
```
CLAUDE.md에 기술 스택, 코딩 컨벤션, 금지 사항 명시
→ Plan Mode로 기능 설계 → Normal로 구현 → Hooks로 자동 검증
→ Subagent로 코드 리뷰 분리
```

### 보고서 / 문서 작업
```
templates/에 보고서 형식 보관
→ "client-report-template.md를 읽고 지난 7일 변화만 반영한 초안 작성"
→ outputs/client-a/에 날짜 포함 파일명으로 저장
```

---

## 10. 반복 실패 패턴 방지 (5가지 금지 사항)

아래는 Claude Code 사용자들이 가장 자주 빠지는 실패 패턴입니다. **이 에이전트는 이 패턴을 절대 반복하지 않습니다.**

| # | 실패 패턴 | 올바른 대응 |
|---|-----------|-------------|
| 1 | 계획 없이 즉시 실행 | 반드시 plan.md 작성 후 승인 받기 |
| 2 | 하나의 세션에서 모든 작업 처리 | 작업 성격 변경 시 세션 분리 |
| 3 | 컨텍스트 오염 방치 | /context 확인 → /compact → /clear 순서로 관리 |
| 4 | 규칙을 프롬프트로만 지시 | Hooks와 settings.json으로 코드에 심기 |
| 5 | 검증 없이 자동화 | 검증 계층 구축 후 자동화 도입 |

---

## 11. 사용자 맞춤형 품질 기준

모든 결과물은 아래 기준을 **동시에** 충족해야 합니다.

**문체 및 표현:**
- **AI 냄새 제거**: 기계적·획일적 어투를 피하고, 전문가가 직접 작성한 듯한 자연스럽고 세련된 문체 사용
- **쉬운 설명**: 복잡한 기술 용어는 비전문가도 이해할 수 있도록 풀어서 설명
- **완벽한 구현**: 1부터 100까지 상세하고 빠짐없이 담기

**데이터 및 근거:**
- **실제 레퍼런스**: 모든 데이터와 주장은 실제 웹 검색 기반의 검증 가능한 출처 명시
- **할루시네이션 금지**: AI가 생성한 정보는 반드시 검증 후 사용
- **RFP/요구사항 100% 준수**: 요청된 내용을 하나도 빠짐없이 반영

**형식 및 가독성:**
- **한국어 우선**: 기본 언어는 한국어, 한글 폰트 깨짐 방지
- **표와 시각화 활용**: 복잡한 정보는 표·다이어그램으로 정리
- **파일명 규칙**: `2026-04-08-작업명.md` 형식으로 날짜 포함

---

## 12. 긴급 상황 대응 체크리스트

**Claude가 이상한 결과를 낼 때:**
1. `/context` — 컨텍스트 사용량 확인 (70% 초과 시 원인)
2. `Ctrl+O` (Verbose 모드) — 어떤 파일을 보고 있는지 확인
3. `Esc` 두 번 — 이전 상태로 되감기
4. `/compact` — 대화 압축 후 재시도
5. `/clear` + 새 세션 — 완전 초기화

**작업이 막혔을 때:**
1. Plan Mode로 전환하여 문제 재탐색
2. `ultrathink` 키워드로 심층 추론 요청
3. Subagent에게 독립적 분석 위임
4. 사용자에게 AskUserQuestion으로 추가 정보 요청

---

## 참고: 핵심 단축키 & 명령어 요약

| 단축키/명령 | 기능 |
|-------------|------|
| `Shift+Tab` | Plan → Normal → Auto Accept 모드 순환 |
| `Cmd+T` | Extended Thinking 토글 |
| `Ctrl+O` | Verbose 모드 토글 |
| `Esc` × 2 | 되감기 (이전 상태 복원) |
| `@경로` | 파일/폴더 직접 참조 |
| `!명령` | bash 명령 실행 결과 컨텍스트 주입 |
| `/context` | 컨텍스트 사용량 확인 |
| `/compact` | 대화 압축 (핵심만 유지) |
| `/clear` | 컨텍스트 완전 초기화 |
| `/resume` | 이전 세션 복귀 |
| `claude -n "이름"` | 이름 붙인 새 세션 시작 |
| `claude -c` | 최근 세션 이어가기 |
| `ultrathink` | Extended Thinking 최대 강도 |
