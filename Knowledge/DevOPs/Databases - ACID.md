#databases #acid


#### ACID (Atomicity, Consistency, Isolation, Durability)

ACID is a set of guarantees provided by **transactional** database systems to ensure that operations on data are safe, reliable, and recoverable.

#### **1. Atomicity – “All or Nothing”**

A transaction must be treated as a single unit:

- If **all operations succeed**, the transaction is committed.
    
- If **any operation fails**, the entire transaction is rolled back.
    

**Example:**  
Transferring money between accounts:

- Deduct €100 from A
    
- Add €100 to B  
    If adding to B fails, the deduct from A must also be undone.
    

**How DBs implement it:**

- Write-ahead logs (WAL)
    
- Undo logs
    
- Transactionrollback mechanisms
  
  
#### **2. Consistency – “Valid State → Valid State”**

After the transaction completes, the database must remain in a **valid, rule-abiding state**.  
Consistency rules come from:

- Constraints (unique, foreign keys, check constraints)
    
- Data types
    
- Triggers
    
- Business rules
    

**Example:**  
A transaction cannot violate:

- A product’s stock cannot be negative
    
- A foreign key reference must exist
    

**Important:**  
Consistency is partially the developer’s responsibility — the DB _helps enforce_ rules but application logic defines them.


## **3. Isolation – “Transactions Don’t Interfere“**

While multiple transactions run concurrently, each must behave **as if it’s running alone**.  
Isolation prevents race conditions, dirty reads, lost updates, etc.

### **Isolation Levels (important for interviews!)**

1. **Read Uncommitted** → dirty reads allowed
    
2. **Read Committed** → no dirty reads
    
3. **Repeatable Read** → no dirty or non-repeatable reads
    
4. **Serializable** → fully isolated, as if transactions run sequentially
    

**Lower isolation** = more performance  
**Higher isolation** = more correctness

Implementation:

- Locks
    
- Multi-Version Concurrency Control (MVCC)
    
- Snapshot isolation
    

PostgreSQL uses MVCC heavily; MySQL allows different storage engines.


## **4. Durability – “Committed Means Saved”**

When a transaction is committed, it must persist even if:

- Power fails
    
- OS crashes
    
- Hardware resets
    

DB ensures durability through:

- WAL logs
    
- Disk flushes
    
- Replication
    
- RAID or multi-node persistence in distributed systems