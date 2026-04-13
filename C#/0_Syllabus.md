# Fundamentals
## SECTION 1 — Value Types vs Reference Types
What is the difference between Value Types and Reference Types in C#?
Where are Value Types and Reference Types stored in memory?
What happens when you assign a Value Type to another variable?
What happens when you assign a Reference Type to another variable?
Give examples of Value Types and Reference Types in C#?
What is the difference between struct and class in terms of value/reference?
What is boxing and unboxing in C#?
What are the performance implications of boxing and unboxing?
What is the object type in C#? How does it relate to all types?
What is a nullable value type? (int?, Nullable<T>)

## SECTION 2 — Type System & Keywords

What is the difference between var, explicit types, and dynamic?
When should you use var and when should you avoid it?
What is dynamic keyword? How is it different from object?
What is the difference between const and readonly?
Can readonly be set inside a constructor?
Can const be used with reference types?
What is static keyword? What are static classes?
What is the difference between static readonly and const?
What is the sealed keyword on a class?
What is the partial keyword in C#?

## SECTION 3 — Strings

What is the difference between string and String in C#?
Why are strings immutable in C#?
What is string interning?
What is the difference between string and StringBuilder?
When should you use StringBuilder over string?
What is string.Format() vs string interpolation ($"")?
What is @ verbatim string literal?
What is the difference between == and .Equals() for strings?
What are raw string literals in C# 11?
What is string.IsNullOrEmpty() vs string.IsNullOrWhiteSpace()?

## SECTION 4 — Method Parameters

What is the difference between passing by value and passing by reference?
What is the ref keyword in C#?
What is the out keyword in C#?
What is the difference between ref and out?
What is the in keyword in C#?
What is the params keyword in C#?
Can you use ref and out with async methods?
What is optional parameters in C#?
What is named arguments in C#?
What is the difference between ref, out and returning a Tuple?

## SECTION 5 — Nullable & Null Handling

What is a nullable type in C#?
What is the difference between null and default value?
What is the null coalescing operator ???
What is the null coalescing assignment operator ??=?
What is the null conditional operator ?.?
What is the difference between ?. and null check if (x != null)?
What is NullReferenceException? How do you prevent it?
What are nullable reference types in C# 8+?
What is the ! null forgiving operator in C#?
What is the difference between default keyword for nullable vs non-nullable types?

## SECTION 6 — Pattern Matching

What is Pattern Matching in C#?
What is the is pattern matching expression?
What is the switch expression in C# 8+?
What is the difference between switch statement and switch expression?
What is a positional pattern in C#?
What is a property pattern in C#?
What is a tuple pattern in C#?
What is a relational pattern in C#?
What is a logical pattern (and, or, not) in C#?
What is a list pattern in C# 11?

## SECTION 7 — Tuples & Deconstruction

What are Tuples in C#?
What is the difference between Tuple<T> and ValueTuple?
How do you name tuple elements in C#?
What is tuple deconstruction in C#?
What is the _ discard variable in C#?
How are tuples useful as return types vs creating a class?
What is the performance difference between Tuple and ValueTuple?
Can you deconstruct a custom class in C#?
What is positional deconstruction?
When should you use Tuples vs creating a dedicated class/struct?

# SECTION 8 — Type Conversion & Casting

What is implicit conversion vs explicit conversion in C#?
What is the difference between (int)x casting and Convert.ToInt32(x)?
What is as keyword in C#?
What is is keyword in C#?
What is the difference between as and explicit casting?
What is TryParse vs Parse?
What are user-defined conversions (implicit operator, explicit operator)?
What is checked and unchecked in C#?
What is widening vs narrowing conversion?
What is the difference between Convert.ToString() and .ToString()?

# SECTION 9 — Modern C# Features

What are records in C# 9+?
What is the difference between record, record class, and record struct?
What is init only setter in C#?
What are global usings in C# 10?
What are file-scoped namespaces in C# 10?
What is required keyword in C# 11?
What are primary constructors in C# 12?
What is collection expressions in C# 12?
What is the difference between with expression and object initializer?
What are top-level statements in C# 9?

# SECTION 10 — Miscellaneous but Important

What is the difference between == and ReferenceEquals()?
What is GetHashCode() and when should you override it?
What is the nameof() operator?
What is the sizeof() operator?
What is typeof() vs GetType() in C#?
What is the difference between Array and Span<T>?
What is unsafe code in C#?
What is the stackalloc keyword?
What are preprocessor directives in C# (#if, #region, #pragma)?
What is the difference between early-bound and late-bound in C#?

