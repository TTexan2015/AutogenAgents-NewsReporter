# AutogenAgents-NewsReporter

Agentic AI examples using Round Robin and Selector pattern with Microsoft AutoGen framework for automated news article creation and editing workflows.

## Overview

This project demonstrates two distinct multi-agent collaboration patterns using Azure OpenAI and the AutoGen framework:

- **Round Robin Pattern**: Sequential agent execution for simple news article creation workflow
- **Selector Pattern**: AI-driven agent selection for complex task delegation and coordination

## Features

- **Multi-Agent Collaboration**: News Reporter, Editor, Planning, and Headline Generator agents
- **Azure OpenAI Integration**: GPT-4o model with Azure Active Directory authentication
- **Flexible Patterns**: Compare sequential vs. dynamic agent orchestration
- **Real-time Streaming**: Console output showing agent interactions
- **Termination Conditions**: Smart workflow completion based on content approval or task completion

## Quick Start

### Prerequisites

- Python 3.8+
- Azure OpenAI service access
- Azure Active Directory credentials configured

### Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd AutogenAgents-NewsReporter
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure environment variables in `.env`:
   ```bash
   model-name="gpt-4o"
   api-version="2024-12-01-preview"
   azure_endpoint="https://your-azure-openai-endpoint.openai.azure.com/"
   ```

4. Ensure Azure AD authentication is configured on your system

### Usage

#### Run Round Robin Pattern
```bash
python roundrobin.py
```

**Workflow**: News Reporter → News Editor → Approval/Iteration

#### Run Selector Pattern
```bash
python selector.py
```

**Workflow**: Planning Agent coordinates News Reporter, News Editor, and Headline Generator

## Architecture

### Round Robin Pattern
- **Simple Sequential Processing**: Agents execute in predefined order
- **Two-Agent Team**: News Reporter and News Editor
- **Text-based Termination**: Stops when Editor responds with "APPROVE"

### Selector Pattern
- **Dynamic Agent Selection**: AI chooses the next agent based on context
- **Four-Agent Team**: Planning Agent, News Reporter, News Editor, Headline Generator
- **Complex Coordination**: Planning agent delegates and manages subtasks

## Technical Stack

- **AutoGen Framework**: Multi-agent orchestration
- **Azure OpenAI**: GPT-4o language model
- **Azure Identity**: Authentication and token management
- **Python-dotenv**: Environment configuration

## Documentation

Comprehensive technical documentation is available in the [`TechnicalDocs/`](TechnicalDocs/) directory:

- [Project Overview](TechnicalDocs/ProjectOverview.md) - Detailed architecture and module documentation
- [Infrastructure Design](TechnicalDocs/InfrastructureDesign.md) - Azure cloud architecture and deployment
- [Development Guide](TechnicalDocs/DevelopmentGuide.md) - Workflows, setup, and troubleshooting
- [Documentation Index](TechnicalDocs/DocumentationIndex.md) - Navigation guide for all documentation

## Authentication

This project uses Azure Active Directory authentication via `DefaultAzureCredential`, eliminating the need for API keys in configuration. Ensure your environment has proper Azure AD credentials configured.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test with both patterns
5. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For issues and questions:
1. Check the [troubleshooting guide](TechnicalDocs/ProjectOverview.md#known-issues-and-troubleshooting)
2. Review the [development guide](TechnicalDocs/DevelopmentGuide.md)
3. Create an issue in the repository
