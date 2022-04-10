# C# Fundamentals

**1.** What is the purpose of a `namespace`?

<!-- enter you answer in the space below -->

```
Namespaces are used to organize code into logical groups and to prevent name collisions that can occur especially when your code base includes multiple libraries.
```

**2.** What is the difference between a `class` and a `struct`?

<!-- enter you answer in the space below -->

```
A struct is a value type and classes are reference types
```

**3.** What is the method that returns an instance of a class, yet it has no return type?

<!-- enter you answer in the space below -->

```
Void
```

## Example 1

```c#
abstract class Car
{
  ...
  public virtual string Start()
  {
    return "Vroooom";
  }
}
```

**5.** In the example what is the access modifier of the `Start()` method?

<!-- enter you answer in the space below -->

```
public
```

**6.** In the example what is `string` an indication of?

<!-- enter you answer in the space below -->

```
The return type
```

**7.** In the example what is `abstract` preventing?

<!-- enter you answer in the space below -->

```
The purpose of an abstract class is to provide a blueprint for derived classes and set the rules for what the derived classes must implement of inhertiance. We have not gone over abstract classes or inheritance yet.
```

**8.** In the example what is the purpose of `virtual`?

<!-- enter you answer in the space below -->

```
The virtual in a c# class allows it to be overidden
```

**9.** Name four access modifiers:

<!-- enter you answer in the space below -->

```
public, void, internal, private
```

**10.** If you set a class or method to private, what can access it?

<!-- enter you answer in the space below -->

```
Only the methods that are within its namespace
```

```

```
