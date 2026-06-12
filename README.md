# SS — 개인 AI 비서 템플릿

[Claude Code](https://claude.com/claude-code) 위에 만든 개인 "Chief of Staff" 에이전트 템플릿입니다.
[marvin-template](https://github.com/SterlingChin/marvin-template)에서 영감을 받았습니다.
세션을 넘어 맥락을 기억하고, 목표와 할 일을 추적하고, 며칠 만에 돌아와도 브리핑해 줍니다.

여기엔 코드가 없습니다. 에이전트 전체가 룰셋(`CLAUDE.md` + 슬래시 커맨드)과,
기억으로 쌓이는 마크다운 파일들로 이루어져 있어요.

## 시작하기

1. 이 저장소를 클론합니다 (이름은 마음대로):
   ```
   git clone https://github.com/choslion/agent-ss-template.git my-assistant
   cd my-assistant
   ```
2. Claude Code로 엽니다 — 폴더에서 `claude` 실행 (Windows라면 `SS.bat` 더블클릭).
3. 인사하세요. SS가 온보딩(이름, 목표, 선호 스타일)을 진행합니다.
4. 이후엔 세션을 `/start`로 열고 `/end`로 닫으면 됩니다. 습관은 이게 전부예요.

> **본인 사본은 비공개로 유지하세요.** 목표, 할 일, 세션 로그가 이 폴더에
> 평문 마크다운으로 저장됩니다. GitHub에 올린다면 비공개 저장소를 쓰세요 —
> 그러면 덤으로 비서의 기억이 여러 컴퓨터에서 동기화됩니다.

## SS.bat (Windows) / SS.command (Mac)

더블클릭 한 번으로 SS를 여는 실행 파일입니다 — Windows는 `SS.bat`,
Mac은 `SS.command`. 이 폴더로 이동한 뒤
`claude --model sonnet`을 실행해요. 기본 모델을 바꾸려면 파일 안의
`--model` 플래그를 수정하고, 세션 중에는 `/model` 커맨드로 바꿀 수 있습니다.
사전 준비물: [Claude Code 설치](https://claude.com/claude-code)
(`npm install -g @anthropic-ai/claude-code`) 후 로그인.

## 커맨드

| 커맨드 | 설명 |
|--------|------|
| `/start` | 지난 세션 이어받기 + 오늘 브리핑 (git 저장소면 `git pull`로 동기화) |
| `/update` | 세션 중간 저장 |
| `/status` | 목표·할일·결정 현황 요약 |
| `/end` | 세션 로그 저장 + 상태 갱신 (git 저장소면 `git push`로 백업) |
| `/help` | 사용법 안내 |

## 작동 원리

```
.
├── CLAUDE.md              # SS의 정체성·원칙·세션 규칙 (매 세션 자동 로드)
├── .claude/commands/      # 슬래시 커맨드 정의 (마크다운)
├── profile/me.md          # 내가 누구인지, 어떤 대화 스타일을 원하는지
├── state/
│   ├── current.md         # 세션 간 인수인계 문서
│   ├── goals.md           # 장기 목표 + 진행률
│   ├── todos.md           # 할 일 목록
│   └── decisions.md       # 결정 기록 (이유 포함)
└── sessions/              # 날짜별 세션 로그 (YYYY-MM-DD.md)
```

Claude Code는 매 세션 시작 시 `CLAUDE.md`를 자동으로 읽습니다. 거기에
"state/와 최근 세션 로그를 읽고 이어가라"는 지시가 있어서 대화가 끊기지 않아요.
`/end`가 세션을 디스크에 기록합니다. 기억은 전부 그냥 파일이라 직접 읽고,
고치고, 지우고, 백업할 수 있습니다.

## 확장하기

- **새 커맨드**: `.claude/commands/`에 마크다운 파일 추가 (또는 SS에게 만들어 달라고 하기)
- **외부 연동**: Google Calendar, Notion, Slack 등 MCP 서버 연결 (`claude mcp add`)
- **스타일 변경**: `profile/me.md` 수정
- **모델 변경**: `SS.bat`의 `--model` 플래그 수정, 또는 세션 중 `/model`

## 라이선스

MIT — 자유롭게 쓰고, 포크하고, 이름을 바꾸세요.
