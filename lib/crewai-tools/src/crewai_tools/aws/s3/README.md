# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/aws/s3/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/aws/s3/README.md`

## 한글 요약

AWS S3 도구 설명 이러한 도구는 클라우드 스토리지 서비스인 Amazon S3와 상호 작용하는 방법을 제공합니다. 설치 Crewai 도구 패키지를 설치합니다. AWS 연결 도구는 boto3을 사용하여 AWS S3에 연결합니다. AWS IAM 역할을 사용하도록 환경을 구성할 수 있습니다. AWS IAM 역할 설명서를 참조하십시오. 다음 환경 변수를 설정하십시오. CREW AWS REGION CREW AWS ACCESS KEY ID CREW AWS SEC ACCESS KEY 사용법 CrewAI 에이전트에서 AWS S3 도구를 사용하려면 필요한 도구를 가져와 에이전트 구성에 포함시킵니다. 이러한 도구는 CrewAI 워크플로 내의 S3 버킷에서 읽고 쓰는 데 사용할 수 있습니다. 위의 AWS 연결 섹션에 언급된 대로 AWS 자격 증명을 올바르게 구성했는지 확인하십시오.

## 핵심 발췌

AWS S3 도구 ## 설명 이러한 도구는 클라우드 스토리지 서비스인 Amazon S3와 상호 작용하는 방법을 제공합니다. ## 설치 Crewai 도구 패키지 설치 ## AWS Connecti

## 원문 내용

# AWS S3 Tools

## Description

These tools provide a way to interact with Amazon S3, a cloud storage service.

## Installation

Install the crewai_tools package

```shell
pip install 'crewai[tools]'
```

## AWS Connectivity

The tools use `boto3` to connect to AWS S3.
You can configure your environment to use AWS IAM roles, see [AWS IAM Roles documentation](https://docs.aws.amazon.com/sdk-for-python/v1/developer-guide/iam-roles.html#creating-an-iam-role)

Set the following environment variables:

- `CREW_AWS_REGION`
- `CREW_AWS_ACCESS_KEY_ID`
- `CREW_AWS_SEC_ACCESS_KEY`

## Usage

To use the AWS S3 tools in your CrewAI agents, import the necessary tools and include them in your agent's configuration:

```python
from crewai_tools.aws.s3 import S3ReaderTool, S3WriterTool

# For reading from S3
@agent
def file_retriever(self) -> Agent:
    return Agent(
        config=self.agents_config['file_retriever'],
        verbose=True,
        tools=[S3ReaderTool()]
    )

# For writing to S3
@agent
def file_uploader(self) -> Agent:
    return Agent(
        config=self.agents_config['file_uploader'],
        verbose=True,
        tools=[S3WriterTool()]
    )
```

These tools can be used to read from and write to S3 buckets within your CrewAI workflows. Make sure you have properly configured your AWS credentials as mentioned in the AWS Connectivity section above.