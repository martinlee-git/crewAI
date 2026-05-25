# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/brightdata_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/brightdata_tool/README.md`

## 한글 요약

BrightData 도구 설명서 설명 웹 스크래핑, 데이터 추출 및 검색 작업을 위해 Bright Data의 강력한 인프라를 활용하는 포괄적인 CrewAI 도구 제품군입니다. 이러한 도구는 세 가지 고유한 기능을 제공합니다. BrightDataDatasetTool: 사전 구축된 데이터 세트를 사용하여 인기 있는 데이터 피드(Amazon, LinkedIn, Instagram 등)에서 구조화된 데이터 추출 BrightDataSearchTool: 지역 타겟팅 및 장치 시뮬레이션을 사용하여 여러 검색 엔진에서 웹 검색 수행 BrightDataWebUnlockerTool: 봇 보호 메커니즘을 우회하면서 웹 사이트 콘텐츠 스크랩 설치 이러한 도구를 프로젝트에 통합하려면 아래 설치 지침을 따르십시오. 예제 데이터 세트 도구 Amazon 제품 데이터 검색 도구 추출 웹 검색 수행 웹 잠금 해제 도구 웹 사이트 콘텐츠 스크랩 가져오기 단계 시작됨 BrightData 도구를 효과적으로 사용하려면 다음 단계를 따르십시오. 1. 패키지 설치 : 크루아이[tools] 패키지가 Python 환경에 설치되어 있는지 확인합니다. 2

## 핵심 발췌

. API 키 취득: https://brightdata.com/에서 Bright Data 계정을 등록하고 계정 설정에서 API 자격 증명을 받으세요. 3. 환경 구성: 필요한 환경 변수 설정: 4. 도구 선택: 필요에 따라 적절한 도구 선택: 지원되는 플랫폼의 구조화된 데이터에 DatasetTool 사용 웹 검색 작업에 SearchTool 사용 일반 웹 사이트 스크래핑에 WebUnlockerTool 사용 결론 BrightData 도구를 CrewAI 에이전트에 통합하면 엔터프라이즈급 웹 스크래핑 및 데이터 추출 기능에 액세스할 수 있습니다. 이러한 도구는 봇 보호, 지리적 제한, 데이터 구문 분석과 같은 복잡한 문제를 처리하므로 스크래핑 인프라 관리보다는 애플리케이션 구축에 집중할 수 있습니다.

## 원문 내용

# BrightData Tools Documentation

## Description

A comprehensive suite of CrewAI tools that leverage Bright Data's powerful infrastructure for web scraping, data extraction, and search operations. These tools provide three distinct capabilities:

- **BrightDataDatasetTool**: Extract structured data from popular data feeds (Amazon, LinkedIn, Instagram, etc.) using pre-built datasets
- **BrightDataSearchTool**: Perform web searches across multiple search engines with geo-targeting and device simulation
- **BrightDataWebUnlockerTool**: Scrape any website content while bypassing bot protection mechanisms

## Installation

To incorporate these tools into your project, follow the installation instructions below:

```shell
pip install crewai[tools] aiohttp requests
```

## Examples

### Dataset Tool - Extract Amazon Product Data
```python
from crewai_tools import BrightDataDatasetTool

# Initialize with specific dataset and URL
tool = BrightDataDatasetTool(
    dataset_type="amazon_product",
    url="https://www.amazon.com/dp/B08QB1QMJ5/"
)
result = tool.run()
```

### Search Tool - Perform Web Search
```python
from crewai_tools import BrightDataSearchTool

# Initialize with search query
tool = BrightDataSearchTool(
    query="latest AI trends 2025",
    search_engine="google",
    country="us"
)
result = tool.run()
```

### Web Unlocker Tool - Scrape Website Content
```python
from crewai_tools import BrightDataWebUnlockerTool

# Initialize with target URL
tool = BrightDataWebUnlockerTool(
    url="https://example.com",
    data_format="markdown"
)
result = tool.run()
```

## Steps to Get Started

To effectively use the BrightData Tools, follow these steps:

1. **Package Installation**: Confirm that the `crewai[tools]` package is installed in your Python environment.

2. **API Key Acquisition**: Register for a Bright Data account at `https://brightdata.com/` and obtain your API credentials from your account settings.

3. **Environment Configuration**: Set up the required environment variables:
   ```bash
   export BRIGHT_DATA_API_KEY="your_api_key_here"
   export BRIGHT_DATA_ZONE="your_zone_here"
   ```

4. **Tool Selection**: Choose the appropriate tool based on your needs:
   - Use **DatasetTool** for structured data from supported platforms
   - Use **SearchTool** for web search operations
   - Use **WebUnlockerTool** for general website scraping

## Conclusion

By integrating BrightData Tools into your CrewAI agents, you gain access to enterprise-grade web scraping and data extraction capabilities. These tools handle complex challenges like bot protection, geo-restrictions, and data parsing, allowing you to focus on building your applications rather than managing scraping infrastructure.