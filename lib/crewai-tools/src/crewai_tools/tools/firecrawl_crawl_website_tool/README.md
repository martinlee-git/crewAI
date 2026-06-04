# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/firecrawl_crawl_website_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/firecrawl_crawl_website_tool/README.md`

## 한글 요약

FirecrawlCrawlWebsiteTool 설명 Firecrawl은 웹사이트를 크롤링하고 깔끔한 마크다운 또는 구조화된 데이터로 변환하는 플랫폼입니다. 버전 호환성 이 구현은 FireCrawl API v1 설치와 호환됩니다. firecrawl.dev에서 API 키를 가져와 환경 변수(FIRECRAWL API KEY)에 설정합니다. Crewai[tools] 패키지와 함께 Firecrawl SDK를 설치합니다. 예 에이전트가 웹사이트를 로드할 수 있도록 다음과 같이 FirecrawlScrapeFromWebsiteTool을 활용합니다. 인수 api 키: 선택 사항. Firecrawl API 키를 지정합니다. 기본값은 FIRECRAWL API KEY 환경 변수입니다. 구성: 선택 사항입니다. Firecrawl API 매개변수가 포함되어 있습니다. 이것이 기본 구성입니다

## 핵심 발췌

FirecrawlCrawlWebsiteTool ## 설명 Firecrawl은 웹사이트를 크롤링하고 깔끔한 마크다운 또는 구조화된 데이터로 변환하는 플랫폼입니다. ## 버전 호환성 이 구현은

## 원문 내용

# FirecrawlCrawlWebsiteTool

## Description

[Firecrawl](https://firecrawl.dev) is a platform for crawling and convert any website into clean markdown or structured data.

## Version Compatibility

This implementation is compatible with FireCrawl API v1

## Installation

- Get an API key from [firecrawl.dev](https://firecrawl.dev) and set it in environment variables (`FIRECRAWL_API_KEY`).
- Install the [Firecrawl SDK](https://github.com/mendableai/firecrawl) along with `crewai[tools]` package:

```
pip install firecrawl-py 'crewai[tools]'
```

## Example

Utilize the FirecrawlScrapeFromWebsiteTool as follows to allow your agent to load websites:

```python
from crewai_tools import FirecrawlCrawlWebsiteTool
from firecrawl import ScrapeOptions

tool = FirecrawlCrawlWebsiteTool(
    config={
        "limit": 100,
        "scrape_options": ScrapeOptions(formats=["markdown", "html"]),
        "poll_interval": 30,
    }
)
tool.run(url="firecrawl.dev")
```

## Arguments

- `api_key`: Optional. Specifies Firecrawl API key. Defaults is the `FIRECRAWL_API_KEY` environment variable.
- `config`: Optional. It contains Firecrawl API parameters.

This is the default configuration

```python
from firecrawl import ScrapeOptions

{
    "max_depth": 2,
    "ignore_sitemap": True,
    "limit": 100,
    "allow_backward_links": False,
    "allow_external_links": False,
    "scrape_options": ScrapeOptions(
        formats=["markdown", "screenshot", "links"],
        only_main_content=True,
        timeout=30000,
    ),
}
```