# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-files/README.md
- 미러 경로: `lib/crewai-files/README.md`

## 한글 요약

Crewai 파일 CrewAI 다중 모드 입력을 위한 파일 처리 유틸리티입니다. 지원되는 파일 형식 ImageFile PNG, JPEG, GIF, WebP PDFFile PDF 문서 TextFile 일반 텍스트 파일 AudioFile MP3, WAV, FLAC, OGG, M4A VideoFile MP4, WebM, MOV, AVI 사용법 제작진에게 파일 전달 작업에 파일 전달

## 핵심 발췌

Crewai 파일 CrewAI 다중 모드 입력을 위한 파일 처리 유틸리티입니다. ## 지원되는 파일 형식 ImageFile PNG, JPEG, GIF, WebP PDFFile PDF 문서 TextFile 일반 텍스트 파일 AudioFile MP3, WAV, F

## 원문 내용

# crewai-files

File handling utilities for CrewAI multimodal inputs.

## Supported File Types

- `ImageFile` - PNG, JPEG, GIF, WebP
- `PDFFile` - PDF documents
- `TextFile` - Plain text files
- `AudioFile` - MP3, WAV, FLAC, OGG, M4A
- `VideoFile` - MP4, WebM, MOV, AVI

## Usage

```python
from crewai_files import File, ImageFile, PDFFile

# Auto-detect file type
file = File(source="document.pdf")  # Resolves to PDFFile

# Or use specific types
image = ImageFile(source="chart.png")
pdf = PDFFile(source="report.pdf")
```

### Passing Files to Crews

```python
crew.kickoff(
    input_files={"chart": ImageFile(source="chart.png")}
)
```

### Passing Files to Tasks

```python
task = Task(
    description="Analyze the chart",
    expected_output="Analysis",
    agent=agent,
    input_files=[ImageFile(source="chart.png")],
)
```