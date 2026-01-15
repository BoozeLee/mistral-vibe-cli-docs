# Mistral Vibe CLI - Built-in Tools Documentation

## Overview

The Mistral Vibe CLI provides a comprehensive set of built-in tools that enable powerful code manipulation, file operations, and task management. These tools are designed with safety, efficiency, and best practices in mind.

## 1. bash Tool

**Location**: `/vibe/core/tools/builtins/prompts/bash.md`

**Purpose**: Execute one-off shell commands.

### Key Characteristics:
- **Stateless**: Each command runs independently in a fresh environment
- **Priority**: Use dedicated tools when available instead of bash commands

### Appropriate Uses:
- **System Information**: `pwd`, `whoami`, `date`, `uname -a`
- **Directory Listings**: `ls -la`, `tree` (if available)
- **Git Operations**: `git status`, `git log --oneline -10`, `git diff`
- **Process Info**: `ps aux | grep process`, `top -n 1`
- **Network Checks**: `ping -c 1 google.com`, `curl -I https://example.com`
- **Package Management**: `pip list`, `npm list`
- **Environment Checks**: `env | grep VAR`, `which python`
- **File Metadata**: `stat filename`, `file filename`, `wc -l filename`

### File Operations - DO NOT USE:
Instead of bash commands, use dedicated tools:
- `cat filename` → `read_file(path="filename")`
- `head -n 20 filename` → `read_file(path="filename", limit=20)`
- `tail -n 20 filename` → `read_file(path="filename", offset=<line_number>, limit=20)`
- `sed -n '100,200p' filename` → `read_file(path="filename", offset=99, limit=101)`
- `less`, `more`, `vim`, `nano` → `read_file` with offset/limit
- `echo "content" > file` → `write_file(path="file", content="content")`
- `echo "content" >> file` → Read first, then `write_file` with overwrite=true

### Search Operations - DO NOT USE:
Instead of bash commands, use dedicated tools:
- `grep -r "pattern" .` → `grep(pattern="pattern", path=".")`
- `find . -name "*.py"` → `bash("ls -la")` or `grep` with appropriate pattern
- `ag`, `ack`, `rg` commands → `grep` tool
- `locate` → `grep` tool

### File Modification - DO NOT USE:
Instead of bash commands, use dedicated tools:
- `sed -i 's/old/new/g' file` → `search_replace` tool
- `awk` for file editing → `search_replace` tool
- Any in-place file editing → `search_replace` tool

### Best Practices:
- **Efficiency**: Use `read_file` with limit/offset for large files
- **Safety**: Avoid destructive operations
- **Tool Priority**: Always prefer dedicated tools over bash when available

## 2. grep Tool

**Location**: `/vibe/core/tools/builtins/prompts/grep.md`

**Purpose**: Recursively search for regular expression patterns in files.

### Key Features:
- **Speed**: Very fast pattern searching
- **Smart Filtering**: Automatically ignores files like .pyc, .venv directories
- **Use Cases**: Find function definitions, variable usage, error messages

### Usage:
```python
grep(pattern="TODO", path=".")
grep(pattern="import.*requests", path="src/")
```

### Best Practices:
- Use specific patterns to reduce false positives
- Combine with path filtering for targeted searches
- Respect .gitignore patterns by default

## 3. read_file Tool

**Location**: `/vibe/core/tools/builtins/prompts/read_file.md`

**Purpose**: Read file content safely with chunking support.

### Key Features:
- **Safety**: Handles large files with byte limits
- **Chunking**: Read specific line ranges efficiently
- **Navigation**: Offset and limit parameters for large files

### Usage:
```python
# Read entire file
read_file(path="filename.txt")

# Read first 1000 lines
read_file(path="large_file.txt", limit=1000)

# Read lines 1000-2000
read_file(path="large_file.txt", offset=1000, limit=1000)
```

### Strategy for Large Files:
1. Read first chunk with limit (e.g., 1000 lines)
2. Check if `was_truncated: true`
3. Read next chunk with appropriate offset

### Best Practices:
- Always check `was_truncated` for large files
- Use offset/limit for efficient navigation
- Prefer over bash commands for file reading

## 4. search_replace Tool

**Location**: `/vibe/core/tools/builtins/prompts/search_replace.md`

