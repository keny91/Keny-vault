#reactive_programming_patterns

**Reactive programming** is about handling **asynchronous data streams** and reacting to events. It shines in **real-time systems** or **high-concurrency environments**.

### 🔄 a. **Backpressure**

- **Problem**: Producers generate data faster than consumers can process.
    
- **Solution**: Use **backpressure signals** to slow or buffer input, or drop values.
    

**Use Case**:

- Streaming platforms (e.g., video, sensor data)
    
- APIs handling burst traffic
    

**Example in RxJava:**

```
Flowable.fromPublisher(publisher)
  .onBackpressureBuffer()
  .subscribe(consumer);
```

### 🧾 b. **Event Sourcing**

- **Instead of storing state**, store a **sequence of events** that represent changes over time.
    
- To get the current state, replay all events.
    

**Example**:

- Instead of “Balance = $500”, store:
    
    - “Deposited $200”
        
    - “Withdrew $100”
        
    - “Deposited $400”
        

**Why Use:**

- Full audit trail
    
- Time travel (debugging, analytics)
    
- Powerful for CQRS (Command-Query Responsibility Segregation)
    

---

### ⚡When Reactive Patterns Shine:

- Real-time systems
    
- Event-driven architectures
    
- Systems with unpredictable loads