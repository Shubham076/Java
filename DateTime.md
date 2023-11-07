
# Working with LocalDateTime in Java

The `java.time` package introduced in Java 8 includes `LocalDateTime`, which represents a date-time without a time zone. It can be used to represent a wide range of time-related tasks.

## Parsing and Formatting LocalDateTime


```
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class DateTimeExample {

    public static void main(String[] args) {
        // Parse a String into a LocalDateTime
        String strDate = "2023-11-07T15:23:01";
        LocalDateTime parsedDate = LocalDateTime.parse(strDate);

        // Format LocalDateTime into a String
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");
        String formattedDate = parsedDate.format(formatter);
        System.out.println("Formatted Date: " + formattedDate);
    }
}
``` 

## Conversion Between Different Time Zones

To convert `LocalDateTime` to a different time zone, you need to convert it to a `ZonedDateTime`. Here's how you can do it:

```
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.time.format.DateTimeFormatter;

public class TimeZoneConversion {

    public static void main(String[] args) {
        // LocalDateTime now
        LocalDateTime localDateTime = LocalDateTime.now();

        // Convert LocalDateTime to ZonedDateTime in system default time zone
        ZonedDateTime zonedDateTime = localDateTime.atZone(ZoneId.systemDefault());

        // Convert to a different time zone, for example, Europe/Paris
        ZonedDateTime parisTime = zonedDateTime.withZoneSameInstant(ZoneId.of("Europe/Paris"));
        
        // Format to a string for display
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss z");
        String formattedParisTime = parisTime.format(formatter);
        System.out.println("Current time in Paris: " + formattedParisTime);
    }
}
``` 

## Working with Timestamps

With `LocalDateTime`, you can obtain a timestamp in milliseconds since the Unix epoch (January 1, 1970, 00:00:00 GMT) by converting it to an `Instant`:

```
import java.time.LocalDateTime;
import java.time.ZoneOffset;

public class TimestampExample {

    public static void main(String[] args) {
        // Current LocalDateTime
        LocalDateTime localDateTime = LocalDateTime.now();

        // Convert LocalDateTime to timestamp
        long timestamp = localDateTime.toInstant(ZoneOffset.UTC).toEpochMilli();
        System.out.println("Timestamp: " + timestamp);
    }
}
``` 

Remember that `LocalDateTime` does not contain information about the time zone. If you need the current moment with time zone information, you should use `ZonedDateTime` or `Instant`.

### Addition And Subtraction

```
import java.time.LocalDate;
import java.time.Period;

public class DateTimeExample {

    public static void main(String[] args) {
        // Adding and subtracting days to/from the current date
        LocalDate today = LocalDate.now();
        LocalDate tenDaysLater = today.plusDays(10);
        LocalDate tenDaysBefore = today.minusDays(10);

        // Adding a period to a date
        Period period = Period.ofDays(5);
        LocalDate fiveDaysLater = today.plus(period);
    }
}
```
