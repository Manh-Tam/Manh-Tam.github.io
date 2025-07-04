---
layout: post
title: "OOP in C#: Class Definition, Member Variables (Fields), Constructor, Properties"
date: 2025-06-29
---

### **Base Class - Derived Class**

**Also known as:**

* Parent Class - Child Class
* Superclass - Subclass

---

### **178. Inheritance: Base Class vs Derived Class**

* A **Base Class** is a class whose properties and methods are inherited by another class.
* A **Derived Class** is a class that inherits properties and methods from the base class.

✅ **Syntax in C#:**

```csharp
class BaseClass 
{
    // base class members
}

class DerivedClass : BaseClass 
{
    // derived class members
}
```

C# supports class inheritance, just like C++.

---

### **179. HAS-A and IS-A Relationships in C#**

* **HAS-A** relationship: A class contains another class as a member (field). This is *composition*.
* **IS-A** relationship: A derived class is a type of its base class. This is *inheritance*.

✅ Example:

```csharp
class Engine {}  
class Car // HAS-A relationship  
{
    Engine engine = new Engine();  
}

class Dog : Animal // IS-A relationship  
{}
```

---

### **180. Types of Inheritance in C#**

1. **Single Inheritance**

```csharp
class DerivedClass : BaseClass {}
```

2. **Multilevel Inheritance**

```csharp
class FurtherDerivedClass : DerivedClass {}
```

3. **Hierarchical Inheritance**

```csharp
class DerivedClass1 : BaseClass {}
class DerivedClass2 : BaseClass {}
```

4. **Multiple Inheritance** (❌ Not supported in C# with classes)

> C# does **not** support multiple inheritance with classes.
> But it allows it using **interfaces** instead.

---

### **181. Access Modifiers and the `protected` Keyword**

* **private**: Only accessible within the class itself.
* **protected**: Accessible within the class and by derived classes.
* **public**: Accessible from anywhere.

These access modifiers help implement **encapsulation**, one of the main principles of OOP.

---

### **182. Method Overriding (`virtual` and `override`)**

To enable **polymorphism**, C# uses `virtual` in the base class method, and `override` in the derived class method.

✅ Example:

```csharp
class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("A generic sound");
    }
}

class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Gau Gau...");
    }
}

class Program
{
    static void Main()
    {
        Animal dog = new Dog();
        dog.MakeSound(); // Output: Gau Gau...
    }
}
```

Even though the variable type is `Animal`, the overridden method in `Dog` is called.
This is **runtime polymorphism**.

---

### **183. Method Hiding (`new` keyword)**

If a derived class defines a method with the same name as in the base class **without** using `override`, it **hides** the base class method.

✅ Example:

```csharp
class Animal
{
    public void MakeSound()
    {
        Console.WriteLine("Animal sound");
    }
}

class Dog : Animal
{
    public new void MakeSound()
    {
        Console.WriteLine("Dog sound");
    }
}
```

This is **not** polymorphism. Use `new` keyword to make it explicit that you are hiding a method.

---

### **184. Sealed Methods in C#**

A `sealed` method **cannot** be overridden again in any further derived class.

✅ Example:

```csharp
class Person
{
    public virtual void SayHello()
    {
        Console.WriteLine("Hello");
    }
}

class Student : Person
{
    public sealed override void SayHello()
    {
        Console.WriteLine("Student");
    }
}

class GoodStudent : Student
{
    // Error! Cannot override a sealed method
    // public override void SayHello() {}
}
```

🔒 Use `sealed` to **stop** method overriding in deeper inheritance levels.

---

### **185. The `base` Keyword and Why Inheritance Matters**

* The `base` keyword allows a derived class to call methods or constructors from its base class.

✅ Example (method):

```csharp
class Person
{
    public void PrintPerson()
    {
        Console.WriteLine("Person");
    }
}

class Student : Person
{
    public void PrintStudent()
    {
        base.PrintPerson();
        Console.WriteLine("Student");
    }
}
```

✅ Example (constructor):

```csharp
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}

class Student : Person
{
    public int Grade { get; set; }

    public Student(string name, int age, int grade) : base(name, age)
    {
        Grade = grade;
    }
}
```

✔️ Using `base(...)` in the constructor ensures that the base class is initialized properly.

---

### **186. Abstract Classes and Methods in C#**

* An **abstract class** cannot be instantiated. It is a blueprint for other classes.
* It may contain **abstract methods** (methods without a body) that must be implemented in the derived class.

✅ Example:

```csharp
abstract class Animal
{
    public abstract void MakeSound();
}

class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Gau Gau...");
    }
}
```

---

### **187–190. Constructor Inheritance**

You already covered this in section 185 using `base(...)`. Just remember:

* Base constructors are **not inherited**, but you can call them using `base(...)`.
* Constructor inheritance helps initialize shared properties properly.
* It's useful in deep inheritance chains or when base class initialization logic is important.

---

### **191. Every Class Inherits from the `Object` Class**

In C#, all classes automatically inherit from the `System.Object` class.

This means every class has access to methods like:

* `ToString()`
* `Equals()`
* `GetHashCode()`
* `GetType()`

---

### **192. XML Comments Documentation**

In C#, you can use XML comments (`///`) to generate documentation.

✅ Example:

```csharp
/// <summary>
/// This class represents a student.
/// </summary>
class Student
{
    /// <summary>
    /// Prints student info
    /// </summary>
    public void PrintInfo() {}
}
```

You can generate API documentation using tools like **DocFX** or within **Visual Studio**.

---

### **193. The `sealed` Keyword**

* A **sealed class** cannot be inherited.
* This is like a **final class** in other languages (e.g., Java).

✅ Example:

```csharp
sealed class UtilityClass
{
    public static void DoWork() {}
}

// class MyClass : UtilityClass {} // ❌ Error
```

---

### **194. Cheatsheet – Inheritance & OOP in C#**

* `:` → Inheritance
* `virtual`, `override`, `sealed` → Polymorphism
* `abstract`, `interface` → Design contracts
* `base` → Access base class methods/constructors
* `protected` → Access from subclasses
* `sealed class` → Cannot be inherited

---

Would you like me to turn this into a properly formatted PDF or Word document? Or keep helping you write more sections like interfaces, events, or delegates?
