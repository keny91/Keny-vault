#creational_pattern 

Focus on object creation mechanisms, trying to create objects in a manner suitable to the situation.

|Pattern|What it does|Use Case Example|
|---|---|---|
|**Singleton**|Ensures a class has only one instance and provides a global access point to it.|Managing a shared resource like a logging service or configuration manager.|
|**Factory Method**|Defines an interface for creating an object, but lets subclasses decide which class to instantiate.|When a class can't anticipate the type of objects it needs to create upfront.|
|**Abstract Factory**|Provides an interface for creating families of related objects without specifying their concrete classes.|UI toolkits that support multiple look-and-feels (Windows/Mac/Linux).|
|**Builder**|Separates construction of a complex object from its representation, so the same construction process can create different representations.|Constructing complex objects like HTML pages, complex documents, or configurations.|
|**Prototype**|Creates new objects by copying an existing object, known as the prototype.|When object creation is expensive or complex, and many similar objects are needed.|