### Examples
- Function<T, R>: Takes an argument of type T and returns a result of type R.
- Consumer<T>: Accepts a single input argument of type T and returns no result (represents an operation to be performed on the argument).
- Supplier<T>: Represents a supplier of results (no arguments, returns a result of type T).
- Predicate<T>: Takes an argument of type T and returns a boolean value.
- UnaryOperator<T>: A specialization of Function where the input and output are the same type.
- BiFunction<T, U, R>: Like Function, but takes two arguments.

```
import java.util.function.Function;
import java.util.function.Consumer;
import java.util.function.Supplier;
import java.util.function.Predicate;

public class FunctionalInterfaceExamples {
    
    public static void main(String[] args) {
        
        // Using Function interface
        Function<String, Integer> lengthFunction = String::length;
        Integer length = lengthFunction.apply("Hello");
        System.out.println(length); // Outputs: 5
        
        // Using Consumer interface
        Consumer<String> printConsumer = System.out::println;
        printConsumer.accept("Hello, Consumer!"); // Outputs: Hello, Consumer!
        
        // Using Supplier interface
        Supplier<Double> randomSupplier = Math::random;
        Double randomValue = randomSupplier.get();
        System.out.println(randomValue); // Outputs a random value
        
        // Using Predicate interface
        Predicate<String> nonEmptyStringPredicate = (String s) -> !s.isEmpty();
        boolean isNonEmpty = nonEmptyStringPredicate.test("Not empty");
        System.out.println(isNonEmpty); // Outputs: true
    }
}
```
