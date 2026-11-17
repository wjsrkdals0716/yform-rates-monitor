# Y-FoRM Rates Monitor 공동 작업 저장소

미국 국채시장 대시보드(7개 탭과 공통 캘린더)를 팀원 5명이 함께 만드는 저장소이다. 팀원은 각자 자기 Claude와 독립적으로 이야기하고, 수정할 내용만 요청서로 올린다. 저장소를 지키는 감시 LLM(keeper) 하나가 요청서를 올라온 순서대로 반영하므로, 공동 작업물은 항상 하나의 최신본으로 유지된다.

- 최신본 보기: https://wjsrkdals0716.github.io/yform-rates-monitor/
- 처리 기록: [log/CHANGELOG.md](log/CHANGELOG.md)
- 규칙서: [RULES.md](RULES.md)

## 흐름

```
팀원 m01~m05 ── 각자 Claude와 대화 ──> inbox/ 에 요청서 push
                                            │
                                  keeper가 올라온 순서대로 처리
                                            │
              ┌─────────────────────────────┼──────────────────────────┐
        dashboard/ 수정              outbox/ 에 답장             log/ 에 기록
              │                    (R0007_to_m04.md 등)
     GitHub Pages 최신본 갱신
```

## 팀원이 처음 할 일

1. GitHub 계정을 강민님께 알려 Collaborator 초대를 받고 수락한다.
2. Claude Code에서 [prompts/member_prompt.md](prompts/member_prompt.md)의 첫 문장을 자기 번호로 바꿔 보낸다. 번호는 [team.md](team.md)에 있다.
3. 이후에는 저장소 폴더에서 `claude`를 실행하면 Claude가 새 답장을 먼저 알려 준다.

## 감시 LLM 실행

keeper는 아래 두 방법 중 **한 곳에서만** 실행한다.

**현재 실행 위치: 아직 정하지 않음**

### 방법 A. GitHub Actions

요청서가 push될 때마다 GitHub 서버에서 keeper가 자동으로 실행된다. 아무도 PC를 켜 둘 필요가 없다.

1. 저장소 Settings → Secrets and variables → Actions에 아래 둘 중 하나를 등록한다.
   - `CLAUDE_CODE_OAUTH_TOKEN`: Claude Pro/Max 구독자가 자기 PC에서 `claude setup-token`을 실행해 받은 값. 등록한 사람의 구독 사용량을 쓴다.
   - `ANTHROPIC_API_KEY`: Anthropic Console에서 발급한 API 키. 사용량만큼 과금된다.
2. Actions 탭에서 `keeper`를 한 번 수동 실행(Run workflow)해 동작을 확인한다.

키가 등록되지 않은 동안에는 워크플로가 실행되어도 아무것도 하지 않고 끝난다. 실행이 겹치면 하나씩 차례로 돌며, 각 실행은 아직 처리하지 않은 요청서를 모두 처리한다.

### 방법 B. 한 사람의 PC에서 Claude Code

1. 저장소 폴더에서 `claude`를 실행한다.
2. 다음을 입력한다.

```
/loop 5m prompts/keeper_prompt.md의 지시대로 keeper 역할을 한 번 수행해
```

PC와 터미널이 켜져 있는 동안 5분마다 새 요청서를 확인한다. 이 방법을 쓰는 동안에는 GitHub의 Secret을 등록하지 않는다.

## 폴더 구조

| 경로 | 내용 |
|---|---|
| `inbox/` | 팀원 요청서 |
| `outbox/` | keeper의 답장 |
| `dashboard/` | 공동 작업물(대시보드) |
| `log/CHANGELOG.md` | 처리 기록 |
| `state/processed.txt` | 처리한 요청서 목록 |
| `prompts/` | keeper와 팀원 Claude의 프롬프트 |
| `RULES.md`, `CLAUDE.md`, `team.md` | 규칙서, Claude 역할, 팀원 번호 |
