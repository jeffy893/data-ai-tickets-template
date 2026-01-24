---
inclusion: always
---

# Available CLI Tools

## Core Platform Tools

### Snowflake CLI (`snow`)
**Database queries and management** | [Docs](https://docs.snowflake.com/en/developer-guide/snowflake-cli/index)

- Authentication: Duo Security (15-minute lockout warning)
- Query execution: `snow sql -q "SELECT * FROM table" --format csv`
- Object management: `snow connection list`, `snow warehouse list`
- Schema operations: `snow sql -q "DESCRIBE TABLE schema.table"`

### Jira CLI (`acli`)
**Ticket tracking and workflow automation** | [Docs](https://developer.atlassian.com/cloud/acli/reference/commands/)

- View tickets: `acli jira workitem view TICKET-KEY`
- List projects: `acli jira project list --limit 10`
- Create tickets: Use file input to avoid labels field issues (**<200 words max**)
- Transition tickets: `acli jira workitem transition --key "PROJECT-XXX" --status "Done"`
- Comments: `acli jira workitem comment --key "PROJECT-XXX" --body "Comment text"` (**<100 words max**)

### GitHub CLI (`gh`)
**Repository and issue management** | [Docs](https://cli.github.com/manual/)

- Create PRs: `gh pr create --title "PR title" --body "PR description"` (**<200 words max**)
- Issue management: `gh issue create`, `gh issue list`

### Databricks CLI (`databricks`)
**Job orchestration and data platform management** | [Docs](https://docs.databricks.com/dev-tools/cli/index.html)

- Profile: `DEFAULT` (no `--profile` flag needed)
- Workspace management: `databricks workspace list /`
- Job management: `databricks jobs list`, `databricks jobs create --json-file config.json`
- File operations: `databricks fs cp local_file.py dbfs:/path/`
- Job execution: `databricks jobs run-now --job-id <id>`

### AWS CLI (`aws`)
**Cloud services management (S3, Athena, and more)** | [Docs](https://docs.aws.amazon.com/cli/)

- S3 operations: `aws s3 ls s3://bucket-name/`, `aws s3 cp file.csv s3://bucket-name/`
- Athena queries: `aws athena start-query-execution --query-string "SELECT * FROM table" --result-configuration OutputLocation=s3://bucket/results/`
- Query results: `aws athena get-query-results --query-execution-id <id>`
- List databases: `aws athena list-databases --catalog-name AwsDataCatalog`

## Enhanced Analysis Tools

- **tree** - Directory visualization: `tree -L 2 tickets/`
- **jq** - JSON processing: `snow sql -q "query" --format json | jq '.data[]'`
- **bat** - Syntax highlighting: `bat final_deliverables/query.sql`
- **ripgrep (rg)** - Fast search: `rg "pattern" tickets/`
- **fd** - File finder: `fd -e sql final_deliverables/`
- **fzf** - Interactive selection: `git log --oneline | fzf`

## Data Science and Analysis Tools

- **csvkit** - CSV manipulation: `csvcut`, `csvsql`, `csvstat`, `csvgrep`
- **DuckDB** - Fast analytical SQL: `duckdb -c "SELECT * FROM 'data.csv'"`
- **Miller (mlr)** - Data transformation: `mlr --csv cut -f name,amount data.csv`
- **yq** - YAML/JSON processor: `yq '.field' file.yaml`
- **xsv** - Fast CSV toolkit: `xsv stats data.csv`
- **hyperfine** - Benchmarking: `hyperfine "snow sql -q 'SELECT COUNT(*)'"`
- **JupyterLab** - Interactive notebooks: `jupyter lab`
- **Python packages** - pandas, numpy, matplotlib, seaborn, plotly, snowflake-connector-python, sqlalchemy, openpyxl, xlsxwriter, requests, beautifulsoup4, scipy, scikit-learn
