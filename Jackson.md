
## Jackson

## Convert Object to JSON String

javaCopy code

```
import com.fasterxml.jackson.databind.ObjectMapper;

public class JacksonExample {

    public String convertObjectToJson(Object object) throws IOException {
        ObjectMapper mapper = new ObjectMapper();
        return mapper.writeValueAsString(object);
    }
}
``` 

## Convert JSON String to Object


```
import com.fasterxml.jackson.databind.ObjectMapper;

public class JacksonExample {

    public <T> T convertJsonToObject(String json, Class<T> clazz) throws IOException {
        ObjectMapper mapper = new ObjectMapper();
        return mapper.readValue(json, clazz);
    }
}
``` 

## Convert Object to JSON and Write to File

```
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.File;

public class JacksonExample {

    public void writeObjectToJsonFile(Object object, String filename) throws IOException {
        ObjectMapper mapper = new ObjectMapper();
        mapper.writeValue(new File(filename), object);
    }
}
``` 

## Convert JSON from File to Object

```
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.File;

public class JacksonExample {

    public <T> T readJsonFromFile(String filename, Class<T> clazz) throws IOException {
        ObjectMapper mapper = new ObjectMapper();
        return mapper.readValue(new File(filename), clazz);
    }
}
``` 

## Some Jackson Properties and Annotations

### Annotations

-   `@JsonProperty`: Specifies the property name in JSON.
-   `@JsonIgnore`: Marks a property to be ignored during serialization and deserialization.
-   `@JsonFormat`: Used to specify the format when serializing Date/Time values.
-   `@JsonInclude`: Include properties only when they meet certain criteria.
-   `@JsonIgnoreProperties`: Ignore a list of properties globally at the class level.
-   `@JsonAlias`: Defines one or more alternative names for a property during deserialization.

### Properties

-   `SerializationFeature`: Configure serialization features such as whether to write dates as timestamps.
-   `DeserializationFeature`: Configure deserialization features, for instance, to fail or not when encountering unknown properties.
-   `MapperFeature`: Enable or disable various features of the `ObjectMapper`.

Here's how you might configure an `ObjectMapper` with these properties:

```
import com.fasterxml.jackson.databind.DeserializationFeature;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;

public class JacksonConfiguration {

    public ObjectMapper objectMapper() {
        ObjectMapper mapper = new ObjectMapper();
        mapper.enable(SerializationFeature.INDENT_OUTPUT);
        mapper.disable(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES);
        // ... more configuration
        return mapper;
    }
}
``` 

Using these configurations and annotations, you can fine-tune how Jackson serializes and deserializes objects to and from JSON.


# Jackson Annotations Examples

Jackson annotations are used to configure the serialization and deserialization behavior of Java objects. Here are a few common annotations with examples:

## `@JsonProperty`

Used to map a property to a JSON key that may be different from the Java field name.

```
import com.fasterxml.jackson.annotation.JsonProperty;

public class User {
    @JsonProperty("id")
    private int userId;

    @JsonProperty("name")
    private String userName;

    // Constructors, getters, and setters
}
``` 

## `@JsonIgnore`

Used to ignore a Java property during serialization and deserialization.

```
import com.fasterxml.jackson.annotation.JsonIgnore;

public class User {
    private int userId;

    @JsonIgnore
    private String password;

    // Constructors, getters, and setters
}
``` 

## `@JsonFormat`

Used to format date and time values during serialization.

```
import com.fasterxml.jackson.annotation.JsonFormat;
import java.util.Date;

public class User {
    private String name;

    @JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd HH:mm:ss")
    private Date lastLogin;

    // Constructors, getters, and setters
}
``` 

## `@JsonInclude`

Used to include properties only when they meet certain criteria, such as non-null.


```
import com.fasterxml.jackson.annotation.JsonInclude;

@JsonInclude(JsonInclude.Include.NON_NULL)
public class User {
    private String name;
    private String email;

    // Constructors, getters, and setters
}
``` 

## `@JsonIgnoreProperties`

Used to ignore a set of properties globally at the class level.

```
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;

@JsonIgnoreProperties(value = { "password", "secretQuestion" })
public class User {
    private String name;
    private String email;
    private String password;
    private String secretQuestion;

    // Constructors, getters, and setters
}
``` 

## `@JsonAlias`

Used to define alternative names for a property during deserialization.

```
import com.fasterxml.jackson.annotation.JsonAlias;

public class User {
    @JsonAlias({"username", "user_name"})
    private String name;

    // Constructors, getters, and setters
}
``` 

# Custom Serializer/Deserializer Example

Sometimes, you need custom serialization or deserialization logic. You can implement this by extending `JsonSerializer<T>` or `JsonDeserializer<T>`.

## Custom Serializer


```
import com.fasterxml.jackson.core.JsonGenerator;
import com.fasterxml.jackson.databind.JsonSerializer;
import com.fasterxml.jackson.databind.SerializerProvider;
import java.io.IOException;

public class CustomDateSerializer extends JsonSerializer<Date> {

    private static final SimpleDateFormat dateFormat = new SimpleDateFormat("dd-MM-yyyy");

    @Override
    public void serialize(Date value, JsonGenerator gen, SerializerProvider serializers) throws IOException {
        gen.writeString(dateFormat.format(value));
    }
}
``` 

You can then use the custom serializer in your model:


```
import com.fasterxml.jackson.databind.annotation.JsonSerialize;
import java.util.Date;

public class Event {
    private String title;

    @JsonSerialize(using = CustomDateSerializer.class)
    private Date eventDate;

    // Constructors, getters, and setters
}
``` 

## Custom Deserializer

```
import com.fasterxml.jackson.core.JsonParser;
import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.DeserializationContext;
import com.fasterxml.jackson.databind.JsonDeserializer;

import java.io.IOException;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class CustomDateDeserializer extends JsonDeserializer<Date> {

    private static final SimpleDateFormat dateFormat = new SimpleDateFormat("dd-MM-yyyy");

    @Override
    public Date deserialize(JsonParser p, DeserializationContext ctxt) throws IOException, JsonProcessingException {
        String date = p.getText();
        try {
            return dateFormat.parse(date);
        } catch (ParseException e) {
            throw new RuntimeException(e); // or handle exception
        }
    }
}
``` 

And apply it to your model like this:

```
import com.fasterxml.jackson.databind.annotation.JsonDeserialize;
import java.util.Date;

public class Event {
    private String title;

    @JsonDeserialize(using = CustomDateDeserializer.class)
    private Date eventDate;

    // Constructors, getters, and setters
}
``` 

Remember to handle exceptions appropriately in production code rather than throwing `RuntimeException`. Custom serializers and deserializers allow you to precisely control the JSON output and input beyond what's possible with standard annotations.
