
# Optional Class in Java

The `Optional` class is a container object used to contain not-null objects. `Optional` object is used to represent null with absent value. This class has various utility methods to facilitate code to handle values as ‘available’ or ‘not available’ instead of checking null values.

## Methods and Examples

**empty()**  
Creates an empty instance of `Optional`.

```
Optional<String> optionalEmpty = Optional.empty();
``` 

**of()**  
Returns an `Optional` with the specified non-null value.

```
Optional<String> optionalOf = Optional.of("Hello, World!");
``` 

**ofNullable()**  
Returns an `Optional` for a specified value, allowing null.


```
Optional<String> optionalOfNullable = Optional.ofNullable(null);
``` 

**isPresent()**  
Checks whether there is a value present or not.

```
if (optionalOf.isPresent()) {
    System.out.println("Value found.");
}
``` 

**ifPresent()**  
Performs the given action with the value if it is present.


```
optionalOf.ifPresent(System.out::println);
``` 

**orElse()**  
Returns the value if present, or an alternative if not.


```
String value = optionalOfNullable.orElse("Default Value");
``` 

**orElseGet()**  
Similar to `orElse()`, but the alternative value is provided through a supplier.

```
String value = optionalOfNullable.orElseGet(() -> "Alternative Value");
``` 

**orElseThrow()**  
Returns the value if present, or throws an exception.


```
String value = optionalOfNullable.orElseThrow(NoSuchElementException::new);
``` 

**map()**  
If a value is present, applies the mapping function to it, and if the result is non-null, returns an `Optional`.


```
Optional<Integer> stringLength = optionalOf.map(String::length); 
```

**flatMap()**  
If a value is present, it applies the `Optional`-bearing function to it, returns that result, otherwise returns an empty `Optional`.


```
Optional<Integer> stringLength = optionalOf.flatMap(s -> Optional.of(s.length()));
```

**filter()**  
If a value is present, and the value matches the predicate, returns an `Optional` describing the value, otherwise returns an empty `Optional`.


```
Optional<String> longString = optionalOf.filter(s -> s.length() > 10);
``` 
