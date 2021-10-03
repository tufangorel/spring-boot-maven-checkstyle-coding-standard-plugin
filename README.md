## spring-boot-maven-checkstyle-coding-standard-plugin

Purpose : Enforce common coding style for java source code in IDE at source code compile time. <br/>
Result : Get detailed report about violation of pre-defined common coding style issues such as incorrect indentation, * import, package-class-method-variable naming convention etc. <br/>

### Local run steps <br/>
1- To activate maven checkstyle plugin run the following maven command : <br/>
NOT : Execute maven command from where the pom.xml is located in the project directory. <br/>
<pre> 
$ mvn clean install <br/>
</pre>

[ERROR] \test\StoreServiceIntegrationTest.java:45:19: '(' is followed by whitespace. <br/>
[ERROR] \test\StoreServiceIntegrationTest.java:45:49: ')' is preceded with whitespace. <br/>
[ERROR] \test\java\service\integration\test\StoreServiceIntegrationTest.java:46:19: '(' is followed by whitespace. <br/>
[ERROR] \test\java\service\integration\test\StoreServiceIntegrationTest.java:47:19: '(' is followed by whitespace. <br/>
[ERROR] \test\java\service\unit\test\ProductServiceUnitTest.java:48:32: '(' is followed by whitespace. <br/>
[ERROR] \test\java\service\unit\test\ProductServiceUnitTest.java:48:53: ')' is preceded with whitespace. <br/>
Audit done. <br/>
[INFO] ------------------------------------------------------------------------ <br/>
[INFO] BUILD FAILURE <br/>
[INFO] ------------------------------------------------------------------------ <br/>
[INFO] Total time:  6.120 s <br/>
[INFO] Finished at: 2021-10-03T15:29:57+03:00 <br/>
[INFO] ------------------------------------------------------------------------ <br/>
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-checkstyle-plugin:3.1.2:check (validate) on project spring-boot-maven-checkstyle-coding-standard-plugin: <br/>
Failed during checkstyle execution: <br/>
There are 201 errors reported by Checkstyle 9.0 <br/>
[ERROR] <br/>

![Maven CheckStyle Plugin](docs/maven_checkstyle_plugin.png) <br/>

### Tech Stack
Java 11 <br/>
H2 Database Engine <br/>
spring boot <br/>
spring boot starter data jpa <br/>
spring boot starter web <br/>
spring boot starter test <br/>
hibernate <br/>
logback <br/>
maven <br/>
maven-checkstyle-plugin <br/>
springfox-swagger-ui <br/>
datasource-proxy <br/>
Docker <br/>
<br/>

### Docker build run steps
NOT : Execute docker commands from where the DockerFile is located. <br/>
<pre>
$ docker system prune <br/>
$ docker build . --tag demo  <br/>
$ docker run -p 8080:8080 -e "SPRING_PROFILES_ACTIVE=dev" demo:latest <br/>
</pre>

## API OPERATIONS
### Save store with products successfully to database

Method : HTTP.POST <br/>
URL : http://localhost:8080/customer-info/store/save <br/>

Request : 
<pre>
curl --location --request POST 'http://localhost:8080/customer-info/store/save' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "jeans_store",
  "products": [
    {
      "name": "prod1"
    },
    {
      "name": "prod2"
    },
    {
      "name": "prod3"
    }
  ]
}'
</pre><br/>

Response : 

HTTP response code 200 <br/>
<pre>
{
    "id": 1,
    "name": "jeans_store",
    "products": [
        {
            "id": 1,
            "name": "prod3"
        },
        {
            "id": 2,
            "name": "prod1"
        },
        {
            "id": 3,
            "name": "prod2"
        }
    ]
}
</pre>


### List Store saved to database

Method : HTTP.GET <br/>
URL : http://localhost:8080/customer-info/store/list <br/>

Request : 
<pre>
curl --location --request GET 'http://localhost:8080/customer-info/store/list'
</pre><br/>

Response : 

HTTP response code 200 <br/>
<pre>
[
    {
        "id": 1,
        "name": "jeans_store",
        "products": [
            {
                "id": 1,
                "name": "prod3"
            },
            {
                "id": 2,
                "name": "prod1"
            },
            {
                "id": 3,
                "name": "prod2"
            }
        ]
    }
]
</pre><br/>
