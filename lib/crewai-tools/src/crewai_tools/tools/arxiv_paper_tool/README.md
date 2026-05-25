# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/arxiv_paper_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/arxiv_paper_tool/README.md`

## 한글 요약

ArxivPaperTool 📚 ArxivPaperTool ArxivPaperTool은 공개 API를 사용하여 arXiv 플랫폼에서 메타데이터를 가져오고 선택적으로 학술 논문의 PDF를 다운로드하는 유틸리티입니다. 구성 가능한 쿼리, 일괄 검색, PDF 다운로드, 요약 및 메타데이터에 대한 깔끔한 형식 지정을 지원합니다. 이 도구는 자동화된 문헌 검토를 수행하는 연구자, 학생, 학술 대리인 및 AI 도구에 특히 유용합니다. 설명 이 도구는 검색 쿼리를 수락하고 arXiv에서 논문 목록을 검색합니다. 가져올 최대 결과 수를 구성할 수 있습니다. 선택적으로 일치하는 논문의 PDF를 다운로드합니다. arXiv ID 또는 논문 제목을 사용하여 PDF 파일의 이름을 지정할지 여부를 지정할 수 있습니다. 다운로드한 파일을 사용자 정의 또는 기본 디렉토리에 저장합니다. 메타데이터를 포함하여 가져온 모든 논문의 구조화된 요약을 반환합니다. 인수 | 인수 | 유형 | 필수 | 설명 | | | | | | | 검색어 | str | ✅ | 검색어 문자열(예: "변압기 신경망"). |

## 핵심 발췌

| 최대 결과 | 정수 | ✅ | 가져올 결과 수(1~100)입니다. | | PDF 다운로드 | 부울 | ❌ | 해당 PDF를 다운로드할지 여부입니다. 기본값은 False입니다. | | 디렉토리 저장 | str | ❌ | PDF를 저장할 디렉토리(존재하지 않는 경우 생성됨) 기본값은 ./arxiv PDF입니다. | | 제목을 파일 이름으로 사용 | 부울 | ❌ | 논문 제목을 파일 이름으로 사용합니다(삭제됨). 기본값은 False입니다. | 📄 ArxivPaperTool 사용 예 이 문서는 ArxivPaperTool을 사용하여 arXiv에서 연구 논문 메타데이터를 가져오고 선택적으로 PDF를 다운로드하는 방법을 보여줍니다. 🔧 도구 초기화 예 1: 메타데이터만 가져오기(다운로드 없음) 예 2: PDF 가져오기 및 다운로드(arXiv ID를 파일 이름으로) 예 3: PDF를 사용자 정의 디렉터리로 다운로드 예 4: 문서 제목을 파일 이름으로 사용 예 5: 모든 옵션 결합 기본을 통해 실행

## 원문 내용

# ArxivPaperTool


# 📚 ArxivPaperTool

The **ArxivPaperTool** is a utility for fetching metadata and optionally downloading PDFs of academic papers from the [arXiv](https://arxiv.org) platform using its public API. It supports configurable queries, batch retrieval, PDF downloading, and clean formatting for summaries and metadata. This tool is particularly useful for researchers, students, academic agents, and AI tools performing automated literature reviews.

---

## Description

This tool:

* Accepts a **search query** and retrieves a list of papers from arXiv.
* Allows configuration of the **maximum number of results** to fetch.
* Optionally downloads the **PDFs** of the matched papers.
* Lets you specify whether to name PDF files using the **arXiv ID** or **paper title**.
* Saves downloaded files into a **custom or default directory**.
* Returns structured summaries of all fetched papers including metadata.

---

## Arguments

| Argument                | Type   | Required | Description                                                                       |
| ----------------------- | ------ | -------- | --------------------------------------------------------------------------------- |
| `search_query`          | `str`  | ✅        | Search query string (e.g., `"transformer neural network"`).                       |
| `max_results`           | `int`  | ✅        | Number of results to fetch (between 1 and 100).                                   |
| `download_pdfs`         | `bool` | ❌        | Whether to download the corresponding PDFs. Defaults to `False`.                  |
| `save_dir`              | `str`  | ❌        | Directory to save PDFs (created if it doesn’t exist). Defaults to `./arxiv_pdfs`. |
| `use_title_as_filename` | `bool` | ❌        | Use the paper title as the filename (sanitized). Defaults to `False`.             |

---

## 📄 `ArxivPaperTool` Usage Examples

This document shows how to use the `ArxivPaperTool` to fetch research paper metadata from arXiv and optionally download PDFs.

### 🔧 Tool Initialization

```python
from crewai_tools import ArxivPaperTool 
```

---

### Example 1: Fetch Metadata Only (No Downloads)

```python
tool = ArxivPaperTool()
result = tool._run(
    search_query="deep learning",
    max_results=1
)
print(result)
```

---

### Example 2: Fetch and Download PDFs (arXiv ID as Filename)

```python
tool = ArxivPaperTool(download_pdfs=True)
result = tool._run(
    search_query="transformer models",
    max_results=2
)
print(result)
```

---

### Example 3: Download PDFs into a Custom Directory

```python
tool = ArxivPaperTool(
    download_pdfs=True,
    save_dir="./my_papers"
)
result = tool._run(
    search_query="graph neural networks",
    max_results=2
)
print(result)
```

---

### Example 4: Use Paper Titles as Filenames

```python
tool = ArxivPaperTool(
    download_pdfs=True,
    use_title_as_filename=True
)
result = tool._run(
    search_query="vision transformers",
    max_results=1
)
print(result)
```

---

### Example 5: All Options Combined

```python
tool = ArxivPaperTool(
    download_pdfs=True,
    save_dir="./downloads",
    use_title_as_filename=True
)
result = tool._run(
    search_query="stable diffusion",
    max_results=3
)
print(result)
```

---

### Run via `__main__`

Your file can also include:

```python
if __name__ == "__main__":
    tool = ArxivPaperTool(
        download_pdfs=True,
        save_dir="./downloads2",
        use_title_as_filename=False
    )
    result = tool._run(
        search_query="deep learning",
        max_results=1
    )
    print(result)
```

---