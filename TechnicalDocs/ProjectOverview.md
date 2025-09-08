# AutogenAgents-NewsReporter Project Documentation

## Referenced Files
- [roundrobin.py](../roundrobin.py) - Round Robin pattern implementation with News Reporter and Editor agents
- [selector.py](../selector.py) - Selector pattern implementation with Planning, Reporter, Editor, and Headline Generator agents
- [requirements.txt](../requirements.txt) - Project dependencies
- [README.md](../README.md) - Basic project description

## Overview

AutogenAgents-NewsReporter is a Python project that demonstrates **Agentic AI patterns** using Microsoft's AutoGen framework. The project showcases two distinct multi-agent collaboration patterns: **Round Robin** and **Selector** patterns for automated news article creation and editing workflows.

### Primary Purpose

The repository serves as an educational example of how different agent orchestration patterns can be implemented to create collaborative AI systems that work together to produce high-quality news content.

## Architecture Overview

The project implements two distinct agent collaboration patterns:

### 1. Round Robin Pattern ([`roundrobin.py`](../roundrobin.py))
- **Simple Sequential Processing**: Agents take turns in a predefined order
- **Two-Agent Workflow**: News Reporter → News Editor
- **Automatic Termination**: Stops when Editor responds with "APPROVE"

### 2. Selector Pattern ([`selector.py`](../selector.py))
- **Dynamic Agent Selection**: AI-driven selection of the next agent to execute
- **Four-Agent Workflow**: Planning Agent coordinates News Reporter, News Editor, and Headline Generator
- **Complex Task Delegation**: Planning agent breaks down tasks and assigns them to specialized agents

## Core Components

### Agent Definitions

#### News Reporter Agent
- **Role**: Creates news articles based on given facts
- **Behavior**: Writes concise, factual news content
- **Implementation**: Present in both patterns with similar functionality

#### News Editor Agent
- **Round Robin**: Reviews and improves articles, responds with "APPROVE" when satisfied
- **Selector**: Provides feedback and suggestions but doesn't write content

#### Planning Agent (Selector Only)
- **Role**: Task coordination and delegation
- **Behavior**: Breaks down complex tasks and assigns them to team members
- **Termination**: Summarizes findings and ends with "TERMINATE"

#### Headline Generator Agent (Selector Only)
- **Role**: Creates engaging headlines for news articles
- **Behavior**: Focuses specifically on headline creation

### Technology Stack

#### Core Dependencies
- **autogen-agentchat**: Main framework for agent creation and orchestration
- **autogen-ext[azure]**: Azure-specific extensions for model integration
- **python-dotenv**: Environment variable management
- **azure-identity**: Azure authentication and token management

#### Azure Integration
- **Azure OpenAI**: Language model backend via [`AzureOpenAIChatCompletionClient`](../roundrobin.py:40)
- **Azure Active Directory**: Authentication using [`DefaultAzureCredential`](../roundrobin.py:17)
- **Token Provider**: Bearer token authentication for secure API access

## Module Documentation

### roundrobin.py

**Primary Functions:**
- [`main()`](../roundrobin.py:77): Main execution function that runs the Round Robin team
- Agent initialization with Azure OpenAI client
- Team configuration with termination conditions

**Key Classes and Objects:**
- [`News_Reporter`](../roundrobin.py:50): Assistant agent for article writing
- [`News_Editor`](../roundrobin.py:60): Assistant agent for article review and editing
- [`RoundRobinGroupChat`](../roundrobin.py:74): Team orchestrator for sequential agent execution
- [`TextMentionTermination`](../roundrobin.py:71): Termination condition based on "APPROVE" text

**Configuration:**
- Model client setup with Azure OpenAI integration
- Environment variable loading for API credentials
- System message definitions for agent behavior

### selector.py

**Primary Functions:**
- [`main()`](../selector.py:116): Main execution function that runs the Selector team
- Advanced agent coordination with planning capabilities

