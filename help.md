We can ignore specific fields at the class level, using the @JsonIgnoreProperties annotation and specifying the fields by name:

@JsonIgnoreProperties(value = { "intValue" })
public class MyDto {
 
    private String stringValue;
    private int intValue;
    private boolean booleanValue;
 
    public MyDto() {
        super();
    }
 
    // standard setters and getters are not shown
}

We can also ignore a field directly via the @JsonIgnore annotation directly on the field:


public class MyDto {
 
    private String stringValue;
    @JsonIgnore
    private int intValue;
    private boolean booleanValue;
 
    public MyDto() {
        super();
    }
 
    // standard setters and getters are not shown
}

We can ignore all fields of a specified type, using the @JsonIgnoreType annotation. If we control the type, then we can annotate the class directly:

@JsonIgnoreType
public class SomeType { ... }

https://www.baeldung.com/jackson-ignore-properties-on-serialization

https://www.baeldung.com/jackson-collection-array

https://github.com/eugenp/tutorials/tree/master/jackson#readme
