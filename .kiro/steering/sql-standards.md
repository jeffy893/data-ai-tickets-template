---
inclusion: always
---

# SQL Development Standards

## Development Process

1. **Investigate structures**: Use `DESCRIBE` or `SELECT * LIMIT 5`
2. **Build incrementally**: Start basic, add joins/filters
3. **Use appropriate filters**: Apply date filters, limits during exploration
4. **Run and self-correct**: ALWAYS execute development queries and fix any errors
5. **Test base queries**: Queries that will become views/tables must be thoroughly tested
6. **Present final queries**: Show completed, tested queries after exploration
7. **Document logic**: Explain joins, filters, business logic concisely

## Safety Rules

- Simple SELECT operations permitted without approval
- **NEVER** run ALTER, CREATE, DROP, INSERT, UPDATE, DELETE without permission
- Use LIMIT clauses during exploration
- Apply reasonable date filters

## Standards and Conventions

- **Parameterize values** as variables at script top
- **Document variables** with clear comments
- **Include comprehensive commenting** explaining business logic
- **Always output CSV format** using `--format=csv`
- **ALWAYS include column headers** in CSV outputs
- **Use CAST()** for data type conversions when joining
- **Handle missing columns** gracefully using alternatives
- **No hardcoding test results**: do not hardcode things like "pass", "fail", or any other strings for query tests. Not all tests will have a pass/fail result, but if they do, make sure you use conditional logic to get the end result.
- **SQL Test Formatting**: Place test titles (`--X.Y: Test Description`) directly above queries with no separator lines

## Query Optimization

Always evaluate queries for efficiency before finalizing:

1. **Structure Review**: Eliminate unnecessary CTEs, optimize joins, simplify logic
2. **Testing Protocol**: Test optimized queries against original results using `diff`
3. **Performance Focus**: Write queries as efficiently as possible within the design constraints
4. **Large Dataset Handling**: Apply sampling for exploration when working with large datasets
5. **Quality Gates**: SQL must be tested, results identical, focus on clean efficient code

## Performance Workaround for Long-Running QC Queries

When QC queries take a long time to execute (e.g., comparing large views/tables), use temporary tables to materialize the data once:

```sql
-- Use larger warehouse for better performance
use warehouse BUSINESS_INTELLIGENCE_LARGE;

-- Create temp tables to materialize data once
CREATE OR REPLACE TEMP TABLE dev_data_temp AS
SELECT * FROM BUSINESS_INTELLIGENCE_DEV.REPORTING.VW_SOME_VIEW;

CREATE OR REPLACE TEMP TABLE prod_data_temp AS
SELECT * FROM BUSINESS_INTELLIGENCE.REPORTING.VW_SOME_VIEW;

-- Run all QC tests against temp tables instead of re-querying views
SELECT COUNT(*) FROM dev_data_temp;
SELECT COUNT(*) FROM prod_data_temp;
-- Additional QC tests...
```

This approach:
- Materializes expensive views once at the start
- Allows multiple QC tests without re-executing the underlying view queries
- Significantly improves QC script performance for complex views