# Opps
🔷 SECTION 1 — Basics & Fundamentals

What is a Class vs an Object?
What is a Constructor and what are its types?
What is a Destructor? When is it called in C#?
What is the this keyword in C#?
What is the difference between a Class and a Struct in C#?
What are instance variables vs static variables?
Can a constructor be private? What's the use case?
What is a copy constructor in C#?
What is object initializer syntax in C#?
What is the difference between new keyword and object pooling?

🔷 SECTION 2 — Encapsulation

What is Encapsulation and why does it matter?
What are access modifiers in C#? (public, private, protected, internal, protected internal)
What are Properties in C#? How are they better than public fields?
What is the difference between private and protected?
What is data hiding and how does encapsulation achieve it?
What are auto-implemented properties?
What is the difference between a read-only property and a constant?
What is the readonly keyword vs const in C#?

🔷 SECTION 3 — Inheritance

What is Inheritance and what problem does it solve?
What types of inheritance does C# support?
Why doesn't C# support multiple inheritance with classes?
What is the base keyword in C#?
What is constructor chaining using : this() and : base()?
What is method overriding in C#? What rules apply?
What is the difference between virtual, override, and new keywords?
What is method hiding in C#?
Can we override a static method in C#?
What is the difference between IS-A and HAS-A relationships?
What is the sealed keyword? When would you use it?

🔷 SECTION 4 — Polymorphism

What is Polymorphism and what are its types?
What is compile-time polymorphism in C#? (Method Overloading)
What is runtime polymorphism in C#? (Method Overriding)
What is dynamic method dispatch in C#?
What is operator overloading in C#?
What is covariant return type?
What is the dynamic keyword in C#? How does it relate to polymorphism?
What is the difference between early binding and late binding?

🔷 SECTION 5 — Abstraction

What is Abstraction? How is it different from Encapsulation?
What is an Abstract Class in C#? Can it have a constructor?
What is an Interface in C#? How is it different from an Abstract Class?
Can an Interface have a constructor in C#?
What are default interface methods in C# 8+?
What is an explicit interface implementation?
When would you use an Abstract Class over an Interface and vice versa?
What is a Marker Interface?

🔷 SECTION 6 — Advanced OOP

What is Composition vs Aggregation vs Association?
What is Dependency Injection in C#?
What is the difference between shallow copy and deep copy?
What is ICloneable in C#?
What are immutable objects? How do you create one in C#?
What is a Singleton class? How is it implemented thread-safely in C#?
What is the difference between == and .Equals() in C#?
What is GetHashCode() and why must it be consistent with Equals()?
What are extension methods in C#?
What are partial classes in C#?
What is object deconstruction in C#?
What are records in C# 9+? How are they different from classes?

🔷 SECTION 7 — SOLID Principles

What is the Single Responsibility Principle (SRP)?
What is the Open/Closed Principle (OCP)?
What is the Liskov Substitution Principle (LSP)?
What is the Interface Segregation Principle (ISP)?
What is the Dependency Inversion Principle (DIP)?
Give a real-world C# violation of each SOLID principle and how to fix it.

🔷 SECTION 8 — Design Patterns

What are Design Patterns? Why are they important?
What are the 3 categories of design patterns?
Singleton Pattern — implementation + thread safety in C#
Factory Pattern — when and how to use it?
Abstract Factory Pattern
Builder Pattern — when to prefer it over constructors?
Observer Pattern — real-world use in C# (Events & Delegates)
Strategy Pattern
Decorator Pattern
Facade Pattern
Adapter Pattern
Repository Pattern (very common in .NET interviews)
What is the difference between Factory and Abstract Factory?
What is the difference between Strategy and Command pattern?

🔷 SECTION 9 — System Design (LLD with OOP)

Design a Parking Lot system using OOP in C#
Design an ATM Machine using OOP
Design a Library Management System
Design a Hotel Booking System
Design an Elevator/Lift System
Design a Chess Game using OOP
Design a Shopping Cart / E-commerce system
How do you identify classes, relationships, and responsibilities in LLD?

🔷 SECTION 10 — Tricky & Conceptual

What is the order of execution — static constructor, instance constructor, static block?
Can we override a sealed method?
Can an abstract class have a sealed method?
What is the difference between final, finally, and finalize equivalent in C#?
What happens when two interfaces have the same method signature?
What is upcasting and downcasting in C#?
What is the is and as keyword in C#?
What is boxing and unboxing in C#?
What is the difference between IEnumerable and IQueryable from an OOP perspective?
What is covariance and contravariance in C# generics?

#