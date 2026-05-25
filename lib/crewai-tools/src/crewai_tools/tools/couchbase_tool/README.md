# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/couchbase_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/couchbase_tool/README.md`

## 한글 요약

CouchbaseFTSVectorSearchTool 설명 Couchbase는 벡터 검색 기능을 갖춘 NoSQL 데이터베이스입니다. 사용자는 벡터 임베딩을 저장하고 쿼리할 수 있습니다. 여기에서 Couchbase 벡터 검색에 대해 자세히 알아볼 수 있습니다: https://docs.couchbase.com/cloud/벡터 검색/벡터 검색.html 이 도구는 Couchbase를 사용하여 의미론적 검색을 수행하기 위해 특별히 제작되었습니다. 이 도구를 사용하면 주어진 쿼리와 의미상 유사한 문서를 찾을 수 있습니다. 설치 터미널에서 다음 명령을 실행하여 크루아이 도구 패키지를 설치합니다. 설정 도구를 인스턴스화하기 전에 Couchbase 클러스터가 필요합니다. Couchbase의 클라우드 데이터베이스 솔루션인 Couchbase Capella에 클러스터를 생성하세요. 로컬 Couchbase 서버를 만듭니다. 클러스터에 버킷, 범위, 컬렉션을 생성해야 합니다. 그런 다음 이 가이드에 따라 Couchbase Cluster 개체를 생성하고 문서를 컬렉션에 로드하세요. Couchbase에서 벡터 검색 색인을 생성하려면 아래 문서를 따르세요. Couchbase Capella에서 벡터 검색 색인을 생성합니다. 벡터 만들기

## 핵심 발췌

로컬 Couchbase 서버에서 색인을 검색하세요. 인덱스의 차원 필드가 임베딩 모델과 일치하는지 확인하세요. 예를 들어 OpenAI의 텍스트 임베딩 3 소형 모델의 임베딩 차원은 1536차원이므로 인덱스의 차원 필드는 1536이어야 합니다. 예 다양한 사용 사례에 CouchbaseFTSVectorSearchTool을 활용하려면 다음 예를 따르십시오. 인수 클러스터: 초기화된 Couchbase 클러스터 인스턴스입니다. 버킷 이름: Couchbase 버킷의 이름입니다. 범위 이름: 버킷 내의 범위 이름입니다. 컬렉션 이름: 범위 내의 컬렉션 이름입니다. index name: 검색 인덱스(벡터 인덱스)의 이름입니다. 임베딩 함수: 문자열을 가져와 해당 임베딩(부동 소수점 목록)을 반환하는 함수입니다. 임베딩 키: 검색 인덱스의 필드 이름

## 원문 내용

# CouchbaseFTSVectorSearchTool
## Description
Couchbase is a NoSQL database with vector search capabilities. Users can store and query vector embeddings. You can learn more about Couchbase vector search here: https://docs.couchbase.com/cloud/vector-search/vector-search.html 

This tool is specifically crafted for performing semantic search using Couchbase. Use this tool to find semantically similar docs to a given query.

## Installation
Install the crewai_tools package by executing the following command in your terminal:

```shell
uv pip install 'crewai[tools]'
```

## Setup
Before instantiating the tool, you need a Couchbase cluster. 
- Create a cluster on [Couchbase Capella](https://docs.couchbase.com/cloud/get-started/create-account.html), Couchbase's cloud database solution.
- Create a [local Couchbase server](https://docs.couchbase.com/server/current/getting-started/start-here.html). 

You will need to create a bucket, scope and collection on the cluster. Then, [follow this guide](https://docs.couchbase.com/python-sdk/current/hello-world/start-using-sdk.html) to create a Couchbase Cluster object and load documents into your collection.

Follow the docs below to create a vector search index on Couchbase.
- [Create a vector search index on Couchbase Capella.](https://docs.couchbase.com/cloud/vector-search/create-vector-search-index-ui.html)
- [Create a vector search index on your local Couchbase server.](https://docs.couchbase.com/server/current/vector-search/create-vector-search-index-ui.html)

Ensure that the `Dimension` field in the index matches the embedding model. For example, OpenAI's `text-embedding-3-small` model has an embedding dimension of 1536 dimensions, and so the `Dimension` field must be 1536 in the index.

## Example
To utilize the CouchbaseFTSVectorSearchTool for different use cases, follow these examples:

```python
from crewai_tools import CouchbaseFTSVectorSearchTool

# Instantiate a Couchbase Cluster object from the Couchbase SDK

tool = CouchbaseFTSVectorSearchTool(
    cluster=cluster,
    collection_name="collection",
    scope_name="scope",
    bucket_name="bucket",
    index_name="index",
    embedding_function=embed_fn
)

# Adding the tool to an agent
rag_agent = Agent(
    name="rag_agent",
    role="You are a helpful assistant that can answer questions with the help of the CouchbaseFTSVectorSearchTool.",
    llm="gpt-4o-mini",
    tools=[tool],
)
```

## Arguments
- `cluster`: An initialized Couchbase `Cluster` instance. 
- `bucket_name`: The name of the Couchbase bucket. 
- `scope_name`: The name of the scope within the bucket. 
- `collection_name`: The name of the collection within the scope. 
- `index_name`: The name of the search index (vector index). 
- `embedding_function`: A function that takes a string and returns its embedding (list of floats). 
- `embedding_key`: Name of the field in the search index storing the vector. (Optional, defaults to 'embedding')
- `scoped_index`: Whether the index is scoped (True) or cluster-level (False). (Optional, defaults to True)
- `limit`: The maximum number of search results to return. (Optional, defaults to 3)