---
inclusion: always
---

# Complete Git Workflow Requirements

## Branch Creation and Setup

```bash
git checkout main && git pull origin main
git checkout -b TICKET-XXX
mkdir -p tickets/[team_member]/TICKET-XXX/{source_materials,final_deliverables,exploratory_analysis,archive_versions}
```

## Semantic PR Requirements - MANDATORY

**All Pull Requests MUST use Semantic/Conventional Commit format in titles to pass automated checks:**

**Required Format:** `<type>: <description>`

**Common Types:**
- `feat:` - New features or enhancements
- `fix:` - Bug fixes
- `docs:` - Documentation updates
- `refactor:` - Code refactoring without functional changes
- `chore:` - Maintenance, dependencies, tooling
- `test:` - Test additions or modifications
- `ci:` - CI/CD pipeline changes

**Examples:**
- `feat: add Snowflake data object PRP generation commands`
- `fix: resolve duplicate detection logic in QC validation`
- `docs: update data object creation workflow documentation`
- `refactor: simplify QC validation to single file approach`

**Critical:** PRs with non-semantic titles will fail the Semantic PR check and cannot be merged.

## Folder Structure Standards

```
tickets/[team_member]/TICKET-XXX/
├── README.md                    # REQUIRED: Complete documentation with assumptions
├── KIRO.md                      # REQUIRED: Analysis context for future Kiro sessions
├── source_materials/            # Original files and references
├── final_deliverables/          # REQUIRED: Ready-to-deliver outputs (numbered)
│   ├── 1_[description].sql     # Numbered in review order
│   ├── 2_[description].csv     # Easy review progression
│   └── qc_queries/             # Quality control validation
│       ├── 1_record_count_validation.sql
│       └── 2_duplicate_check.sql
├── original_code/               # REQUIRED: When modifying views/tables
├── exploratory_analysis/        # Optional: Working files (consolidated)
└── [ticket_comment].txt         # Final Jira comment
```

## Ticket-Specific KIRO.md Requirements

Each ticket folder MUST include a `KIRO.md` file that captures:

1. **Ticket Objective**: Clear statement of what the ticket aims to accomplish
2. **Technical Approach**: Tools used, query development process, key SQL/code
3. **Data/Domain Insights**: Learnings about the data structure, patterns discovered
4. **Lessons Learned**: Technical gotchas, workarounds, best practices discovered
5. **Relationship to Other Tickets**: Links to related or dependent tickets
6. **Repository Integration**: How this ticket fits into the broader workflow

This file serves as context for future Kiro sessions working on related tickets.

## Closing Procedures

### 1. Final Consolidation Review

- Eliminate unnecessary queries and files
- Consolidate similar scripts into single numbered files
- **DEFAULT: Overwrite** existing files rather than creating new versions
- Run all final queries and self-correct any errors
- Optimize SQL performance and re-test
- Test optimized queries against original results using `diff`
- Keep folder structure minimal and human-friendly

### 2. Documentation Completion

- Comprehensive README.md with business context and ALL assumptions documented
- All deliverables clearly labeled and numbered for review order
- Quality control results documented with specific validation steps
- File organization prioritizing simplicity over complex structure

### 3. Commit and Push

```bash
git add .
git commit -m "TICKET-XXX: [Brief description of solution]"
git push origin TICKET-XXX
```

### 4. Pull Request Creation - SEMANTIC TITLE REQUIRED

```bash
gh pr create --title "feat: TICKET-XXX [semantic description]" \
  --body "**Business Impact:** [Impact summary]

**Deliverables:**
- [List key deliverables]

**Technical Notes:**
- [Any important technical details]

**QC Results:** [Quality control summary]"
```

**CRITICAL:** PR titles MUST follow semantic format: `feat:`, `fix:`, `docs:`, `refactor:`, `chore:`, etc.
Non-semantic titles will fail automated checks and prevent merging.

### 5. Post-Merge Cleanup

- Archive local branch: `git branch -d TICKET-XXX`
- Create Google Drive backup (with permission)
