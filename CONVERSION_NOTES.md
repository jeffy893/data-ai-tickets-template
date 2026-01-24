# Claude to Kiro Conversion Notes

## What Was Changed

This repository has been converted from Claude Code context to Kiro AI Assistant context. Here's what changed:

### File Structure Changes

**Created:**
- `.kiro/steering/` - New directory for Kiro context files (auto-loaded)
  - `project-context.md` - Core philosophy and operating rules
  - `cli-tools.md` - CLI tool reference
  - `git-workflow.md` - Git and PR standards
  - `sql-standards.md` - SQL development guide
  - `quality-control.md` - QC requirements
- `KIRO.md` - Quick reference guide (replaces CLAUDE.md)
- `CLI_SETUP_GUIDE.md` - Comprehensive CLI tool installation guide

**Preserved:**
- `.claude/` directory - Kept for reference (agents and commands)
- `CLAUDE.md` - Original file preserved for comparison
- All documentation in `documentation/`
- All video examples in `videos/`
- All ticket templates and structures

**Updated:**
- `README.md` - References changed from Claude to Kiro
- Folder structure examples updated to include `.kiro/` directory

### Key Differences: Claude vs Kiro

#### Context Management

**Claude Code:**
- Single large `CLAUDE.md` file with all instructions
- Custom agents in `.claude/agents/`
- Custom commands in `.claude/commands/`
- Settings in `.claude/settings.json`

**Kiro:**
- Modular steering files in `.kiro/steering/` (auto-loaded)
- Shorter `KIRO.md` as quick reference
- Hooks system for automation (instead of commands)
- Context organized by topic for easier maintenance

#### Advantages of Kiro Approach

1. **Modular Context**: Steering files are loaded automatically and can be organized by topic
2. **Easier Maintenance**: Update individual steering files instead of one large document
3. **Better Organization**: Related instructions grouped together
4. **Selective Loading**: Can control which steering files load with frontmatter
5. **Cleaner Structure**: Separation of concerns across multiple files

### What Stayed the Same

The core workflows, standards, and best practices remain identical:

- Git workflow and semantic PR requirements
- SQL development standards
- Quality control processes
- CLI tool usage patterns
- Folder structure conventions
- Documentation requirements

### Migration Path

If you're migrating from Claude Code to Kiro:

1. **Keep your `.claude/` directory** for reference
2. **Create `.kiro/steering/` directory** with modular context files
3. **Create `KIRO.md`** as a quick reference guide
4. **Update references** in README and documentation
5. **Test workflows** to ensure everything works as expected

### Using This Repository

**With Kiro:**
- Kiro automatically loads all files in `.kiro/steering/`
- Reference `KIRO.md` for quick guidance
- All workflows and standards work the same way

**With Claude Code:**
- Use the original `CLAUDE.md` file
- Reference `.claude/agents/` and `.claude/commands/`
- All workflows and standards work the same way

Both AI assistants can work with this repository structure!

## CLI Tools Required

See `CLI_SETUP_GUIDE.md` for detailed installation and configuration instructions for:

1. **Snowflake CLI** (`snow`) - Database queries and management
2. **Atlassian CLI** (`acli`) - Jira ticket management
3. **GitHub CLI** (`gh`) - Repository and PR management
4. **Databricks CLI** (`databricks`) - Job orchestration
5. **AWS CLI** (`aws`) - Cloud services management

Plus optional tools for enhanced analysis (tree, jq, bat, ripgrep, etc.)

## Questions?

- Check `KIRO.md` for quick reference
- Review `.kiro/steering/` files for detailed workflows
- See `CLI_SETUP_GUIDE.md` for tool installation
- Explore `videos/` folder for working examples
