#object-oriented-programming

### 1. **Inheritance**

A class (derived/child) inherits properties and methods from another class (base/parent). It allows code reuse and establishes an “is-a” relationship.

```
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def speak(self):
        print("Bark")

dog = Dog()
dog.speak()  # Output: Bark
```


### 2. **Polymorphism**

Objects of different classes can be treated through a common interface, but behave differently.

```
def animal_sound(animal):
    animal.speak()

animal_sound(Animal())  # Animal sound
animal_sound(Dog())     # Bark
```


### 3. **Method Overloading**

Having multiple methods with the same name but different parameters. _Python does not support it directly_, but can simulate it using default args or `*args`.

```
class Math:
    def add(self, a, b, c=0):
        return a + b + c

m = Math()
print(m.add(2, 3))     # 5
print(m.add(2, 3, 4))  # 9
```


### 4. **Encapsulation**

Hiding internal details of an object and exposing only what’s necessary.

```
class BankAccount:
    def __init__(self):
        self.__balance = 0  # private attribute

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance

acc = BankAccount()
acc.deposit(100)
print(acc.get_balance())  # 100
# print(acc.__balance)    # Error: private attribute
```

### 6. **Virtual Methods**

Methods in a base class meant to be overridden in derived classes. In Python, all methods are virtual by default.


#abstract-classes
### 7. **Abstract Classes**

Used to define interfaces or base behavior that **must** be implemented by subclasses. They can contain abstract and concrete methods.

```
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def start_engine(self):
        pass

class Car(Vehicle):
    def start_engine(self):
        print("Car engine started")

car = Car()
car.start_engine()  # Car engine started
```


### 8. **Constructor (`__init__`) and Destructor (`__del__`)**

Used to initialize or clean up objects.

```
class User:
    def __init__(self, name):
        self.name = name
        print(f"User {self.name} created")

    def __del__(self):
        print(f"User {self.name} deleted")

u = User("Alice")
# When `u` is deleted or program ends, destructor runs
```

#instace
### 9. **Class vs Instance Attributes**

- **Class attribute**: shared across all instances. A **class method**:

	- Is declared with the `@classmethod` decorator.
	    
	- Receives the **class itself** (`cls`) as the first argument.
	    
	- Can access and modify **class-level** data.
	    
	- Can be called on either a class or an instance.

```
class Example:
    count = 0

    @classmethod
    def increment_count(cls):
        cls.count += 1
        return cls.count
```

- **Instance attribute**: unique to each instance.
  
```
class Product:
    tax = 0.1  # class attribute

    def __init__(self, price):
        self.price = price  # instance attribute

a = Product(100)
b = Product(200)
print(a.tax, b.tax)  # 0.1 0.1
print(a.price, b.price)  # 100 200

```

### 10. **Static Methods vs Class Methods**

- `@staticmethod`: no access to class or instance.
    
- `@classmethod`: access to class, not instance.
  
```
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b

    @classmethod
    def description(cls):
        return f"This is {cls.__name__}"

print(MathUtils.add(2, 3))         # 5
print(MathUtils.description())     # This is MathUtils
```

### 11. **Composition vs Inheritance**

- **Inheritance**: “is-a” relationship.
    
- **Composition**: “has-a” relationship.

```
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()  # composition

    def drive(self):
        self.engine.start()

c = Car()
c.drive()  # Engine started
```


#operator-overload
### 12. **Operator Overloading**

Define how operators behave for custom objects.

```
class Point:
    def __init__(self, x, y):
        self.x, self.y = x, y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

p1 = Point(1, 2)
p2 = Point(3, 4)
p3 = p1 + p2
print(p3.x, p3.y)  # 4 6

```

Other operator overloadable:

