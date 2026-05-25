# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/cli/src/crewai_cli/templates/tool/README.md
- 미러 경로: `lib/cli/src/crewai_cli/templates/tool/README.md`

## 한글 요약

{{폴더 이름}} {{폴더 이름}}은 CrewAI 도구입니다. 이 템플릿은 팀의 역량을 강화하는 맞춤형 도구를 만드는 데 도움이 되도록 설계되었습니다. 설치 시스템에 Python =3.10 <3.14가 설치되어 있는지 확인하십시오. 이 프로젝트는 종속성 관리 및 패키지 처리에 UV를 사용하여 원활한 설정 및 실행 환경을 제공합니다. 먼저, 아직 설치하지 않았다면 uv를 설치합니다. 그런 다음 프로젝트 디렉터리로 이동하여 다음을 사용하여 종속성을 설치합니다. 게시 조직 내에서 도구를 공유하여 공동 작업하거나 공개적으로 게시하여 커뮤니티에 기여합니다. 다른 사람들은 다음을 실행하는 팀에 귀하의 도구를 설치할 수 있습니다. 지원 {{crew name}} 도구 또는 CrewAI에 관한 지원, 질문 또는 피드백. 문서를 방문하십시오. GitHub 저장소를 통해 우리에게 연락하십시오. 문서와 함께 Discord 채팅에 참여하십시오. 크루 AI의 강력함과 단순함으로 함께 경이로움을 만들어 봅시다.

## 핵심 발췌

{{폴더 이름}} {{폴더 이름}}은 CrewAI 도구입니다. 이 템플릿은 팀의 역량을 강화하는 맞춤형 도구를 만드는 데 도움이 되도록 설계되었습니다. ## 설치 시스템에 Python =3.10 <3.14가 설치되어 있는지 확인하세요. 이 홍보

## 원문 내용

# {{folder_name}}

{{folder_name}} is a CrewAI Tool. This template is designed to help you create
custom tools to power up your crews.

## Installing

Ensure you have Python >=3.10 <3.14 installed on your system. This project
uses [UV](https://docs.astral.sh/uv/) for dependency management and package
handling, offering a seamless setup and execution experience.

First, if you haven't already, install `uv`:

```bash
pip install uv
```

Next, navigate to your project directory and install the dependencies with:

```bash
crewai install
```

## Publishing

Collaborate by sharing tools within your organization, or publish them publicly
to contribute with the community.

```bash
crewai tool publish {{tool_name}}
```

Others may install your tool in their crews running:

```bash
crewai tool install {{tool_name}}
```

## Support

For support, questions, or feedback regarding the {{crew_name}} tool or CrewAI.

- Visit our [documentation](https://docs.crewai.com)
- Reach out to us through our [GitHub repository](https://github.com/joaomdmoura/crewai)
- [Join our Discord](https://discord.com/invite/X4JWnZnxPb)
- [Chat with our docs](https://chatg.pt/DWjSBZn)

Let's create wonders together with the power and simplicity of crewAI.