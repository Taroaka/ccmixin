# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Claude Code Mixin OSS** is a tool that enables Claude Code to intelligently merge multiple Claude Code-focused OSS repositories into a single, best-practices compilation.

### Purpose

GitHub hosts many excellent Claude Code OSS projects (slash commands, CLAUDE.md files, hooks, etc.). However, users often want to combine the best features from multiple projects. This tool allows Claude Code itself to:

1. Analyze multiple OSS repositories
2. Understand their structure and content
3. Intelligently merge them into a unified output
4. Resolve conflicts by consulting the user

### Not a Script-Based Tool

**Important**: This tool does NOT use scripts or automated merging logic. Instead:
- The `/ccmixin` command provides detailed instructions to Claude Code
- Claude Code reads and understands the content of multiple repositories
- Claude Code makes intelligent decisions about how to merge files
- For `CLAUDE.md`, `README.md`, and `settings.json`, Claude Code creates semantically unified versions

## Architecture

### Directory Structure

```
claude-code-docs/
├── repos/                    # User clones OSS repositories here
│   ├── awesome-claude-skills/
│   ├── claude-best-practices/
│   └── README.md            # Instructions for cloning
├── ccmixin/                 # Generated output (gitignored)
│   ├── CLAUDE.md           # Merged version
│   ├── README.md           # Merged version
│   ├── .claude/
│   │   ├── commands/       # Merged slash commands
│   │   └── settings.json   # Merged settings
│   └── scripts/            # Merged scripts
├── docs/                    # Claude Code official documentation (reference)
│   ├── hooks.md
│   ├── mcp.md
│   └── ...
├── .claude/
│   └── commands/
│       └── ccmixin.md      # The /ccmixin command definition
├── CLAUDE.md               # This file
├── README.md               # User-facing documentation
└── TODO.md                 # Implementation checklist
```

### Key Components

#### 1. `/ccmixin` Command (`.claude/commands/ccmixin.md`)

This is the core of the tool. It's a detailed prompt that instructs Claude Code to:
- Detect repositories in `repos/`
- Analyze directory structures
- Compare files across repositories
- Identify conflicts and unique files
- Merge intelligently (not just concatenate)
- Prompt user for conflict resolution
- Generate output in `ccmixin/`

#### 2. `repos/` Directory

This is where users clone the OSS repositories they want to merge. Requirements:
- At least 2 repositories
- Can handle 3+ repositories
- `.git/`, `node_modules/`, etc. are automatically ignored

#### 3. `ccmixin/` Output Directory

The generated output containing:
- Merged `CLAUDE.md` (semantically unified)
- Merged `README.md` (combined sections)
- Merged `.claude/settings.json` (hooks arrays unified)
- Slash commands (with conflict resolution)
- All unique files from both repositories

#### 4. `docs/` Reference Documentation

Contains Claude Code official documentation for reference. This helps Claude Code understand:
- How hooks work
- How MCP works
- How skills work
- Best practices

**This folder is kept from the previous project** as it provides valuable context.

## Development Workflow

### Testing `/ccmixin`

```bash
# 1. Clone two test repositories into repos/
cd repos/
git clone <test-repo-1>
git clone <test-repo-2>
cd ..

# 2. Run the command in Claude Code CLI
/ccmixin

# 3. Check the output
ls -la ccmixin/
cat ccmixin/CLAUDE.md
cat ccmixin/README.md
```

### Understanding the Merge Process

When you run `/ccmixin`, Claude Code follows this process:

1. **Detection Phase**
   - Scans `repos/` for subdirectories
   - Validates that at least 2 repos exist
   - Checks for existing `ccmixin/` folder

2. **Analysis Phase**
   - Reads all files from each repository
   - Categorizes files (settings, commands, docs, scripts, etc.)
   - Identifies conflicts (same filename, different content)

3. **Conflict Resolution Phase**
   - For `CLAUDE.md`: Reads both, understands content, creates unified version
   - For `README.md`: Merges sections intelligently
   - For `settings.json`: Combines hooks arrays, preserves structure
   - For slash commands: Asks user which to use if names conflict
   - For other files: Asks user or keeps both (renamed)