| Operator | Method                  | Example                           |
| -------- | ----------------------- | --------------------------------- |
| `+`      | `__add__(self, other)`  | `a + b`                           |
| `-`      | `__sub__`               | `a - b`                           |
| `*`      | `__mul__`               | `a * b`                           |
| `/`      | `__truediv__`           | `a / b`                           |
| `//`     | `__floordiv__`          | `a // b`                          |
| `%`      | `__mod__`               | `a % b`                           |
| `**`     | `__pow__`               | `a ** b`                          |
| `==`     | `__eq__`                | `a == b`                          |
| `!=`     | `__ne__`                | `a != b`                          |
| `<`      | `__lt__`                | `a < b`                           |
| `>`      | `__gt__`                | `a > b`                           |
| `<=`     | `__le__`                | `a <= b`                          |
| `>=`     | `__ge__`                | `a >= b`                          |
| `[]`     | `__getitem__`           | `obj[key]`                        |
| `in`     | `__contains__`          | `x in obj`                        |
| `len()`  | `__len__`               | `len(obj)`                        |
| `str()`  | `__str__`               | `str(obj)` for printing           |
| `repr()` | `__repr__`              | debugging, `repr(obj)`            |
| `call()` | `__call__`              | Make an instance callable         |
| `with`   | `__enter__`, `__exit__` | Used in context managers (`with`) |
| `+=`     | `__iadd__`              | In-place addition                 |
| `-=`     | `__isub__`              | In-place subtraction              |

## 🦆 **Duck Typing**

“**If it walks like a duck and quacks like a duck, it's a duck**.”

In Python, you don’t need to inherit from a specific base class to use an object — if it implements the necessary methods, it's accepted.

```
class Duck:
    def quack(self):
        print("Quack!")

class Person:
    def quack(self):
        print("I'm quacking like a duck!")

def make_it_quack(thing):
    thing.quack()

make_it_quack(Duck())    # Quack!
make_it_quack(Person())  # I'm quacking like a duck!
```

**This is possible because Python uses **dynamic typing** and focuses on behavior, not inheritance.

## 🔁 **Mixin Classes**

Mixins are **small reusable classes** that add functionality to other classes through multiple inheritance. They aren’t meant to stand on their own.

```
class LoggerMixin:
    def log(self, message):
        print(f"[LOG]: {message}")

class User(LoggerMixin):
    def __init__(self, name):
        self.name = name
        self.log(f"User {self.name} created")

u = User("Alice")
# [LOG]: User Alice created
```

#inheritance #multi-inheritance
## ⚙️ **Multiple Inheritance**

A class can inherit from **more than one** base class.

```
class A:
    def action(self):
        print("A")

class B:
    def action(self):
        print("B")

class C(A, B):
    pass

c = C()
c.action()  # A (due to Method Resolution Order — MRO)
```

You can inspect MRO (Method Resolution Order) using:

```
print(C.__mro__)
```

When a class uses **multiple inheritance**, Python needs a clear rule to decide **which parent class to look at first** when a method or attribute is called.

```
class A: pass
class B(A): pass
class C(A): pass
class D(B, C): pass

print(D.__mro__)
```

This will show:
```
This shows a **tuple of classes** in the order Python will search:
```
**So when you call `d.method()`, Python will search in D → B → C → A.**

#metaclass
## 🧠 **Metaclasses** (Advanced)

A metaclass controls **how classes themselves are created**. Normally used to enforce patterns or auto-modify classes.

Useful in:

- ORM frameworks
    
- Plugin systems
    
- Validating class definitions

```
class Meta(type):
    def __new__(cls, name, bases, dct):
        print(f"Creating class {name}")
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=Meta):
    pass

# Output: Creating class MyClass
```

### 🔸 Without Metaclass:

You'd have to manually ensure naming rules.

### 🔸 With Metaclass:

You can enforce a rule globally across classes.

```
class UpperAttrMeta(type):
    def __new__(cls, name, bases, dct):
        new_attrs = {
            key.upper(): value
            for key, value in dct.items()
            if not key.startswith('__')
        }
        return super().__new__(cls, name, bases, new_attrs)

class MyClass(metaclass=UpperAttrMeta):
    foo = 'bar'
    baz = 123

print(hasattr(MyClass, 'foo'))  # False
print(hasattr(MyClass, 'FOO'))  # True
print(MyClass.BAZ)              # 123

```


You can use metaclasses to:

- Add logging to all methods
    
- Enforce interface implementation
    
- Register classes automatically in a plugin system