
# Lombok Annotations Guide

Project Lombok is a Java library that automatically plugs into your editor and build tools, and helps to avoid boilerplate code. It does this by providing a set of annotations that can be used to generate code like getters, setters, and various other utility methods and constructors. Below are some of the most important and commonly used Lombok annotations and what they do:

## `@Getter` and `@Setter`

These annotations generate the getters and setters for your fields.

-   `@Getter`: Generates a getter method for a field.
-   `@Setter`: Generates a setter method for a field.

```
import lombok.Getter;
import lombok.Setter;

public class User {
    @Getter @Setter private String name;
    @Getter @Setter private int age;
}
``` 

## `@ToString`

Generates an implementation of the `toString()` method.


```
import lombok.ToString;

@ToString
public class User {
    private String name;
    private int age;
}
``` 

The `toString()` method would output something like `User(name=John, age=30)

## `@EqualsAndHashCode`

Generates `equals(Object other)` and `hashCode()` methods.

javaCopy code

```i
mport lombok.EqualsAndHashCode;

@EqualsAndHashCode
public class User {
    private String name;
    private int age;
}
``` 

## `@NoArgsConstructor`, `@RequiredArgsConstructor`, and `@AllArgsConstructor`

These annotations generate constructors.

-   `@NoArgsConstructor`: Generates a no-argument constructor.
-   `@RequiredArgsConstructor`: Generates a constructor for all final fields, plus any fields marked with `@NonNull` that aren't initialized where they are declared.
-   `@AllArgsConstructor`: Generates a constructor with one parameter for each field in your class.


```
import lombok.NoArgsConstructor;
import lombok.RequiredArgsConstructor;
import lombok.AllArgsConstructor;
import lombok.NonNull;

@NoArgsConstructor
@RequiredArgsConstructor
@AllArgsConstructor
public class User {
    @NonNull private String name;
    private int age;
}
``` 

## `@Data`

A shortcut for `@ToString`, `@EqualsAndHashCode`, `@Getter` on all fields, `@Setter` on all non-final fields, and `@RequiredArgsConstructor`.


```
import lombok.Data;

@Data
public class User {
    private final String name;
    private int age;
}
``` 

## `@Value`

Immutable variant of `@Data`; all fields are made `private` and `final` by default, and setters are not generated.


```
import lombok.Value;

@Value
public class User {
    String name;
    int age;
}
``` 

## `@Builder`

Implements the Builder pattern for object creation.


```
import lombok.Builder;

@Builder
public class User {
    private String name;
    private int age;
}
``` 

## `@Slf4j`

Generates a logger field using SLF4J (Simple Logging Facade for Java).

javaCopy code

```
import lombok.extern.slf4j.Slf4j;

@Slf4j
public class User {
    public void doSomething() {
        log.debug("Doing something");
    }
}
``` 

## `@NonNull`

Generates a null-check statement for the annotated parameter or field.

javaCopy code

```
import lombok.NonNull;

public class User {
    private final String name;
    
    public User(@NonNull String name) {
        this.name = name;
    }
}
``` 

These are some of the key annotations provided by Lombok, each serving to reduce boilerplate code in Java applications. By using Lombok, developers can keep their model and data classes concise and focus on the logic rather than repetitive method creation.

To use Lombok, you need to add it to your project's build configuration and ensure your IDE has the Lombok plugin installed and enabled, so it can recognize the annotations and generate the corresponding bytecode.# Lombok Annotations Guide

Project Lombok is a Java library that automatically plugs into your editor and build tools, and helps to avoid boilerplate code. It does this by providing a set of annotations that can be used to generate code like getters, setters, and various other utility methods and constructors. Below are some of the most important and commonly used Lombok annotations and what they do:

