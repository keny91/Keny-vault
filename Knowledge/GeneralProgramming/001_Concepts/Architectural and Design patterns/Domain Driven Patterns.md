#Domain_patterns

**Domain-Driven Design** is about modeling software closely around the **business domain** and using shared language between developers and domain experts. These patterns help manage complexity, especially in **large systems**.

### 🧩 a. **Value Objects**

- **Definition**: Immutable objects that represent a concept (e.g., Money, Coordinates) but **have no identity**.
    
- **Example**: Two `$10` bills are the same value — we care about the amount, not which specific bill.
    

**Why Use:**

- Simpler than entities
    
- Immutable → safe for concurrent use
  
```
class Money {
  private final BigDecimal amount;
  private final String currency;
}
```

### 🧱 b. **Aggregates**

- **Definition**: A **cluster of related objects** treated as a single unit for data changes.
    
- Has a **root entity** (called _Aggregate Root_) that controls access and invariants.
    

**Example**: An `Order` aggregate might contain `OrderItems`, but only the `Order` can update them.

**Why Use:**

- Enforces consistency boundaries
    
- Reduces bugs in complex object graphs
    

---

### 📦 c. **Repositories**

- **Definition**: Abstractions that **store and retrieve aggregates**, simulating a collection in memory.
    

**Example**:

```
OrderRepository.save(order);
OrderRepository.findById(orderId);
```

**Why Use:**

- Separates domain logic from persistence concerns (e.g., SQL, NoSQL, etc.)
    

---

### ✅ When DDD Shines:

- Complex business domains (e.g., banking, insurance, logistics)
    
- Microservices with clearly bounded contexts
    
- Systems requiring clear business rules and validation