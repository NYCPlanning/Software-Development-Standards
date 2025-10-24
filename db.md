# SQL Server Standards
## Naming Conventions
	· Tables: PascalCase, plural nouns (Customers, OrderDetails)
	· Columns: PascalCase, singular nouns (FirstName, OrderDate)
	· Primary Keys: Id or TableNameId(CustomerId)
	· Foreign Keys: FK_ChildTable_ParentTable_ColumnName
	· Indexes: IX_TableName_ColumnName(non-clustered), CIX_TableName_ColumnName(clustered)
	· Stored Procedures: usp_VerbNoun(usp_GetCustomerOrders, usp_UpdateInventory)
	· Functions: fn_VerbNoun (scalar), tvf_VerbNoun (table-valued)
## Schema Design
	· Use appropriate data types (avoid NVARCHAR(MAX) unless necessary, prefer NVARCHAR(n)).
	· Always define NOT NULL or NULL explicitly.
	· Use DATETIME2 instead of DATETIME for new columns.
	· Include audit columns where appropriate: CreatedDate, CreatedBy, ModifiedDate, ModifiedBy.
	· Use surrogate keys (identity columns) for primary keys.

## Query Writing
-- Use clear formatting and indentation
SELECT 
    c.CustomerId,
    c.FirstName,
    c.LastName,
    c.Email,
    COUNT(o.OrderId) AS TotalOrders
FROM Customers c
LEFT JOIN Orders o ON c.CustomerId = o.CustomerId
WHERE c.IsActive = 1
    AND c.CreatedDate >= '2024-01-01'
GROUP BY c.CustomerId, c.FirstName, c.LastName, c.Email
ORDER BY TotalOrders DESC;
 
-- Always use schema prefix
SELECT * FROM dbo.Customers; -- Good
SELECT * FROM Customers;     -- Bad
 
-- Avoid SELECT *, specify needed columns
-- Use parameterized queries to prevent SQL injection
-- Use EXISTS instead of COUNT(*) for existence checks

## Stored Procedures
	· Include error handling with TRY...CATCH blocks.
	· Use transactions for multi-statement operations.
	· Return consistent result sets and error codes.
	· Document parameters and purpose in header comments.

## Indexing
	· Create indexes on foreign keys and frequently queried columns.
	· Monitor query plans and missing index recommendations.
	· Include columns in indexes when beneficial (covering indexes).
	· Be cautious of over-indexing - impacts insert/update performance.

## Performance
	· Avoid cursors; use set-based operations.
	· Use WITH (NOLOCK) carefully and only for reporting queries where dirty reads are acceptable.
	· Avoid functions in WHERE clauses on large tables.
	· Use table variables for small datasets, temp tables for larger ones.

