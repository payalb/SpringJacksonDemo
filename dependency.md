 The Jackson library is composed of three components: Jackson Databind, Core, and Annotation. Jackson Databind has internal dependencies on Jackson Core and Annotation. Therefore, adding Jackson Databind to your Maven POM dependency list will include the other dependencies as well. 

When Jackson maps JSON to POJOs, it inspects the setter methods. Jackson by default maps a key for the JSON field with the setter method name. For Example, Jackson will map the name JSON field with the setName() setter method in a POJO.

In the JSON Tree Model, the ObjectMapper constructs a hierarchical tree of nodes from JSON data. If you are familiar with XML processing, you can relate the JSON Tree Model with XML DOM Model. In the JSON Tree Model, each node in the tree is of the JsonNode type, and represents a piece of JSON data. In the Tree Model, you can randomly access nodes with the different methods that JsonNode provides.

public String readNameNode()
{
    JsonNode nameNode=rootNode.path("name");
    String name=nameNode.asText();
    logger.info("\n----------------------------\nEmployee Nme: "+name+"\n");
    return name;
}
. . .
In the code above, we called the path() method on the JsonNode object that represents the root node. To the path() method, we passed the name of the node to access, which in this example is name. We then called the asText() method on the JsonNode object that the path() method returns. The asText() method that we called returns the value of the name node as a string.

let’s access the personalInformation and phoneNumbers nodes.


. . .
public Map<String,String> readPersonalInformation() throws JsonProcessingException
 {
     JsonNode personalInformationNode = rootNode.get("personalInformation");
     Map<String, String> personalInformationMap = objectMapper.convertValue(personalInformationNode, Map.class);
     for (Map.Entry<String, String> entry : personalInformationMap.entrySet())
     {
         logger.info("\n----------------------------\n"+entry.getKey() + "=" + entry.getValue()+"\n");
     }
       return personalInformationMap;
 }

 public Iterator<JsonNode> readPhoneNumbers(){
     JsonNode phoneNumbersNode = rootNode.path("phoneNumbers");
     Iterator<JsonNode> elements = phoneNumbersNode.elements();
     while(elements.hasNext()){
         JsonNode phoneNode = elements.next();
         logger.info("\n----------------------------\nPhone Numbers = "+phoneNode.asLong());
     }
     return elements;
 }

. . .
public Map<String,String> readPersonalInformation() throws JsonProcessingException
 {
     JsonNode personalInformationNode = rootNode.get("personalInformation");
     Map<String, String> personalInformationMap = objectMapper.convertValue(personalInformationNode, Map.class);
     for (Map.Entry<String, String> entry : personalInformationMap.entrySet())
     {
         logger.info("\n----------------------------\n"+entry.getKey() + "=" + entry.getValue()+"\n");
     }
       return personalInformationMap;
 }
 
 public Iterator<JsonNode> readPhoneNumbers(){
     JsonNode phoneNumbersNode = rootNode.path("phoneNumbers");
     Iterator<JsonNode> elements = phoneNumbersNode.elements();
     while(elements.hasNext()){
         JsonNode phoneNode = elements.next();
         logger.info("\n----------------------------\nPhone Numbers = "+phoneNode.asLong());
     }
     return elements;
 }
. . . .
 
 we called the get() method instead of path() on the root node. Both the methods perform the same functions – they return the specified node as a JsonNode object. The difference is how they behave when the specified node is not present or the node doesn’t have an associated value. When the node is not present or does not have a value, the get() method returns a null value, while the path() method returns a JsonNode object that represents a “missing node“. The “missing node” returns true for a call to the isMissingNode() method
