# Kiro AI Assistant Instructions

## Overview

This document provides instructions for Kiro when working with the data-tickets repository. You have access to several powerful command-line tools that can help solve data analysis tickets and issues.

**IMPORTANT**: 
- Before adding any new information to this document, always scan the entire file to check if the information already exists to avoid duplication.
- Present all information in a concise, clear manner.
- **Read and weigh each part of this document equally** - all sections are important for effective ticket resolution.

## Quick Reference

All detailed instructions are organized in `.kiro/steering/` files that are automatically loaded:

- **project-context.md** - Core philosophy, operating rules, and workflow standards
- **cli-tools.md** - Available CLI tools and their usage
- **git-workflow.md** - Git branching, PR requirements, and folder structure
- **sql-standards.md** - SQL development process and optimization
- **quality-control.md** - QC requirements and validation standards

## Key Principles

1. **Quality Control Everything** - QC is mandatory, not optional
2. **Document All Assumptions** - Enumerate in README.md with reasoning
3. **Update, Don't Sprawl** - Overwrite files rather than creating versions
4. **Organize for Review** - Number files in logical review order
5. **SQL First, Python Second** - Start with SQL for data exploration
6. **Permission Required** - All database modifications need explicit approval

## Getting Started with a Ticket

```bash
# Create branch and folder structure
git checkout main && git pull origin main
git checkout -b TICKET-XXX
mkdir -p tickets/[team_member]/TICKET-XXX/{source_materials,final_deliverables,exploratory_analysis}
```

## Documentation Requirements

Each ticket folder must include:
- **README.md** - Complete documentation with all assumptions
- **KIRO.md** - Analysis context for future Kiro sessions
- **final_deliverables/** - Numbered files ready for review
- **qc_queries/** - Quality control validation scripts

See `.kiro/steering/` files for complete details on all workflows and standards.