**Key Classes and Objects:**
- [`planning_agent`](../selector.py:46): Coordinator agent for task delegation
- [`News_Reporter`](../selector.py:75): Article writing specialist
- [`News_Editor`](../selector.py:86): Content review and feedback provider
- [`Headline_Generator`](../selector.py:97): Headline creation specialist
- [`SelectorGroupChat`](../selector.py:107): AI-driven team orchestrator

**Advanced Features:**
- Multiple termination conditions (text mention OR max messages)
- Dynamic agent selection based on context
- Task delegation and coordination workflow

## Configuration Details

### Environment Variables (.env)
```bash
model-name="gpt-4o"
api-version="2024-12-01-preview"
azure_endpoint="https://ai-icmhub008703513730.openai.azure.com/"
```

**Note**: This project uses Azure Active Directory authentication via `DefaultAzureCredential`, so no API key is required in the environment file.

### Model Configuration
Both implementations use identical model configuration:
- **Model Family**: GPT-4o
- **Azure Deployment**: Environment-specified model name (gpt-4o)
- **Authentication**: Azure AD token provider (no API key required)
- **API Version**: 2024-12-01-preview

## Usage Examples

### Running Round Robin Pattern
```bash
python roundrobin.py
```

**Expected Flow:**
1. News Reporter creates initial article
2. News Editor reviews and improves content
3. Process continues until Editor approves with "APPROVE"
4. Console streams all agent interactions

### Running Selector Pattern
```bash
python selector.py
```

**Expected Flow:**
1. Planning Agent analyzes task and creates execution plan
2. Delegates specific subtasks to appropriate agents
3. Coordinates multiple rounds of content creation and review
4. Headline Generator adds engaging headlines
5. Planning Agent summarizes and terminates with "TERMINATE"

## Setup Instructions

### Prerequisites
- Python 3.8+
- Azure OpenAI service access
- Azure Active Directory credentials

### Installation
1. Clone the repository
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Configure environment variables in `.env` file
4. Ensure Azure AD authentication is properly configured

### Development Setup
1. Set up Azure OpenAI service
2. Configure Azure AD application for authentication
3. Create `.env` file with required credentials
4. Test authentication and model access

## Known Issues and Troubleshooting

### Common Issues

1. **Authentication Failures**
   - Verify Azure AD credentials and permissions
   - Ensure `DefaultAzureCredential` can access required scopes
   - Check Azure OpenAI service endpoint configuration

2. **Model Access Issues**
   - Verify model deployment name matches environment configuration
   - Check API version compatibility
   - Ensure sufficient quota and rate limits

3. **Environment Configuration**
   - Validate all required environment variables are set
   - Check Azure endpoint URL format
   - Verify API key format and validity

### Troubleshooting Steps

1. **Test Azure Authentication**:
   ```python
   from azure.identity import DefaultAzureCredential
   credential = DefaultAzureCredential()
   # Should complete without errors
   ```

2. **Validate Environment Variables**:
   ```python
   from dotenv import load_dotenv
   import os
   load_dotenv()
   print(os.getenv("model-name"))  # Should return model name
   ```

3. **Check Model Client Connection**:
   - Run either script and observe initial connection attempts
   - Monitor console output for authentication and API errors

## Performance Considerations

### Scalability
- Round Robin: Linear scaling with agent count
- Selector: Dynamic scaling based on task complexity
- Both patterns support asynchronous execution

### Cost Optimization
- Monitor API usage through Azure portal
- Implement rate limiting for production use
- Consider caching strategies for repeated tasks

### Monitoring
- Console streaming provides real-time agent interactions
- Azure OpenAI provides usage metrics and analytics
- Consider implementing custom logging for production scenarios

## Security Best Practices

1. **Credential Management**
   - Use Azure Key Vault for production credentials
   - Implement proper secret rotation
   - Avoid hardcoding sensitive information

2. **Network Security**
   - Configure Azure OpenAI with appropriate network restrictions
   - Use private endpoints for enhanced security
   - Implement proper firewall rules

3. **Access Control**
   - Follow principle of least privilege for Azure AD permissions
   - Regular audit of access permissions
   - Implement proper resource group isolation