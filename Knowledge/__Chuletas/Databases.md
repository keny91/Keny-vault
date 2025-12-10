# ✅ **Most Common Database Operations**

We’ll cover:

1. **CREATE** (create databases, tables, users)
```
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(200) UNIQUE,
    created_at TIMESTAMP DEFAULT NOW()
);
```

2. **SELECT** (read data)

```
SELECT id, name, email
FROM customers
WHERE name LIKE 'Luis%';

```
2. **INSERT** (add data)

```
INSERT INTO customers (name, email)
VALUES ('Luis Herranz', 'luis@example.com');

```

2. **UPDATE** (modify data)
    
```
UPDATE customers
SET email = 'newmail@example.com'
WHERE id = 42;

```

2. **DELETE** (remove data)

```
DELETE FROM customers
WHERE id = 42;
```

2. **JOIN** (combine data from multiple tables)
    
```
SELECT c.name, o.total
FROM customers c
JOIN orders o ON c.id = o.customer_id;

```

#### Use cases

- Combine customers with their orders
    
- Link invoices with payments
    
- Link users to their roles
    

#### Most common join types:

- **INNER JOIN** → Only matching rows
    
- **LEFT JOIN** → Everything from left table + matches
    
- **RIGHT JOIN** → Opposite of left
    
- **FULL OUTER JOIN** → All rows from both
    
- **CROSS JOIN** → Cartesian product

2. **WHERE** (filtering)
    
```
SELECT *
FROM orders
WHERE total > 50 AND status = 'completed';

```

2. **ORDER BY / LIMIT** (sorting & pagination)
    
```
SELECT name, created_at
FROM customers
ORDER BY created_at DESC
LIMIT 10;

```

2. **GROUP BY / HAVING** (aggregations)
    
```
SELECT customer_id, SUM(total) as total_spent
FROM orders
GROUP BY customer_id
HAVING SUM(total) > 500;

```

2. **ALTER** (modify structure)
    
```
# Add a column
ALTER TABLE customers
ADD COLUMN phone VARCHAR(20);
----------
# Modify a column
ALTER TABLE customers
MODIFY COLUMN email VARCHAR(300);

```

2. **DROP** (delete structure) Delete tables, databases, columns
    
```
DROP TABLE customers_backup;
```

2. **TRANSACTIONS** (BEGIN / COMMIT / ROLLBACK)
    
    Maintain **ACID**
    
```
BEGIN;

UPDATE accounts SET balance = balance - 50 WHERE id = 1;
UPDATE accounts SET balance = balance + 50 WHERE id = 2;

COMMIT;
---------
# ROLLBACK ON ERROR
ROLLBACK;


```


Let’s go one by one.