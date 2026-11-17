# 팀원 Claude 시작 프롬프트

Claude Code를 쓰는 팀원은 저장소 폴더에서 `claude`를 실행하기만 하면 된다. 저장소의 `CLAUDE.md`가 자동으로 읽혀 역할이 정해지므로 따로 붙여 넣을 것이 없다.

처음 한 번은 아래 문장의 번호와 이름을 자기 것으로 바꿔 Claude에게 보낸다.

```
나는 Rates Monitor 팀의 m04 전강민이야. https://github.com/wjsrkdals0716/yform-rates-monitor 저장소를 이 폴더에 clone하고(이미 있으면 git pull), 저장소의 CLAUDE.md와 RULES.md를 읽은 뒤 그 규칙대로 내 Claude 역할을 해 줘. 내 번호는 .member 파일에 저장해 줘.
```

Claude Code가 아닌 곳(claude.ai 대화 등)에서는 저장소에 직접 push할 수 없다. 그때는 위 문장 대신 아래를 보내고, Claude가 만들어 준 요청서 파일을 GitHub 웹에서 `inbox/` 폴더에 직접 올린다(Add file → Create new file).

```
나는 Rates Monitor 팀의 m04 전강민이야. https://github.com/wjsrkdals0716/yform-rates-monitor 의 RULES.md 3장 양식으로 요청서를 같이 써 줘. 대시보드 파일은 고치지 말고 요청서 초안과 파일 이름만 만들어 줘.
```
