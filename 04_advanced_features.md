# Mistral Vibe CLI - Advanced Features Documentation

## Overview

The Mistral Vibe CLI includes several advanced features that extend its capabilities beyond basic file operations and code manipulation. These features enable sophisticated workflows, customization, and integration with other systems.

## 1. Agent Modes

**Location**: `/vibe/core/modes.py`

**Purpose**: Define different operational modes for the agent.

### Available Modes:

#### DEFAULT Mode
- **Behavior**: Standard interactive mode
- **Characteristics**:
  - User approval required for actions
  - Step-by-step execution
  - Interactive feedback
  - Safety checks enabled

#### AUTO_APPROVE Mode
- **Behavior**: Automatic execution without confirmation
- **Characteristics**:
  - No user approval required
  - Faster execution
  - Suitable for trusted operations
  - Programmatic usage

#### PLAN Mode
- **Behavior**: Planning and analysis mode
- **Characteristics**:
  - Focus on analysis and planning
  - Detailed breakdown of tasks
  - Step-by-step action plans
  - Recommendations without execution

### Mode Selection:
- **CLI Arguments**: `--auto-approve`, `--plan`
- **Programmatic**: Specified in `run_programmatic` call
- **Default**: DEFAULT mode for interactive sessions

### Use Cases:
- **DEFAULT**: Interactive coding sessions, learning, exploration
- **AUTO_APPROVE**: Trusted operations, CI/CD integration, automation
- **PLAN**: Complex problem analysis, architecture planning, strategy

## 2. Skills and Extensions

**Location**: `/vibe/core/skills/`

**Purpose**: Extend functionality with custom skills and plugins.

### Skill System:
- **Modular Design**: Add custom functionality
- **Plugin Architecture**: Easy integration
- **Skill Discovery**: Automatic detection
- **Configuration**: Skill-specific settings

### Available Skills:
- **Code Analysis**: Advanced code understanding
- **Refactoring**: Code improvement suggestions
- **Testing**: Test generation and execution
- **Documentation**: Documentation generation
- **Security**: Security analysis and fixes

### Creating Custom Skills:
```python
from vibe.core.skills import BaseSkill

class MyCustomSkill(BaseSkill):
    def __init__(self, config):
        super().__init__(config)
        self.name = "my_skill"
        self.description = "My custom functionality"
    
    def execute(self, *args, **kwargs):
        # Custom logic here
        return result
```

### Skill Management:
- **Enable/Disable**: Configure which skills are active
- **Priority**: Set skill execution order
- **Configuration**: Skill-specific parameters
- **Discovery**: Automatic skill loading

## 3. Middleware System

**Location**: `/vibe/core/middleware.py`

**Purpose**: Intercept and modify agent behavior at various stages.

### Middleware Types:

#### Pre-Processing Middleware
- **Execution Point**: Before prompt processing
- **Use Cases**:
  - Prompt transformation
  - Context enrichment
  - Input validation
  - Security checks

#### Post-Processing Middleware
- **Execution Point**: After response generation
- **Use Cases**:
  - Response formatting
  - Output filtering
  - Logging and analytics
  - Error handling

#### Tool Middleware
- **Execution Point**: Around tool execution
- **Use Cases**:
  - Tool usage logging
  - Safety checks
  - Performance monitoring
  - Error handling

### Middleware Example:
```python
from vibe.core.middleware import BaseMiddleware

class LoggingMiddleware(BaseMiddleware):
    async def pre_process(self, prompt, context):
        # Log incoming prompt
        self.log_prompt(prompt)
        return prompt, context
    
    async def post_process(self, response):
        # Log response
        self.log_response(response)
        return response
```

### Middleware Chain:
- **Order Matters**: Middleware executed in configured order
- **Short-circuiting**: Can interrupt processing chain
- **Configuration**: Enable/disable specific middleware

## 4. Trusted Folders

**Location**: `/vibe/core/trusted_folders.py`

**Purpose**: Manage access control to file system locations.

### Features:
- **Whitelist System**: Define trusted directories
- **Security**: Prevent access to sensitive areas
- **Configuration**: Customize trusted paths
- **Validation**: Check paths before access

### Configuration:
```yaml
trusted_folders:
  - /home/user/projects
  - /var/www
  - /opt/app
dangerous_patterns:
  - /etc
  - /root
  - /sys
```

### Usage Patterns:
- **Project Isolation**: Restrict to project directories
- **Security**: Prevent system file access
- **Multi-project**: Manage multiple trusted locations
- **Dynamic**: Update trusted folders during session

## 5. Path Management

**Location**: `/vibe/core/paths/`

**Purpose**: Handle file system paths and locations.

### Key Components:

#### Config Paths
- **CONFIG_FILE**: Main configuration file location
- **INSTRUCTIONS_FILE**: Agent instructions file
- **HISTORY_FILE**: Conversation history
- **SESSION_DIR**: Session storage directory

#### Path Utilities
- **Path Validation**: Check path safety
- **Path Resolution**: Convert relative to absolute
- **Path Normalization**: Standardize path formats
- **Path Comparison**: Safe path comparisons

### Usage:
```python
from vibe.core.paths.config_paths import CONFIG_FILE

# Access config file
config_path = CONFIG_FILE.path
if config_path.exists():
    content = config_path.read_text()
```

## 6. Interaction Logging

**Location**: `/vibe/core/interaction_logger.py`

**Purpose**: Comprehensive logging of all interactions.

### Features:

#### Session Logging
- **Complete History**: All messages and context
- **Metadata**: Timestamps, agent info, mode
- **Searchable**: Find specific interactions
- **Exportable**: Save sessions for analysis

