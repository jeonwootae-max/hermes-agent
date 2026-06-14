# Hermes Agent — 한글 요약

> **Nous Research의 자기 개선 AI 에이전트** — 경험에서 기술을 학습하고, 사용 중 개선하며, 세션 간 지식을 지속하고, 사용자 모델을 심화하는 내장 학습 루프를 가진 유일한 에이전트입니다.

---

## 🎯 핵심 기능

| 기능 | 설명 |
|---------|-------------|
| **실제 터미널 인터페이스** | 전체 TUI: 다중 행 편집, 슬래시 명령어 자동완성, 대화 기록, 중단 및 리디렉션, 스트리밍 도구 출력 |
| **멀티 플랫폼 게이트웨이** | Telegram, Discord, Slack, WhatsApp, Signal, Email — 음성 메모 전사 및 크로스 플랫폼 연속성을 갖춘 단일 게이트웨이 프로세스 |
| **폐쇄형 학습 루프** | 주기적 알림이 있는 에이전트 큐레이션 메모리 • 복잡한 작업 후 자율 기술 생성 • 사용 중 기술 자가 개선 • LLM 요약이 있는 FTS5 세션 검색 • [Honcho](https://github.com/plastic-labs/honcho) 변증법적 사용자 모델링 • [agentskills.io](https://agentskills.io/) 오픈 표준과 호환 |
| **예약 자동화** | 모든 플랫폼으로 전달되는 내장 크론 스케줄러 — 일일 리포트, 야간 백업, 주간 감사를 자연어로 |
| **위임 및 병렬화** | 병렬 워크스트림을 위한 격리된 서브에이전트 생성 • 도구를 RPC로 호출하는 Python 스크립트 작성, 다단계 파이프라인 압축 |
| **어디서나 실행** | 6가지 터미널 백엔드: 로컬, Docker, SSH, Singularity, Modal, Daytona • Daytona/Modal은 서버리스 지속성 제공 (유휴 시 최대 절전, 요청 시 깨움, 근제로 비용) • $5 VPS나 GPU 클러스터에서 실행 가능 |
| **연구 준비** | 배치 궤적 생성, 차세대 도구 호출 모델 학습을 위한 궤적 압축 |

---

## 🔧 모델 유연성

**어떤 모델이든 사용 가능 — 락인 없음.** `hermes model`로 전환:

- [Nous Portal](https://portal.nousresearch.com/) (300+ 모델 + 도구 게이트웨이)
- [OpenRouter](https://openrouter.ai/) (200+ 모델)
- [NovitaAI](https://novita.ai/) (AI 네이티브 클라우드)
- [NVIDIA NIM](https://build.nvidia.com/) (Nemotron)
- [Xiaomi MiMo](https://platform.xiaomimimo.com/)
- [z.ai/GLM](https://z.ai/)
- [Kimi/Moonshot](https://platform.moonshot.ai/)
- [MiniMax](https://www.minimax.io/)
- [Hugging Face](https://huggingface.co/)
- OpenAI, Anthropic, 또는 **자체 엔드포인트**

---

## ⚡ 빠른 설치

### Linux, macOS, WSL2, Termux
```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
```

### Windows (네이티브 PowerShell)
```powershell
iex (irm https://hermes-agent.nousresearch.com/install.ps1)
```
> **네이티브 Windows** — WSL 불필요. uv, Python 3.11, Node.js, ripgrep, ffmpeg, **포터블 Git Bash (MinGit)**를 `%LOCALAPPDATA%\hermes\git`에 설치 (관리자 권한 불필요, 격리됨). 기존 Git 감지 시 활용.

### Android / Termux
[Termux 가이드](https://hermes-agent.nousresearch.com/docs/getting-started/termux) 참조 — Android 호환 `.[termux]` extra 설치 (전체 `.[all]`은 Android 비호환 음성 의존성 포함).

### 설치 후
```bash
source ~/.bashrc    # 또는 ~/.zshrc
hermes              # 채팅 시작!
```

---

## 🚀 시작 명령어

| 명령어 | 용도 |
|---------|------|
| `hermes` | 대화형 CLI — 대화 시작 |
| `hermes model` | LLM 제공자 및 모델 선택 |
| `hermes tools` | 활성화할 도구 구성 |
| `hermes config set` | 개별 설정 값 지정 |
| `hermes gateway` | 메시징 게이트웨이 시작 (Telegram, Discord 등) |
| `hermes setup` | 전체 설정 마법사 (모든 것 구성) |
| `hermes claw migrate` | OpenClaw에서 마이그레이션 |
| `hermes update` | 최신 버전으로 업데이트 |
| `hermes doctor` | 문제 진단 |

📖 **[전체 문서 →](https://hermes-agent.nousresearch.com/docs/)**

---

## 🌐 Nous Portal — API 키 수집 건너뛰기

한 구독으로 **모델 + 웹 검색 + 이미지 생성 + TTS + 클라우드 브라우저** 커버:

```bash
hermes setup --portal
```
- OAuth 로그인, Nous를 제공자로 설정, 도구 게이트웨이 활성화
- 상태 확인: `hermes portal info`
- **여전히 도구별로 자체 키 사용 가능** — 게이트웨이는 백엔드별, 올-오어-낫 없음

---

## 💬 CLI vs 메시징 빠른 참조

| 작업 | CLI | 메시징 (Telegram, Discord, Slack, WhatsApp, Signal, Email) |
|--------|-----|---------------------------------------------------------------|
| 채팅 시작 | `hermes` | `hermes gateway setup` + `hermes gateway start`, 봇에 메시지 |
| 새 대화 | `/new` 또는 `/reset` | `/new` 또는 `/reset` |
| 모델 변경 | `/model [provider:model]` | `/model [provider:model]` |
| 페르소나 설정 | `/personality [name]` | `/personality [name]` |
| 마지막 턴 재시도/실행 취소 | `/retry`, `/undo` | `/retry`, `/undo` |
| 컨텍스트 압축 / 사용량 | `/compress`, `/usage`, `/insights [--days N]` | `/compress`, `/usage`, `/insights [days]` |
| 기술 찾아보기 | `/skills` 또는 `/<skill-name>` | `/<skill-name>` |
| 작업 중단 | `Ctrl+C` 또는 새 메시지 | `/stop` 또는 새 메시지 |
| 플랫폼 상태 | `/platforms` | `/status`, `/sethome` |

📖 [CLI 가이드](https://hermes-agent.nousresearch.com/docs/user-guide/cli) | [게이트웨이 가이드](https://hermes-agent.nousresearch.com/docs/user-guide/gateway)

---

## 🧠 학습 루프 작동 방식

```
┌─────────────────────────────────────────────────────────────┐
│  1. 작업 수행                                               │
│     ↓                                                       │
│  2. 에피소드 저장 (FTS5 + 벡터)                              │
│     ↓                                                       │
│  3. 복잡한 작업 후 → 기술 자동 생성                          │
│     ↓                                                       │
│  4. 기술 사용 시 → 경계 사례에서 학습 → 자체 패치            │
│     ↓                                                       │
│  5. 주기적 메모리 큐레이션 → 사용자 모델 업데이트 (Honcho)   │
└─────────────────────────────────────────────────────────────┘
```

- **메모리**: 에피소드(대화) + 시맨틱(기술/사실) + 절차적(워크플로우)
- **기술**: 마크다운 + 프론트매터, 버전 관리, `agentskills.io` 표준 준수
- **사용자 모델**: Honcho의 변증법적 추론으로 선호도/패턴/제약 학습

---

## 🛠 기술 생태계

| 카테고리 | 예시 |
|-----------|-------|
| **AI/ML** | `llama-cpp`, `vllm`, `dspy`, `evaluating-llms-harness`, `huggingface-hub` |
| **개발** | `github-*`, `plan`, `systematic-debugging`, `test-driven-development`, `subagent-driven-development` |
| **리서치** | `arxiv`, `polymarket`, `blogwatcher`, `llm-wiki` |
| **창작** | `excalidraw`, `manim-video`, `p5js`, `baoyu-*`, `design-md` |
| **생산성** | `notion`, `obsidian`, `linear`, `google-workspace`, `airtable` |
| **데브옵스** | `kanban-orchestrator`, `kanban-worker`, `webhook-subscriptions` |
| **모바일/애플** | `imessage`, `apple-notes`, `apple-reminders`, `findmy`, `macos-computer-use` |

📦 **[전체 기술 목록 →](https://hermes-agent.nousresearch.com/docs/skills/)**

---

## 🏗 아키텍처 하이라이트

- **게이트웨이**: 단일 Rust 프로세스, 모든 플랫폼 관리, 음성 메모를 위해 Whisper.cpp 내장
- **에이전트 코어**: Python, 비동기 우선, 플러그인 도구 시스템, 기술 로더
- **터미널 백엔드**: 로컬 PTY, SSH, Docker, Singularity, Modal, Daytona (각각 별도 프로세스 격리)
- **세션 DB**: SQLite + FTS5, 전체 텍스트 검색, LLM 요약 북엔드
- **기술 저장소**: `~/.hermes/skills/` (사용자) + 내장 (시스템), Git 호환

---

## 📄 라이선스

**Apache-2.0** — 상용 사용, 수정, 배포 자유.

---

## 🔗 링크

- **문서**: https://hermes-agent.nousresearch.com/docs/
- **Nous Portal**: https://portal.nousresearch.com/
- **Discord 커뮤니티**: https://discord.gg/nousresearch
- **GitHub**: https://github.com/nous-research/hermes-agent
- **기술 표준**: https://agentskills.io/

---

> **Nous Research가 ❤️로 만들었습니다** — 인간 가치와 일치하는 AI 시스템 구축.