---
inclusion: always
---

# Quality Control Standards and Requirements

## Mandatory Quality Control Process

**EVERY finalized query MUST have QC and optimization as explicit todo items:**

### Todo List Requirements for Query Development

When finalizing any query, ALWAYS add these todo items:
1. "Run and debug finalized query - fix any errors"
2. "Execute quality control checks and self-correct issues"
3. "Optimize query for performance and re-test"
4. "Validate data quality and record counts"

For queries becoming database objects: "Test extensively as base for view/table"
If data structure is unclear: "Clarify data structure requirements with user"

### QC Validation Requirements

QC validation must include:

#### 1. Filter Verification
Validate all WHERE clauses and schema filters

```sql
-- Example QC query
SELECT 'Schema Filter Check' as check_type,
       schema_name, 
       COUNT(*) as record_count
FROM target_table 
GROUP BY schema_name;
```

#### 2. Duplicate Detection
Check for and explain any duplicate records

```sql
-- Duplicate check example
SELECT loan_id, COUNT(*) as duplicate_count
FROM results_table
GROUP BY loan_id
HAVING COUNT(*) > 1;
```

#### 3. Business Logic Validation
Verify calculated fields and business rules

#### 4. Record Count Reconciliation
Compare input vs output record counts

#### 5. Join Validation
Verify join conditions and unmatched records

#### 6. Data Structure Verification
Confirm understanding of tables and relationships

## Pre-Delivery Checklist

- [ ] **Quality Control**: All QC scripts executed and documented in numbered qc_queries/ folder
- [ ] **Assumption Documentation**: All assumptions enumerated in README.md with reasoning
- [ ] **File Organization**: All deliverables numbered for logical review progression
- [ ] **SQL Optimization**: Queries tested and optimized for performance
- [ ] **Data Validation**: Record counts, filters, and business logic verified
- [ ] **File Consolidation**: Updated existing files rather than creating new versions
- [ ] **Documentation**: Complete README.md with business context and methodology

## Self-Review Process

1. **Code Quality**: Eliminate unnecessary CTEs, optimize joins, simplify logic
2. **Performance Testing**: Measure execution times, compare optimized vs original
3. **Result Validation**: Use `diff` to ensure optimized queries match original results
4. **Documentation Review**: Ensure README.md tells complete story
5. **Final Consolidation**: Remove redundant files and queries

## Quality Gates

- **SQL must be tested** with validation queries
- **Results must be identical** when comparing optimized vs original
- **Performance must be measured** and documented where applicable
- **Documentation must be complete** for handoff
