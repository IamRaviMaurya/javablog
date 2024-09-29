---
title: "Java OOPs"
date: 2019-06-16
weight: 1
---

Object-oriented programming (OOP) is a way of writing code in Java that uses objects and classes to design and develop software. It's based on the idea that objects are the core building blocks of a program, and that they have properties and behaviors similar to things in the real world.

![Accounting Services](/images/oops/oops.png)

- Classes: These are user-defined data types that act as blueprints for objects, attributes, and methods.
- Objects: These are instances of a class that are created with specific data.
- Methods: These are functions that objects can perform.
- Attributes: These represent the state of an object.

# In a Java program how many Java classes can we take?

- In the Java program, we can take N number of classes.

### Example

File Name 'Test.java'

```java
@Configuration
class A{
}
class B{
}
class C{
}
class D{
}
```

For the above classes we can save in a single program and we can also save files under whatever name we want. When we compile the code then we get whatever name we have taken for the class for those only bytecode will be generated for the above example if we compile code **javac Test.java** then we get 4 different bytecode class names. 
**A.class**, **B.class**, **C.class**, and **D.class**.

# What is a public keyword in Java?

- In Java 'public' keyword is the access modifier. Access modifier mean visibility and accessibility of the class or its members.
- Public class is visible for all other classes. If a class is declared public, all other classes interact with it no matter where they are located within the project.

- Only one public class is allowed per file.
  - A single Java file can contain multiple classes, but only one of them can be public.
- The file name must match the public class name.
  - The name of the Java file must exactly match the name of the public class. This means the file should be saved as ClassName.java if the class is declared as public class ClassName.
- If the file name does not match the public class name, the compiler will give an error.
  - The Java compiler (javac) will expect the file to be named after the public class. If the file name is different, it will throw a compilation error.

# What is the fully qualified name?

A fully qualified name consists package name followed by the class name. It is used to avoid name conflict and access classes without import.

### Example

```java
com. example.utl.List customList = new com. example.utl.List();
java.util.List<String> javaList = new java.util.List<>();
```

It helps avoid name conflicts when two classes have the same name but belong to different packages.

# What is an import keyword and how many types of import?

A import keyword is used to bring a certain class or entire package into visibility for use in our Java program. By using import we can refer there simple names instead of using fully qualified names.

## There are main two type of import

- **Explicit import(Single Type Import):**- Its import class name from package without need to fully qualified name.

```java
import java.util.List;  
```

- **Implicit import or wild card import or on-demand impor**t:- It imports all public classes for specific packages and does not import sub-packages and it does not import nonclass members like static fields or methods

```java
import java.util.*;
```

## A special type of import

- **Static Import**:- This imports static members (methods and fields) from a class, allowing them to use the class name.

```java
import static java.lang.Math.PI;
import static java.lang.Math.*;
public class Example {
    public static void main(String[] args) {
        System.out.println(PI);
        System.out.println(sqrt(16));
    }
}
// Using PI directly without Math.PI
// Using sqrt directly without Math.sqrt 
```

If we are using the same package class we don't need the required import statement also java.long package does not need to require import by default it's imported.

>**Note:** Whenever we are importing a package all classes are present in that package are available but not subpackage class will available so if we want to import a sub package class then we have to follow till subpackage class by dot(.).