4. **Generation Phase**
   - Creates `ccmixin/` directory
   - Writes merged files
   - Copies unique files
   - Preserves directory structure

5. **Report Phase**
   - Shows statistics (files merged, copied, skipped)
   - Provides next steps

## File Merging Strategies

### Intelligent Merging (CLAUDE.md, README.md)

Claude Code doesn't just concatenate these files. Instead:

**For CLAUDE.md:**
- Identifies common sections (Project Overview, Architecture, etc.)
- Merges section content intelligently
- Removes duplicate information
- Prioritizes more detailed/useful information
- Creates a cohesive, well-structured document

**For README.md:**
- Merges project descriptions
- Combines installation instructions
- Unifies usage examples
- Preserves important badges/links
- Creates a professional, unified README

### Array Merging (settings.json)

For `.claude/settings.json`:
```json
{
  "hooks": {
    "PreToolUse": [
      /* Hooks from Repo1 */
      /* + Hooks from Repo2 */
      /* Duplicates removed */
    ],
    "PostToolUse": [
      /* Combined similarly */
    ]
  }
  /* Other settings merged with conflict detection */
}
```

### Conflict Resolution (Slash Commands)

When both repos have `/commit.md`:
- Claude Code asks user which to use
- Options: Use Repo1, Use Repo2, Keep both (rename), Merge both
- User's choice is applied

## Important Implementation Notes

### No Scripts Required

Previous versions of this repository used Python scripts (`fetch_claude_docs.py`) and Bash scripts (`install.sh`). These have been removed because:
- The new approach relies on Claude Code's intelligence
- No automated merging logic is needed
- Claude Code understands context and makes better decisions

### Reference Documentation

The `docs/` folder contains official Claude Code documentation. This is useful because:
- Claude Code can reference it while working
- Helps understand Claude Code concepts (hooks, MCP, etc.)
- Provides examples of best practices

### User Interaction

The `/ccmixin` command uses `AskUserQuestion` tool when:
- Deleting existing `ccmixin/` folder
- Resolving file conflicts
- Choosing between conflicting slash commands
- Handling 3+ repositories

## Testing Philosophy

Before using `/ccmixin` with real repositories:
1. Test with 2 simple repos (minimal conflicts)
2. Test with conflicting slash commands
3. Test with different `CLAUDE.md` structures
4. Test with 3+ repositories
5. Verify merged output is coherent and usable

## Common Scenarios

### Scenario 1: Merging Skills from Two Repos

**Repo1**: `/commit`, `/review`, `/test`
**Repo2**: `/deploy`, `/docs`, `/fix`

**Result**: All 6 commands in `ccmixin/.claude/commands/`

### Scenario 2: Conflicting Commands

**Repo1**: `/commit.md` (simple git commit)
**Repo2**: `/commit.md` (advanced commit with conventional commits)

**Process**: Claude Code asks which to use → User chooses Repo2 → Advanced version is used

### Scenario 3: Different CLAUDE.md Styles

**Repo1**: Detailed architecture documentation
**Repo2**: Coding standards and best practices

**Process**: Claude Code reads both → Creates unified document with both architecture AND best practices

## Future Enhancements

Potential improvements (not yet implemented):
- Support for 3+ repository merging with priority system
- Merge configuration file (specify which repo takes precedence)
- Dry-run mode (preview without creating output)
- Merge history tracking
- GitHub URL input (auto-clone repos)

## Contributing

When contributing to this project:
1. Maintain the philosophy: Claude Code does the intelligent work
2. Update `/ccmixin` command prompts, not scripts
3. Test with real OSS repositories
4. Document any new merging strategies

## Key Files

- `.claude/commands/ccmixin.md` - Core command definition and prompt
- `repos/README.md` - User instructions for cloning repos
- `README.md` - Main project documentation
- `TODO.md` - Implementation checklist
- `docs/` - Claude Code reference documentation (preserved)
