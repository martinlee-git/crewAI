# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/file_read_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/file_read_tool/README.md`

## 한글 요약

FileReadTool 설명 FileReadTool은 파일에서 콘텐츠를 읽고 검색하는 프로세스를 간소화하도록 설계된 크루아이 도구 패키지의 다목적 구성 요소입니다. 이는 배치 텍스트 파일 처리, 런타임 구성 파일 읽기 및 분석을 위한 데이터 가져오기와 같은 시나리오에서 특히 유용합니다. 이 도구는 .txt, .csv, .json을 포함한 다양한 텍스트 기반 파일 형식을 지원하고 파일 유형에 따라 기능을 조정합니다(예: 쉽게 사용할 수 있도록 JSON 콘텐츠를 Python 사전으로 변환). 또한 이 도구는 시작 줄과 읽을 줄 수를 지정하여 파일의 특정 청크 읽기를 지원합니다. 이는 메모리에 완전히 로드할 필요가 없는 대용량 파일을 작업할 때 유용합니다. 설치 프로젝트에서 FileReadTool을 사용하려면 크루아이 도구 패키지를 설치하십시오. 예 FileReadTool을 시작하려면: 인수 파일 경로: 읽으려는 파일의 경로입니다. 절대 경로와 상대 경로를 모두 허용합니다. 보장

## 핵심 발췌

e 파일이 존재하며 해당 파일에 액세스하는 데 필요한 권한이 있습니다. start line: (선택 사항) 읽기를 시작할 줄 번호입니다(인덱스 1개). 기본값은 1(첫 번째 줄)입니다. line count: (선택 사항) 읽을 줄 수입니다. 제공되지 않으면 파일의 시작 줄부터 끝까지 읽습니다.

## 원문 내용

# FileReadTool

## Description

The FileReadTool is a versatile component of the crewai_tools package, designed to streamline the process of reading and retrieving content from files. It is particularly useful in scenarios such as batch text file processing, runtime configuration file reading, and data importation for analytics. This tool supports various text-based file formats including `.txt`, `.csv`, `.json`, and adapts its functionality based on the file type, for instance, converting JSON content into a Python dictionary for easy use.

The tool also supports reading specific chunks of a file by specifying a starting line and the number of lines to read, which is helpful when working with large files that don't need to be loaded entirely into memory.

## Installation

Install the crewai_tools package to use the FileReadTool in your projects:

```shell
pip install 'crewai[tools]'
```

## Example

To get started with the FileReadTool:

```python
from crewai_tools import FileReadTool

# Initialize the tool to read any files the agents knows or lean the path for
file_read_tool = FileReadTool()

# OR

# Initialize the tool with a specific file path, so the agent can only read the content of the specified file
file_read_tool = FileReadTool(file_path='path/to/your/file.txt')

# Read a specific chunk of the file (lines 100-149)
partial_content = file_read_tool.run(file_path='path/to/your/file.txt', start_line=100, line_count=50)
```

## Arguments

- `file_path`: The path to the file you want to read. It accepts both absolute and relative paths. Ensure the file exists and you have the necessary permissions to access it.
- `start_line`: (Optional) The line number to start reading from (1-indexed). Defaults to 1 (the first line).
- `line_count`: (Optional) The number of lines to read. If not provided, reads from the start_line to the end of the file.