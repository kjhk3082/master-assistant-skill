# 마스터 어시스턴트 스킬 (Claude Code용)

![Hero Banner](assets/hero-banner.png)

엄격하고 전문적인 소프트웨어 개발 워크플로우를 강제하는 Claude Code용 실전 테스트 완료 스킬 프레임워크입니다.

단순한 프롬프트 템플릿과 달리, 이것은 컨텍스트에 따라 자동으로 트리거되는 **상호 연결된 스킬 컬렉션**으로, Claude Code가 작업을 제대로 계획하고, 검증하고, 문서화하도록 강제합니다.

## 🌟 왜 사용해야 하나요?

기본적으로 Claude Code는 강력하지만 혼란스러울 수 있습니다. 묻지 않고 파일을 덮어쓰거나, 테스트를 건너뛰거나, 세션 간에 컨텍스트를 잃어버릴 수 있습니다.

이 스킬 컬렉션은 **4단계 워크플로우**를 강제하여 이 문제를 해결합니다:

![Workflow Diagram](assets/workflow.png)

1. **계획 (Plan)**: 코딩 전에 Claude가 브레인스토밍하고 `plan.md`를 작성하도록 강제합니다.
2. **실행 (Execute)**: 보안 및 UI/UX 검사와 함께 단계별 구현을 강제합니다.
3. **검증 (Verify)**: 테스트/린터가 통과할 때까지 Claude가 성공을 선언하지 못하게 합니다.
4. **핸드오프 (Handoff)**: 컨텍스트를 보존하기 위해 자동으로 `handoff.md`를 생성합니다.

## 📦 설치 방법

### 옵션 1: Claude Code 플러그인 마켓플레이스 (권장)
```bash
/plugin marketplace add kjhk3082/master-assistant-skill
/plugin install master-assistant-skill
```

### 옵션 2: 수동 설치
이 레포지토리를 전역 또는 프로젝트별 스킬 디렉토리에 클론합니다:
```bash
# 전역 설치
git clone https://github.com/kjhk3082/master-assistant-skill.git ~/.claude/skills/master-assistant

# 프로젝트별 설치
git clone https://github.com/kjhk3082/master-assistant-skill.git .claude/skills/master-assistant
```

## 🛠️ 포함된 기능

이 레포지토리에는 함께 작동하는 특수 스킬 제품군이 포함되어 있습니다:

| 스킬 | 자동 트리거 조건 | 목적 |
|-------|---------------------------|---------|
| `master-assistant` | **항상 활성** | 워크플로우를 오케스트레이션하고 하위 스킬로 라우팅합니다. |
| `brainstorming` | 새로운 기능/아이디어 | 명확한 질문을 하고 설계 승인을 받습니다. |
| `planning` | 승인된 설계 | 단계별 `plan.md`를 작성합니다. |
| `debugging` | 에러 또는 버그 | 수정 전에 4단계 근본 원인 분석을 강제합니다. |
| `ui-ux` | 프론트엔드 변경 | 디자인 시스템, 접근성 및 4px 그리드를 강제합니다. |
| `security` | 백엔드/데이터 변경 | 입력 유효성 검사 및 안전한 코딩 관행을 강제합니다. |
| `review` | 완료된 단계 | 코드 품질 및 테스트 커버리지를 검증합니다. |

## ⌨️ 커스텀 슬래시 커맨드

포함된 슬래시 커맨드를 사용하여 수동으로 스킬을 트리거할 수도 있습니다:

| 커맨드 | 설명 |
|---------|-------------|
| `/m-brainstorming` | 브레인스토밍 프로세스 시작 |
| `/m-planning` | 구현 계획 작성 |
| `/m-debugging` | 체계적인 디버깅 시작 |
| `/m-ui-ux` | UI/UX 가이드라인 적용 |
| `/m-security` | 보안 코딩 관행 적용 |
| `/m-review` | 코드 변경 사항 검토 |

## 💡 실제 활용 예시

이 스킬을 설치하기 **전**과 **후**의 Claude Code 동작 방식입니다:

![Before and After Example](assets/example-before-after.png)

## 🤝 기여하기

기여를 환영합니다! 풀 리퀘스트 제출, 이슈 보고 또는 새로운 스킬 제안 방법에 대한 자세한 내용은 [기여 가이드](CONTRIBUTING.md)를 참조하십시오.

## 📄 라이선스

이 프로젝트는 MIT 라이선스에 따라 라이선스가 부여됩니다 - 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하십시오.
