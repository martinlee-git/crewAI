# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/directory_read_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/directory_read_tool/README.md`

## 한글 요약

shell pip install 'crewai[tools]' python from 크루ai tools import DirectoryReadTool 탐색하려는 디렉토리로 도구 초기화 tool = DirectoryReadTool(directory='/path/to/your/directory') 도구를 사용하여 지정된 디렉토리의 내용 나열하기 디렉토리 내용 = tool.run() print(디렉터리 내용) DirectoryReadTool에 대한 이 개정된 문서는 명확성, 일관성 및 고품질 표준 준수를 위해 조정된 구조 및 내용 요구 사항을 개략적으로 유지합니다. 제공된 문서 예시에 예시되어 있습니다.

## 핵심 발췌

``markdown # DirectoryReadTool ## 설명 DirectoryReadTool은 디렉토리 내용의 포괄적인 목록을 위해 설계된 매우 효율적인 유틸리티입니다. 지정된 디렉터리를 재귀적으로 탐색합니다.

## 원문 내용

```markdown
# DirectoryReadTool

## Description
The DirectoryReadTool is a highly efficient utility designed for the comprehensive listing of directory contents. It recursively navigates through the specified directory, providing users with a detailed enumeration of all files, including those nested within subdirectories. This tool is indispensable for tasks requiring a thorough inventory of directory structures or for validating the organization of files within directories.

## Installation
Install the `crewai_tools` package to use the DirectoryReadTool in your project. If you haven't added this package to your environment, you can easily install it with pip using the following command:

```shell
pip install 'crewai[tools]'
```

This installs the latest version of the `crewai_tools` package, allowing access to the DirectoryReadTool and other utilities.

## Example
The DirectoryReadTool is simple to use. The code snippet below shows how to set up and use the tool to list the contents of a specified directory:

```python
from crewai_tools import DirectoryReadTool

# Initialize the tool with the directory you want to explore
tool = DirectoryReadTool(directory='/path/to/your/directory')

# Use the tool to list the contents of the specified directory
directory_contents = tool.run()
print(directory_contents)
```

This example demonstrates the essential steps to utilize the DirectoryReadTool effectively, highlighting its simplicity and user-friendly design.

## Arguments
The DirectoryReadTool requires minimal configuration for use. The essential argument for this tool is as follows:

- `directory`: A mandatory argument that specifies the path to the directory whose contents you wish to list. It accepts both absolute and relative paths, guiding the tool to the desired directory for content listing.

The DirectoryReadTool provides a user-friendly and efficient way to list directory contents, making it an invaluable tool for managing and inspecting directory structures.
```

This revised documentation for the DirectoryReadTool maintains the structure and content requirements as outlined, with adjustments made for clarity, consistency, and adherence to the high-quality standards exemplified in the provided documentation example.