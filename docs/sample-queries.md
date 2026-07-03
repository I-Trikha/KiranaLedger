# Sample SQL Queries

## View All Customers

```sql
SELECT * FROM customers;
```

## View All Transactions

```sql
SELECT * FROM transactions;
```

## Outstanding Balances

```sql
SELECT
c.name,
SUM(
CASE
WHEN t.type='credit' THEN t.amount
ELSE -t.amount
END
) AS balance
FROM customers c
LEFT JOIN transactions t
ON c.id=t.customer_id
GROUP BY c.id;
```

## Recent Transactions

```sql
SELECT
c.name,
t.type,
t.amount,
t.date
FROM customers c
JOIN transactions t
ON c.id=t.customer_id
ORDER BY t.date DESC;
```

## Overdue Payments

```sql
SELECT
c.name,
t.amount,
t.due_date
FROM transactions t
JOIN customers c
ON c.id=t.customer_id
WHERE t.type='credit'
AND t.due_date < DATE('now');
```
