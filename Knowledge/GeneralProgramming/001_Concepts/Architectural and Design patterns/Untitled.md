#anti_patterns


**Anti-patterns** are solutions that seem helpful at first but cause problems in the long run.

### 💥 a. **God Object / God Class**

- One class does everything → too big, unmaintainable.
    
- Violates Single Responsibility Principle.
    

**Solution**: Refactor into smaller, focused classes.

---

### 🔗 b. **Tight Coupling**

- Components are too dependent on each other’s internals.
    
- Changes in one part ripple through others.
    

**Solution**: Use interfaces, dependency injection, events.

---

### 🧱 c. **Big Ball of Mud**

- Code with no clear architecture or boundaries.
    
- Common in rushed or legacy projects.
    

**Solution**: Apply modular design, DDD, or service boundaries.

---

### 🔄 d. **Reinventing the Wheel**

- Writing your own auth system, DB, framework without need.
    

**Solution**: Use battle-tested libraries and standards.

---

### 🔁 e. **Premature Optimization**

- Making things faster/clever before knowing it’s needed.
    
- Increases complexity and maintenance cost.
    

**Solution**: First write clean, correct code → then profile.

---

### 🔥 f. **Copy-Paste Programming**

- Repeating the same code with slight tweaks.
    

**Solution**: Use functions, templates, inheritance, or polymorphism.

---