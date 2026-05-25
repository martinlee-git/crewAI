# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/databricks_query_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/databricks_query_tool/README.md`

## 한글 요약

Databricks 쿼리 도구 설명 이 도구를 사용하면 AI 에이전트가 Databricks 작업 영역 테이블에 대해 SQL 쿼리를 실행하고 결과를 검색할 수 있습니다. SQL을 사용하여 Databricks 테이블에서 데이터를 쿼리하기 위한 간단한 인터페이스를 제공하므로 에이전트가 Databricks에 저장된 데이터에 쉽게 액세스하고 분석할 수 있습니다. 설치 databricks extra: 인증을 사용하여 크루아이 도구 패키지를 설치합니다. 이 도구에는 Databricks 인증 자격 증명이 필요합니다. 이를 두 가지 방법으로 제공할 수 있습니다. 1. Databricks CLI 프로필 사용: DATABRICKS CONFIG PROFILE 환경 변수를 프로필 이름으로 설정합니다. 2. 직접 자격 증명 사용: DATABRICKS HOST 및 DATABRICKS TOKEN 환경 변수를 모두 설정합니다. 예: 사용 매개 변수 쿼리를 실행할 때 다음 매개 변수를 제공할 수 있습니다. 쿼리(필수): Databricks 작업 영역 카탈로그에 대해 실행할 SQL 쿼리(선택 사항): Databricks 카탈로그 이름 스키마(선택 사항): Databricks 스키마 이름 웨어하우스 ID(선택 사항): Databricks SQL 웨어하우스 ID 행

## 핵심 발췌

제한(선택 사항): 반환할 최대 행 수(기본값: 1000) 제공되지 않으면 도구는 초기화 중에 설정된 기본값을 사용합니다.

## 원문 내용

# Databricks Query Tool

## Description

This tool allows AI agents to execute SQL queries against Databricks workspace tables and retrieve the results. It provides a simple interface for querying data from Databricks tables using SQL, making it easy for agents to access and analyze data stored in Databricks.

## Installation

Install the crewai_tools package with the databricks extra:

```shell
pip install 'crewai[tools]' 'databricks-sdk'
```

## Authentication

The tool requires Databricks authentication credentials. You can provide these in two ways:

1. **Using Databricks CLI profile**:
   - Set the `DATABRICKS_CONFIG_PROFILE` environment variable to your profile name.

2. **Using direct credentials**:
   - Set both `DATABRICKS_HOST` and `DATABRICKS_TOKEN` environment variables.

Example:
```shell
export DATABRICKS_HOST="https://your-workspace.cloud.databricks.com"
export DATABRICKS_TOKEN="dapi1234567890abcdef"
```

## Usage

```python
from crewai_tools import DatabricksQueryTool

# Basic usage
databricks_tool = DatabricksQueryTool()

# With default parameters for catalog, schema, and warehouse
databricks_tool = DatabricksQueryTool(
    default_catalog="my_catalog",
    default_schema="my_schema",
    default_warehouse_id="warehouse_id"
)

# Example in a CrewAI agent
@agent
def data_analyst(self) -> Agent:
    return Agent(
        config=self.agents_config["data_analyst"],
        allow_delegation=False,
        tools=[databricks_tool]
    )
```

## Parameters

When executing queries, you can provide the following parameters:

- `query` (required): SQL query to execute against the Databricks workspace
- `catalog` (optional): Databricks catalog name
- `schema` (optional): Databricks schema name
- `warehouse_id` (optional): Databricks SQL warehouse ID
- `row_limit` (optional): Maximum number of rows to return (default: 1000)

If not provided, the tool will use the default values set during initialization.