**Purpose**: Make targeted changes to files using SEARCH/REPLACE blocks.

### Key Features:
- **Precision**: Exact text matching required
- **Safety**: Multiple search/replace blocks in one operation
- **Validation**: Detailed error messages with context

### Format:
```python
search_replace(
    file_path="filename.py",
    content="""
<<<<<<< SEARCH
def old_function():
    return "old value"
=======
def new_function():
    return "new value"
>>>>>>> REPLACE
"""
)
```

### Requirements:
- SEARCH text must match EXACTLY (whitespace, indentation, line endings)
- SEARCH text must appear exactly once in file
- Use at least 5 equals signs (=====) between SEARCH and REPLACE
- Each block applied in order (later blocks see earlier changes)

### Best Practices:
- Always read file first to understand current content
- Use precise search patterns to avoid accidental matches
- Test changes on small files first
- Consider backup before major changes

## 5. todo Tool

**Location**: `/vibe/core/tools/builtins/prompts/todo.md`

**Purpose**: Manage task lists for complex workflows.

### Key Features:
- **Task Structure**: id, content, status, priority
- **Status Options**: pending, in_progress, completed, cancelled
- **Priority Levels**: low, medium, high

### Usage:
```python
# Read current todos
todo(action="read")

# Update todos (must provide complete list)
todo(action="write", todos=[
    {
        "id": "1",
        "content": "Implement feature X",
        "status": "in_progress",
        "priority": "high"
    }
])
```

### Best Practices:
- **When to Use**:
  - Complex multi-step tasks (3+ steps)
  - Non-trivial tasks requiring planning
  - Multiple user requests
  - Tracking ongoing work

- **When to Skip**:
  - Single, straightforward tasks
  - Trivial operations (< 3 steps)
  - Purely conversational requests

- **Status Management**:
  - Only ONE task should be `in_progress` at a time
  - Mark tasks `in_progress` BEFORE starting
  - Mark `completed` IMMEDIATELY after finishing
  - Keep `in_progress` if blocked

- **Task Organization**:
  - Create specific, actionable items
  - Break complex tasks into manageable steps
  - Use clear, descriptive names
  - Remove irrelevant tasks entirely

## 6. write_file Tool

**Location**: `/vibe/core/tools/builtins/prompts/write_file.md`

**Purpose**: Write content to files with safety features.

### Key Features:
- **Safety**: Fails if file exists (unless overwrite=true)
- **Convenience**: Creates parent directories automatically
- **Flexibility**: Overwrite protection by default

### Usage:
```python
# Create new file
write_file(
    path="new_file.py",
    content="def hello():\n    return 'Hello World'"
)

# Overwrite existing file
write_file(
    path="existing.py",
    content="# Updated content",
    overwrite=True
)
```

### Safety Rules:
- **Default Behavior**: Fails if file exists to prevent data loss
- **Overwrite Requirement**: Must set `overwrite: true` explicitly
- **Directory Creation**: Parent directories created automatically

### Best Practices:
- **ALWAYS** read file first before overwriting
- **PREFER** `search_replace` for editing existing files
- **NEVER** write new files unless explicitly required
- **NEVER** proactively create documentation files
- **AVOID** emojis unless explicitly requested
- **BACKUP** important files before overwriting

## Tool Selection Guide

| Task | Recommended Tool | Alternative | Notes |
|------|------------------|-------------|-------|
| Read file | `read_file` | `bash("cat file")` | Always prefer `read_file` |
| Search patterns | `grep` | `bash("grep pattern")` | Use `grep` for better filtering |
| Edit file | `search_replace` | `bash("sed -i")` | Much safer and precise |
| Create file | `write_file` | `bash("echo > file")` | Use `write_file` for safety |
| Complex tasks | `todo` | Manual tracking | Essential for multi-step workflows |
| System info | `bash` | N/A | Appropriate use case |
| Git operations | `bash` | N/A | Appropriate use case |

## Safety Guidelines

1. **Always prefer dedicated tools** over bash commands
2. **Read before write** - understand file content first
3. **Use search_replace** for precise editing
4. **Manage tasks** with todo tool for complex workflows
5. **Check truncation** when reading large files
6. **Backup important files** before major changes
7. **Follow tool-specific** safety rules and best practices