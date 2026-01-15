# Mistral Vibe CLI - Core Prompts Documentation

## Overview

The Mistral Vibe CLI uses a system of core prompts that define the agent's behavior, capabilities, and interaction patterns. These prompts are the foundation of how the agent understands and responds to user requests.

## 1. CLI Prompt (cli.md)

**Location**: `/vibe/core/prompts/cli.md`

**Purpose**: Defines the agent's role, capabilities, and operational guidelines.

### Key Features:
- **Agent Identity**: "Mistral Vibe, a CLI coding-agent built by Mistral AI"
- **Powered by**: Devstral family of models
- **Primary Function**: Natural language interaction with local codebase

### Capabilities:
- Receive user prompts, project context, and files
- Send responses and emit function calls
- Apply patches and run commands based on user approvals
- Use available tools when helpful

### Operational Guidelines:
- **Tool Selection**: Check if relevant tools are available
- **Parameter Handling**: Ensure required parameters are provided or can be inferred
- **User Input**: Ask user to supply values if tools/parameters are missing
- **Execution**: Proceed with tool calls when requirements are met

### Behavior Patterns:
- **Agentic Assistance**: Break down long tasks into steps
- **Error Handling**: Explain limitations and request more information when needed
- **Tool Priority**: Always try hardest to use tools to answer requests

## 2. Compact Prompt (compact.md)

**Location**: `/vibe/core/prompts/compact.md`

**Purpose**: Create comprehensive conversation summaries for context continuity.

### Structure Requirements:

#### 1. User's Primary Goals and Intent
- Capture ALL explicit requests and objectives
- Preserve exact priorities and constraints

#### 2. Conversation Timeline and Progress
- Chronological documentation of key phases
- Initial requests and resolutions
- Major decisions and their rationale
- Problems encountered and solutions applied
- Current state of work

#### 3. Technical Context and Decisions
- Technologies, frameworks, and tools in use
- Architectural patterns and design decisions
- Key technical constraints or requirements
- Important code patterns or conventions

#### 4. Files and Code Changes
- Full file paths/names
- Purpose and importance of each file
- Specific changes made (with key code snippets)
- Current state of each file

#### 5. Active Work and Last Actions
- Specific task or problem being addressed
- Last completed action
- Any partial work or mid-implementation state
- Relevant code snippets from recent work

#### 6. Unresolved Issues and Pending Tasks
- Errors or issues requiring attention
- Tasks requested but not yet started
- Decisions waiting for user input

#### 7. Immediate Next Step
- Specific next action based on:
  - User's most recent request
  - Current state of implementation
  - Any ongoing work that was interrupted

### Key Requirements:
- Be precise with technical details, file names, and code
- Include enough detail for seamless continuation
- No additional commentary or meta-discussion
- Focus on actionable information

## 3. Project Context Prompt (project_context.md)

**Location**: `/vibe/core/prompts/project_context.md`

**Purpose**: Display project structure information at the start of conversations.

### Components:
- **directoryStructure**: Snapshot of project file structure
- **large_repo_warning**: Warning for large repositories
- **structure**: Actual directory structure display
- **Absolute path**: Current working directory path
- **gitStatus**: Git repository status information

### Characteristics:
- Static snapshot that doesn't update during conversation
- Skips .gitignore patterns
- Provides initial context for navigation

## 4. Dangerous Directory Prompt (dangerous_directory.md)

**Location**: `/vibe/core/prompts/dangerous_directory.md`

**Purpose**: Handle access to sensitive or dangerous directories.

### Typical Content:
- Warnings about accessing system directories
- Security considerations
- Permission requirements
- Guidelines for safe operation

## 5. Tests Prompt (tests.md)

**Location**: `/vibe/core/prompts/tests.md`

**Purpose**: Define testing scenarios and methodologies.

### Typical Content:
- Test case formats
- Testing best practices
- Example test scenarios
- Quality assurance guidelines

## Usage Patterns

These core prompts work together to:
1. **Define Behavior**: CLI prompt sets the operational guidelines
2. **Maintain Context**: Compact prompt ensures continuity between sessions
3. **Provide Awareness**: Project context gives spatial orientation
4. **Ensure Safety**: Dangerous directory prompt prevents accidents
5. **Quality Assurance**: Tests prompt maintains code quality

## Best Practices

- **Prompt Selection**: Use the appropriate prompt for each scenario
- **Context Preservation**: Always include relevant context from compact summaries
- **Safety First**: Respect dangerous directory warnings
- **Testing**: Follow test patterns for quality assurance
- **Continuity**: Use project context to understand file locations