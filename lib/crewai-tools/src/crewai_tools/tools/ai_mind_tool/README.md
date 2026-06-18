# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/ai_mind_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/ai_mind_tool/README.md`

## 한글 요약

AIMind 도구 설명 Minds는 MindsDB에서 제공하는 AI 시스템으로 LLM(대형 언어 모델)과 유사하게 작동하지만 그 이상으로 모든 데이터의 질문에 답합니다. 이는 파라메트릭 검색을 통해 답변에 가장 관련성이 높은 데이터를 선택하고, 의미 검색을 통해 올바른 맥락 내에서 의미를 이해하고 응답을 제공하며, 마지막으로 데이터 분석 및 머신러닝(ML) 모델을 사용하여 정확한 답변을 제공함으로써 달성됩니다. AIMindTool을 사용하면 연결 매개변수를 간단히 구성하여 자연어로 데이터 소스를 쿼리할 수 있습니다. 설치 1. Crewai[tools] 패키지를 설치합니다. 2. Minds SDK를 설치합니다. 3. 여기에서 Minds 계정에 서명하고 API 키를 얻습니다. 4. MINDS API KEY라는 환경 변수에 Minds API 키를 설정합니다. 사용법 datasources 매개변수는 각각 다음 키를 포함하는 사전 목록입니다. 설명: 데이터 소스에 포함된 데이터에 대한 설명입니다. 엔진: 데이터의 엔진(또는 유형)

## 핵심 발췌

긴급. 아래 링크에서 지원되는 엔진 목록을 찾아보세요. 연결 데이터: 데이터 소스에 대한 연결 매개변수를 포함하는 사전입니다. 아래 링크에서 각 엔진에 대한 연결 매개변수 목록을 찾아보세요. tables: 데이터 소스가 사용할 테이블 목록입니다. 이는 선택사항이며 데이터 소스의 모든 테이블을 사용하려는 경우 생략할 수 있습니다. 지원되는 데이터 소스 및 해당 연결 매개변수 목록은 여기에서 확인할 수 있습니다.

## 원문 내용

# AIMind Tool

## Description

[Minds](https://mindsdb.com/minds) are AI systems provided by [MindsDB](https://mindsdb.com/) that work similarly to large language models (LLMs) but go beyond by answering any question from any data.

This is accomplished by selecting the most relevant data for an answer using parametric search, understanding the meaning and providing responses within the correct context through semantic search, and finally, delivering precise answers by analyzing data and using machine learning (ML) models.

The `AIMindTool` can be used to query data sources in natural language by simply configuring their connection parameters.

## Installation

1. Install the `crewai[tools]` package:

```shell
pip install 'crewai[tools]'
```

2. Install the Minds SDK:

```shell
pip install minds-sdk
```

3. Sign for a Minds account [here](https://mdb.ai/register), and obtain an API key.

4. Set the Minds API key in an environment variable named `MINDS_API_KEY`.

## Usage

```python
from crewai_tools import AIMindTool


# Initialize the AIMindTool.
aimind_tool = AIMindTool(
    datasources=[
        {
            "description": "house sales data",
            "engine": "postgres",
            "connection_data": {
                "user": "demo_user",
                "password": "demo_password",
                "host": "samples.mindsdb.com",
                "port": 5432,
                "database": "demo",
                "schema": "demo_data"
            },
            "tables": ["house_sales"]
        }
    ]
)

aimind_tool.run("How many 3 bedroom houses were sold in 2008?")
```

The `datasources` parameter is a list of dictionaries, each containing the following keys:

- `description`: A description of the data contained in the datasource.
- `engine`: The engine (or type) of the datasource. Find a list of supported engines in the link below.
- `connection_data`: A dictionary containing the connection parameters for the datasource. Find a list of connection parameters for each engine in the link below.
- `tables`: A list of tables that the data source will use. This is optional and can be omitted if all tables in the data source are to be used.

A list of supported data sources and their connection parameters can be found [here](https://docs.mdb.ai/docs/data_sources).

```python
from crewai import Agent
from crewai.project import agent


# Define an agent with the AIMindTool.
@agent
def researcher(self) -> Agent:
    return Agent(
        config=self.agents_config["researcher"],
        allow_delegation=False,
        tools=[aimind_tool]
    )
```