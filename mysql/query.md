#### Get the latest record for employee based employee flag.
```sql
SELECT
    employees.id,
    employees.employee_type_id,
    employees.rank_id,
    employees.name,
    from_branchs.name AS from_branch,
    to_branchs.name AS to_branch,
    records.from_branch_id,
    records.to_branch_id,
    records.movement_date
FROM
    employees
JOIN records ON records.employee_id = employees.id
JOIN branchs AS from_branchs ON records.from_branch_id = from_branchs.id
JOIN branchs AS to_branchs ON records.to_branch_id = to_branchs.id
WHERE
    records.xy_in = 1 AND employees.xy_in = 1
ORDER BY
    records.created_at DESC;
```
