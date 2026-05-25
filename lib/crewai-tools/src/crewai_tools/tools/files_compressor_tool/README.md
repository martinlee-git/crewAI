# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/files_compressor_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/files_compressor_tool/README.md`

## 한글 요약

📦 FileCompressorTool FileCompressorTool은 개별 파일 또는 전체 디렉터리(중첩된 하위 디렉터리 포함)를 .zip 또는 .tar(.tar.gz, .tar.bz2 및 .tar.xz 포함)와 같은 다양한 아카이브 형식으로 압축하는 유틸리티입니다. 이 도구는 로그, 문서, 데이터 세트 또는 백업을 컴팩트 형식으로 보관하는 데 유용하며 아카이브 생성 방법의 유연성을 보장합니다. 설명 이 도구는 파일이나 디렉터리를 입력으로 받아들입니다. 하위 디렉터리의 재귀적 압축을 지원합니다. 사용자 정의 출력 아카이브 경로를 정의하거나 현재 디렉터리를 기본값으로 설정할 수 있습니다. 의도하지 않은 데이터 손실을 방지하기 위해 덮어쓰기 방지를 처리합니다. .zip, .tar, .tar.gz, .tar.bz2 및 .tar.xz 등 다양한 압축 형식을 지원합니다. 인수 | 인수 | 유형 | 필수 | 설명 | | | | | | | 입력 경로 | str | ✅ | 압축하려는 파일 또는 디렉터리의 경로입니다. | | 출력 경로 | str | ❌ | 결과 아카이브 파일의 선택적 경로입니다. 기본값은 ./<이름 .<형식 . | | 덮어쓰기 | 우우

## 핵심 발췌

내가 | ❌ | 기존 아카이브 파일을 덮어쓸지 여부입니다. 기본값은 False입니다. | | 형식 | str | ❌ | 사용할 압축 형식입니다. zip, tar, tar.gz, tar.bz2, tar.xz 중 하나일 수 있습니다. 기본값은 zip입니다. | 사용 예 예 시나리오 단일 파일을 zip 아카이브로 압축: 중첩된 폴더가 있는 디렉터리를 zip 아카이브로 압축: zip 아카이브와 함께 사용자 정의 출력 경로 사용: 기존 zip 파일 덮어쓰기 방지: tar 아카이브로 압축: tar.gz 아카이브로 압축: tar.bz2 아카이브로 압축: tar.xz 아카이브로 압축: 오류 처리 및 유효성 검사 파일 확장자 유효성 검사: 도구는 출력 파일 확장자가 선택한 형식과 일치하는지 확인합니다(예: zip 형식의 경우 .zip, tar 형식의 경우 .tar 등). 파일/디렉토리 존재 : 입력 경로가 존재하지 않으면 오류

## 원문 내용

# 📦 FileCompressorTool

The **FileCompressorTool** is a utility for compressing individual files or entire directories (including nested subdirectories) into different archive formats, such as `.zip` or `.tar` (including `.tar.gz`, `.tar.bz2`, and `.tar.xz`). This tool is useful for archiving logs, documents, datasets, or backups in a compact format, and ensures flexibility in how the archives are created.

---

## Description

This tool:
- Accepts a **file or directory** as input.
- Supports **recursive compression** of subdirectories.
- Lets you define a **custom output archive path** or defaults to the current directory.
- Handles **overwrite protection** to avoid unintentional data loss.
- Supports multiple compression formats: `.zip`, `.tar`, `.tar.gz`, `.tar.bz2`, and `.tar.xz`.

---

## Arguments

| Argument      | Type      | Required | Description                                                                 |
|---------------|-----------|----------|-----------------------------------------------------------------------------|
| `input_path`  | `str`     | ✅       | Path to the file or directory you want to compress.                         |
| `output_path` | `str`     | ❌       | Optional path for the resulting archive file. Defaults to `./<name>.<format>`. |
| `overwrite`   | `bool`    | ❌       | Whether to overwrite an existing archive file. Defaults to `False`.         |
| `format`      | `str`     | ❌       | Compression format to use. Can be one of `zip`, `tar`, `tar.gz`, `tar.bz2`, `tar.xz`. Defaults to `zip`. |

---


## Usage Example

```python
from crewai_tools import FileCompressorTool

# Initialize the tool
tool = FileCompressorTool()

# Compress a directory with subdirectories and files into a zip archive
result = tool._run(
    input_path="./data/project_docs",           # Folder containing subfolders & files
    output_path="./output/project_docs.zip",    # Optional output path (defaults to zip format)
    overwrite=True                              # Allow overwriting if file exists
)
print(result)
# Example output: Successfully compressed './data/project_docs' into './output/project_docs.zip'

```

---

## Example Scenarios

### Compress a single file into a zip archive:
```python
# Compress a single file into a zip archive
result = tool._run(input_path="report.pdf")
# Example output: Successfully compressed 'report.pdf' into './report.zip'
```

### Compress a directory with nested folders into a zip archive:
```python
# Compress a directory containing nested subdirectories and files
result = tool._run(input_path="./my_data", overwrite=True)
# Example output: Successfully compressed 'my_data' into './my_data.zip'
```

### Use a custom output path with a zip archive:
```python
# Compress a directory and specify a custom zip output location
result = tool._run(input_path="./my_data", output_path="./backups/my_data_backup.zip", overwrite=True)
# Example output: Successfully compressed 'my_data' into './backups/my_data_backup.zip'
```

### Prevent overwriting an existing zip file:
```python
# Try to compress a directory without overwriting an existing zip file
result = tool._run(input_path="./my_data", output_path="./backups/my_data_backup.zip", overwrite=False)
# Example output: Output zip './backups/my_data_backup.zip' already exists and overwrite is set to False.
```

### Compress into a tar archive:
```python
# Compress a directory into a tar archive
result = tool._run(input_path="./my_data", format="tar", overwrite=True)
# Example output: Successfully compressed 'my_data' into './my_data.tar'
```

### Compress into a tar.gz archive:
```python
# Compress a directory into a tar.gz archive
result = tool._run(input_path="./my_data", format="tar.gz", overwrite=True)
# Example output: Successfully compressed 'my_data' into './my_data.tar.gz'
```

### Compress into a tar.bz2 archive:
```python
# Compress a directory into a tar.bz2 archive
result = tool._run(input_path="./my_data", format="tar.bz2", overwrite=True)
# Example output: Successfully compressed 'my_data' into './my_data.tar.bz2'
```

### Compress into a tar.xz archive:
```python
# Compress a directory into a tar.xz archive
result = tool._run(input_path="./my_data", format="tar.xz", overwrite=True)
# Example output: Successfully compressed 'my_data' into './my_data.tar.xz'
```

---

## Error Handling and Validations

- **File Extension Validation**: The tool ensures that the output file extension matches the selected format (e.g., `.zip` for `zip` format, `.tar` for `tar` format, etc.).
- **File/Directory Existence**: If the input path does not exist, an error message will be returned.
- **Overwrite Protection**: If a file already exists at the output path, the tool checks the `overwrite` flag before proceeding. If `overwrite=False`, it prevents overwriting the existing file.

---

This tool provides a flexible and robust way to handle file and directory compression across multiple formats for efficient storage and backups.