#### Message Structure
- **Role**: User or assistant
- **Content**: Message text
- **Timestamp**: When message was sent
- **Context**: Additional metadata
- **Tools Used**: Tool execution records

#### Advanced Logging
- **Filtering**: Search by date, content, tools
- **Analytics**: Usage patterns and statistics
- **Export**: JSON, text, or custom formats
- **Privacy**: Redaction of sensitive information

## 7. Output Formatters

**Location**: `/vibe/core/output_formatters.py`

**Purpose**: Format agent responses in various ways.

### Available Formatters:

#### Text Formatter
- **Format**: Plain text
- **Use Case**: Human-readable output
- **Features**: Colorization, formatting

#### JSON Formatter
- **Format**: Structured JSON
- **Use Case**: Programmatic consumption
- **Features**: Schema validation, pretty printing

#### Compact Formatter
- **Format**: Summary format
- **Use Case**: Quick overviews
- **Features**: Condensed information

#### Custom Formatters
- **Extension**: Create custom formats
- **Integration**: Plug into output system
- **Configuration**: Formatter-specific options

### Usage:
```python
from vibe.core.output_formatters import OutputFormat

# Use different formats
response = agent.process(prompt, output_format=OutputFormat.JSON)
```

## 8. LLM Integration

**Location**: `/vibe/core/llm/`

**Purpose**: Language model integration and management.

### Features:

#### Model Management
- **Multiple Models**: Support for different LLM backends
- **Configuration**: Model-specific settings
- **Fallback**: Backup models if primary fails
- **Performance**: Model performance tracking

#### API Integration
- **Mistral API**: Native Mistral model support
- **OpenAI Compatible**: Support for OpenAI-style APIs
- **Local Models**: Integration with local LLMs
- **Custom Endpoints**: Configure custom API endpoints

#### Token Management
- **Usage Tracking**: Monitor token consumption
- **Cost Estimation**: Calculate API costs
- **Limits**: Set usage limits
- **Optimization**: Reduce token usage

## 9. System Prompt Management

**Location**: `/vibe/core/system_prompt.py`

**Purpose**: Manage the core system prompts that define agent behavior.

### Features:

#### Prompt Selection
- **Multiple Prompts**: Different prompts for different scenarios
- **Dynamic Loading**: Load prompts at runtime
- **Customization**: Modify prompt behavior
- **Validation**: Ensure prompt integrity

#### Prompt Types
- **CLI Prompt**: Main operational guidelines
- **Compact Prompt**: Conversation summarization
- **Project Context**: Environment awareness
- **Custom Prompts**: User-defined prompts

#### Prompt Engineering
- **Versioning**: Track prompt versions
- **Testing**: Validate prompt effectiveness
- **Optimization**: Improve prompt performance
- **Experimentation**: A/B testing of prompts

## 10. Setup and Onboarding

**Location**: `/vibe/setup/onboarding.py`

**Purpose**: Guide users through initial setup and configuration.

### Features:

#### Onboarding Process
- **API Key Setup**: Configure authentication
- **Configuration**: Set user preferences
- **Environment Check**: Verify system requirements
- **First Run**: Initial configuration setup

#### Setup Options
- **Interactive**: Step-by-step guided setup
- **Automatic**: Default configuration
- **Custom**: Advanced configuration options
- **Validation**: Check configuration integrity

#### Update System
- **Version Checking**: Detect new versions
- **Update Notifications**: Inform users of updates
- **Migration**: Handle configuration updates
- **Changelog**: Display new features

## Advanced Usage Patterns

### Custom Workflows
```python
# Create custom workflow
from vibe.core.workflows import BaseWorkflow

class MyWorkflow(BaseWorkflow):
    def __init__(self, config):
        super().__init__(config)
        self.steps = [
            "analyze_requirements",
            "plan_implementation",
            "execute_changes",
            "verify_results"
        ]
    
    async def execute(self):
        for step in self.steps:
            await self.execute_step(step)
```

### Multi-Agent Collaboration
- **Agent Specialization**: Different agents for different tasks
- **Hand-off**: Pass work between agents
- **Coordination**: Manage multi-agent workflows
- **Conflict Resolution**: Handle differing opinions

### Performance Optimization
- **Caching**: Cache frequent operations
- **Batching**: Group similar operations
- **Parallelism**: Concurrent tool execution
- **Resource Management**: Optimize memory usage

### Security Enhancements
- **Sandboxing**: Isolate operations
- **Validation**: Input/output validation
- **Monitoring**: Activity logging
- **Access Control**: Fine-grained permissions

## Integration with Other Systems

### CI/CD Integration
- **Pipeline Steps**: Add Vibe to build pipelines
- **Automated Reviews**: Code review automation
- **Quality Gates**: Enforce coding standards
- **Reporting**: Generate analysis reports

### IDE Integration
- **Plugin System**: IDE plugin development
- **Editor Integration**: Direct editor access
- **Context Sharing**: Share IDE context
- **Real-time Assistance**: Live coding help

### API Integration
- **REST API**: Expose Vibe as service
- **Webhooks**: Event-driven integration
- **Custom Endpoints**: Extend functionality
- **Authentication**: Secure API access

## Troubleshooting Advanced Features

### Mode Issues
- Verify mode configuration
- Check mode-specific settings
- Review mode transition logic
- Test with different modes

### Skill Problems
- Check skill loading order
- Verify skill dependencies
- Review skill configuration
- Test skills individually

### Middleware Errors
- Check middleware chain order
- Verify middleware compatibility
- Review middleware logging
- Test with minimal middleware

### Performance Issues
- Monitor resource usage
- Check for memory leaks
- Review caching strategies
- Optimize expensive operations

### Integration Challenges
- Verify API compatibility
- Check authentication settings
- Review error handling
- Test integration points