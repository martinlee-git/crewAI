# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/contextualai_parse_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/contextualai_parse_tool/README.md`

## 한글 요약

ContextualAIParseTool 설명 이 도구는 Contextual AI의 엔터프라이즈급 문서 구문 분석 기능을 CrewAI와 통합하여 복잡한 레이아웃, 표 및 그림에 대한 고급 AI 기반 문서 이해를 활용할 수 있도록 설계되었습니다. 이 도구를 사용하면 Contextual AI의 강력한 문서 파서를 사용하여 문서에서 구조화된 콘텐츠를 추출할 수 있습니다. 설치 이 도구를 프로젝트에 통합하려면 아래 설치 지침을 따르십시오. 참고: Contextual AI API 키가 필요합니다. app.contextual.ai에 가입하여 무료 API 키를 받으세요. 예 결과에는 문서의 구문 분석된 내용이 표시됩니다. 예: 매개변수 api 키: Contextual AI API 키 파일 경로: 구문 분석할 문서 경로 구문 분석 모드: 구문 ​​분석 모드(기본값: "표준") 그림 캡션 모드: 그림 캡션 처리(기본값: "concise") 문서 계층 활성화: 계층 구조 감지 활성화(기본값: True) 페이지 범위: 구문 분석할 페이지(예: "0 5", 모두 없음) 출력 유형: 출력 형식(d)

## 핵심 발췌

efault: ["markdown per page"]) 주요 기능 고급 문서 이해: 복잡한 PDF 레이아웃, 표 및 다중 열 문서 처리 그림 및 표 추출: 그림, 차트 및 표 형식 데이터의 지능적 추출 페이지 범위 선택: 특정 페이지 또는 전체 문서 구문 분석 사용 사례 복잡한 PDF 및 연구 논문에서 구조화된 콘텐츠 추출 재무 보고서, 법률 문서 및 기술 매뉴얼 구문 분석 RAG 파이프라인에서 추가 처리를 위해 문서를 마크다운으로 변환 Contextual AI의 기능에 대한 자세한 내용은 공식 웹사이트를 방문하세요. 문서.

## 원문 내용

# ContextualAIParseTool

## Description
This tool is designed to integrate Contextual AI's enterprise-grade document parsing capabilities with CrewAI, enabling you to leverage advanced AI-powered document understanding for complex layouts, tables, and figures. Use this tool to extract structured content from your documents using Contextual AI's powerful document parser.

## Installation
To incorporate this tool into your project, follow the installation instructions below:

```
pip install 'crewai[tools]' contextual-client
```

**Note**: You'll need a Contextual AI API key. Sign up at [app.contextual.ai](https://app.contextual.ai) to get your free API key.

## Example

```python
from crewai_tools import ContextualAIParseTool

tool = ContextualAIParseTool(api_key="your_api_key_here")

result = tool._run(
    file_path="/path/to/document.pdf",
    parse_mode="standard",
    page_range="0-5",
    output_types=["markdown-per-page"]
)
print(result)
```

The result will show the parsed contents of your document. For example: 
```
{
  "file_name": "attention_is_all_you_need.pdf",
  "status": "completed",
  "pages": [
    {
      "index": 0,
      "markdown": "Provided proper attribution ...
    },
    {
      "index": 1,
      "markdown": "## 1 Introduction ...
    },
    ...
  ] 
}
```
## Parameters
- `api_key`: Your Contextual AI API key
- `file_path`: Path to document to parse
- `parse_mode`: Parsing mode (default: "standard")
- `figure_caption_mode`: Figure caption handling (default: "concise")
- `enable_document_hierarchy`: Enable hierarchy detection (default: True)
- `page_range`: Pages to parse (e.g., "0-5", None for all)
- `output_types`: Output formats (default: ["markdown-per-page"])

## Key Features
- **Advanced Document Understanding**: Handles complex PDF layouts, tables, and multi-column documents
- **Figure and Table Extraction**: Intelligent extraction of figures, charts, and tabular data
- **Page Range Selection**: Parse specific pages or entire documents

## Use Cases
- Extract structured content from complex PDFs and research papers
- Parse financial reports, legal documents, and technical manuals
- Convert documents to markdown for further processing in RAG pipelines

For more detailed information about Contextual AI's capabilities, visit the [official documentation](https://docs.contextual.ai).