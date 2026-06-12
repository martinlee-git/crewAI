# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/e2b_sandbox_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/e2b_sandbox_tool/README.md`

## 한글 요약

E2B 샌드박스 도구 셸 명령을 실행하고, Python을 실행하고, E2B 샌드박스 내에서 파일을 관리합니다. E2B는 풍부한 Python 결과를 위한 Jupyter 스타일 코드 인터프리터와 함께 에이전트 기반 코드 실행에 적합한 격리된 임시 VM을 제공합니다. 에이전트에 실제로 필요한 것을 선택할 수 있도록 세 가지 도구가 제공됩니다. E2BExecTool — 셸 명령(sandbox.commands.run)을 실행합니다. E2BPythonTool — E2B 코드 인터프리터(sandbox.run 코드)에서 Python 셀을 실행하여 stdout/stderr 및 리치 결과(차트, 데이터 프레임)를 반환합니다. E2BFileTool — 파일 읽기/쓰기/목록/삭제(sandbox.files.). 설치 API 키 설정: 설정된 경우 E2B DOMAIN도 존중됩니다(자체 호스팅 또는 기본이 아닌 배포의 경우). 샌드박스 수명 주기 세 가지 도구 모두 E2BBaseTool의 동일한 수명 주기 제어를 공유합니다. | 모드 | 샌드박스가 생성되면 | 살해될 때 | | | | | | 임시(기본값, 지속적=False) | 모든 실행 호출 시 | 같은 통화가 끝나면 | | 지속적(지속적=True) | 처음 사용할 때 느리게 | 진행 중

## 핵심 발췌

ss 종료(atexit를 통해) 또는 tool.close()를 통해 수동으로 | | 첨부(샌드박스 ID="…") | 없음 - 도구가 기존 샌드박스에 연결됩니다 | 안 함 - 도구가 생성하지 않은 샌드박스를 종료하지 않습니다 | 임시 모드는 안전한 기본값입니다. 에이전트가 정리하는 것을 잊어버리면 아무것도 누출되지 않습니다. 파일 시스템 상태 또는 설치된 패키지를 여러 단계에 걸쳐 전달하려는 경우 영구 모드를 사용하십시오. 이는 E2BFileTool과 E2BExecTool을 페어링할 때 일반적입니다. E2B 샌드박스는 유휴 시간 초과 후에도 자동으로 만료됩니다. 샌드박스 시간 제한(초, 기본값 300)을 통해 조정합니다. 예 일회성 Python 실행(일시적) 다단계 셸 세션(영구) 기존 샌드박스에 연결 사용자 정의 매개변수 생성 도구 인수 E2BExecTool 명령: str — 실행할 셸 명령입니다. cwd: str | 없음 — 작업 디렉터리. envs: dict[str, str] | N

## 원문 내용

# E2B Sandbox Tools

