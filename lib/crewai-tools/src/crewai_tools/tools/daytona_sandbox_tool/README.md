# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/daytona_sandbox_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/daytona_sandbox_tool/README.md`

## 한글 요약

Daytona Sandbox 도구 쉘 명령을 실행하고, Python을 실행하고, Daytona 샌드박스 내에서 파일을 관리하세요. Daytona는 에이전트 기반 코드 실행에 적합한 격리된 임시 컴퓨팅 환경을 제공합니다. 에이전트에 실제로 필요한 것을 선택할 수 있도록 세 가지 도구가 제공됩니다. DaytonaExecTool — 셸 명령(sandbox.process.exec)을 실행합니다. DaytonaPythonTool — Python 스크립트를 실행합니다(sandbox.process.code 실행). DaytonaFileTool — 파일 읽기/쓰기/목록/삭제(sandbox.fs.). 설치 API 키 설정: DAYTONA API URL 및 DAYTONA TARGET도 설정된 경우 적용됩니다. 샌드박스 수명 주기 세 가지 도구 모두 DaytonaBaseTool의 동일한 수명 주기 제어를 공유합니다. | 모드 | 샌드박스가 생성되면 | 삭제된 경우 | | | | | | 임시(기본값, 지속적=False) | 모든 실행 호출 시 | 같은 통화가 끝나면 | | 지속성(지속적=True) | 처음 사용할 때 느리게 | 프로세스 종료 시(atexit를 통해) 또는 수동으로 tool.close() | | 첨부(샌드박스 ID="…") | 안 함 - 도구가 기존에 연결됩니다.

## 핵심 발췌

샌드박스 | 안 함 - 도구가 생성하지 않은 샌드박스를 삭제하지 않습니다 | 임시 모드는 안전한 기본값입니다. 에이전트가 정리하는 것을 잊어버리면 아무것도 누출되지 않습니다. 파일 시스템 상태 또는 설치된 패키지를 여러 단계에 걸쳐 전달하려는 경우 영구 모드를 사용하십시오. 이는 DaytonaFileTool과 DaytonaExecTool을 페어링할 때 일반적입니다. 예 단발 Python 실행(일시적) 다단계 셸 세션(지속) 기존 샌드박스에 연결 사용자 정의 생성 매개변수 생성 생성 매개변수를 통해 Daytona의 CreateSandboxFromSnapshotParams kwargs 전달: 도구 인수 DaytonaExecTool 명령: str — 실행할 쉘 명령. cwd: str | 없음 — 작업 디렉터리. 환경: dict[str, str] | 없음 — 이 명령에 대한 추가 환경 변수입니다. 시간 초과: 정수 | 없음 – 초. DaytonaPythonTool 코드: str — 실행할 Python 소스입니다. argv: 목록[str]

## 원문 내용

# Daytona Sandbox Tools

Run shell commands, execute Python, and manage files inside a [Daytona](https://www.daytona.io/) sandbox. Daytona provides isolated, ephemeral compute environments suitable for agent-driven code execution.

Three tools are provided so you can pick what the agent actually needs:

- **`DaytonaExecTool`** — run a shell command (`sandbox.process.exec`).
- **`DaytonaPythonTool`** — run a Python script (`sandbox.process.code_run`).
- **`DaytonaFileTool`** — read / write / list / delete files (`sandbox.fs.*`).

## Installation

```shell
uv add "crewai-tools[daytona]"
# or
pip install "crewai-tools[daytona]"
```

Set the API key:

```shell
export DAYTONA_API_KEY="..."
```

`DAYTONA_API_URL` and `DAYTONA_TARGET` are also respected if set.

## Sandbox lifecycle

All three tools share the same lifecycle controls from `DaytonaBaseTool`:

| Mode | When the sandbox is created | When it is deleted |
| --- | --- | --- |
| **Ephemeral** (default, `persistent=False`) | On every `_run` call | At the end of that same call |
| **Persistent** (`persistent=True`) | Lazily on first use | At process exit (via `atexit`), or manually via `tool.close()` |
| **Attach** (`sandbox_id="…"`) | Never — the tool attaches to an existing sandbox | Never — the tool will not delete a sandbox it did not create |

Ephemeral mode is the safe default: nothing leaks if the agent forgets to clean up. Use persistent mode when you want filesystem state or installed packages to carry across steps — this is typical when pairing `DaytonaFileTool` with `DaytonaExecTool`.

## Examples

### One-shot Python execution (ephemeral)

```python
from crewai_tools import DaytonaPythonTool

tool = DaytonaPythonTool()
result = tool.run(code="print(sum(range(10)))")
```

### Multi-step shell session (persistent)

```python
from crewai_tools import DaytonaExecTool, DaytonaFileTool

exec_tool = DaytonaExecTool(persistent=True)
file_tool = DaytonaFileTool(persistent=True)

# Agent writes a script, then runs it — but each tool keeps its OWN persistent
# sandbox. To share the *same* sandbox across two tools, create and use the
# first tool, then read its `active_sandbox_id` and pass it to the second:
#   exec_tool.run(command="pip install httpx")
#   file_tool = DaytonaFileTool(sandbox_id=exec_tool.active_sandbox_id)
```

### Attach to an existing sandbox

```python
from crewai_tools import DaytonaExecTool

tool = DaytonaExecTool(sandbox_id="my-long-lived-sandbox")
```

### Custom create params

Pass Daytona's `CreateSandboxFromSnapshotParams` kwargs via `create_params`:

```python
tool = DaytonaExecTool(
    persistent=True,
    create_params={
        "language": "python",
        "env_vars": {"MY_FLAG": "1"},
        "labels": {"owner": "crewai-agent"},
    },
)
```

## Tool arguments

### `DaytonaExecTool`
- `command: str` — shell command to run.
- `cwd: str | None` — working directory.
- `env: dict[str, str] | None` — extra env vars for this command.
- `timeout: int | None` — seconds.

### `DaytonaPythonTool`
- `code: str` — Python source to execute.
- `argv: list[str] | None` — argv forwarded via `CodeRunParams`.
- `env: dict[str, str] | None` — env vars forwarded via `CodeRunParams`.
- `timeout: int | None` — seconds.

### `DaytonaFileTool`
- `action`: one of `read`, `write`, `append`, `list`, `delete`, `mkdir`, `info`, `exists`, `move`, `find`, `search`, `chmod`, `replace`.
- `path: str | None` — absolute path inside the sandbox. Required for all actions except `replace`.
- `content: str | None` — required for `append`; optional for `write`.
- `binary: bool` — if `True`, `content` is base64 on write / returned as base64 on read.
- `recursive: bool` — for `delete`, removes directories recursively.
- `mode: str | None` — for `mkdir` (defaults to `"0755"`) or for `chmod` (e.g. `"755"`).
- `destination: str | None` — required for `move`.
- `pattern: str | None` — required for `find` (content grep), `search` (filename glob), and `replace`.
- `replacement: str | None` — required for `replace`.
- `paths: list[str] | None` — required for `replace`; list of files to operate on.
- `owner: str | None` / `group: str | None` — for `chmod`. Pass at least one of `mode`, `owner`, or `group`.