Run shell commands, execute Python, and manage files inside an [E2B](https://e2b.dev/) sandbox. E2B provides isolated, ephemeral VMs suitable for agent-driven code execution, with a Jupyter-style code interpreter for rich Python results.

Three tools are provided so you can pick what the agent actually needs:

- **`E2BExecTool`** — run a shell command (`sandbox.commands.run`).
- **`E2BPythonTool`** — run a Python cell in the E2B code interpreter (`sandbox.run_code`), returning stdout/stderr and rich results (charts, dataframes).
- **`E2BFileTool`** — read / write / list / delete files (`sandbox.files.*`).

## Installation

```shell
uv add "crewai-tools[e2b]"
# or
pip install "crewai-tools[e2b]"
```

Set the API key:

```shell
export E2B_API_KEY="..."
```

`E2B_DOMAIN` is also respected if set (for self-hosted or non-default deployments).

## Sandbox lifecycle

All three tools share the same lifecycle controls from `E2BBaseTool`:

| Mode | When the sandbox is created | When it is killed |
| --- | --- | --- |
| **Ephemeral** (default, `persistent=False`) | On every `_run` call | At the end of that same call |
| **Persistent** (`persistent=True`) | Lazily on first use | At process exit (via `atexit`), or manually via `tool.close()` |
| **Attach** (`sandbox_id="…"`) | Never — the tool attaches to an existing sandbox | Never — the tool will not kill a sandbox it did not create |

Ephemeral mode is the safe default: nothing leaks if the agent forgets to clean up. Use persistent mode when you want filesystem state or installed packages to carry across steps — this is typical when pairing `E2BFileTool` with `E2BExecTool`.

E2B sandboxes also auto-expire after an idle timeout. Tune it via `sandbox_timeout` (seconds, default `300`).

## Examples

### One-shot Python execution (ephemeral)

```python
from crewai_tools import E2BPythonTool

tool = E2BPythonTool()
result = tool.run(code="print(sum(range(10)))")
```

### Multi-step shell session (persistent)

```python
from crewai_tools import E2BExecTool, E2BFileTool

exec_tool = E2BExecTool(persistent=True)
file_tool = E2BFileTool(persistent=True)

# Each tool keeps its own persistent sandbox. If you need the *same* sandbox
# across two tools, create one tool, grab the sandbox id via
# `tool._persistent_sandbox.sandbox_id`, and pass it to the other via
# `sandbox_id=...`.
```

### Attach to an existing sandbox

```python
from crewai_tools import E2BExecTool

tool = E2BExecTool(sandbox_id="sbx_...")
```

### Custom create params

```python
tool = E2BExecTool(
    persistent=True,
    template="my-custom-template",
    sandbox_timeout=600,
    envs={"MY_FLAG": "1"},
    metadata={"owner": "crewai-agent"},
)
```

## Tool arguments

### `E2BExecTool`
- `command: str` — shell command to run.
- `cwd: str | None` — working directory.
- `envs: dict[str, str] | None` — extra env vars for this command.
- `timeout: float | None` — seconds.

### `E2BPythonTool`
- `code: str` — source to execute.
- `language: str | None` — override kernel language (default: Python).
- `envs: dict[str, str] | None` — env vars for the run.
- `timeout: float | None` — seconds.

### `E2BFileTool`
- `action: "read" | "write" | "append" | "list" | "delete" | "mkdir" | "info" | "exists"`
- `path: str` — absolute path inside the sandbox.
- `content: str | None` — required for `append`; optional for `write`.
- `binary: bool` — if `True`, `content` is base64 on write / returned as base64 on read.
- `depth: int` — for `list`, how many levels to recurse (default 1).

## Security considerations

These tools hand the LLM arbitrary shell, Python, and filesystem access inside a remote VM. The threat model to keep in mind:

- **Prompt-injection is a code-execution vector.** If the agent ingests untrusted content (web pages, scraped documents, user-supplied files, emails, search results), a malicious instruction hidden in that content can coerce the agent into issuing commands to `E2BExecTool` / `E2BPythonTool`. Treat any pipeline that feeds untrusted text into an agent that also has these tools as equivalent to remote code execution — the LLM is the attacker's shell.
- **Ephemeral mode (the default) is the main blast-radius control.** A fresh sandbox is created per call and killed at the end, so injected commands cannot persist state, exfiltrate long-lived secrets, or build up tooling across turns. Leave `persistent=False` unless you have a concrete reason to change it.
- **Avoid this specific combination:**
  - untrusted content in the agent's context, **plus**
  - `persistent=True` or an explicit long-lived `sandbox_id`, **plus**
  - a large `sandbox_timeout` or credentials/secrets seeded into the sandbox via `envs`.

  That stack lets a single injection pivot into a long-running, credentialed shell that survives across turns. If you must run persistently, also keep `sandbox_timeout` short, scope `envs` to the minimum the task needs, and don't feed the same agent untrusted input.
- **Don't mount production credentials.** Anything you put into `envs`, `metadata`, or files written to the sandbox is reachable from the LLM. Use per-task scoped keys, not your personal API tokens.
- **E2B's VM isolation is the final backstop**, not a license to relax the above — isolation prevents escape to the host, but everything the sandbox can reach (the public internet, any service whose token you dropped in) is still fair game for an injected command.