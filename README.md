# What is REST API (Representational State Transfer Application Programming Interface)
 - Is architectural style and the standard way to client and server to communicate in web services and also REST API is a stateless tranfer protocol that uses HTTP method to interact with the server. meaning the client should pass all the required data needed to call the server via api endpoint without the client or the backend maintain some state to interact to each other example using HTTPSession or cookies.

##### REST API Analogy
 - Lets take a restaurant workflow as an example. Imagine there are 3 entity present in our analogy the Customer(Front end), Waiter(REST API), and Chef(Backend)
 - Now the customer(Front end) calls the waiter(rest api) with all the details he wants his/her order suppose to be, now the waiter(rest api) will go to the chef(backend) and tell all the details that the customer(front end) wants his/her order suppose to be and the chef(backend) will now do all the work/logics to serve the customer request but in the process there some restrictions that customer should follow and the chef(backend) will represent that restriction via HTTP statuses. In context REST API acts likes a mediator between Front end and Back end for those two to communication in standard and proper way. You dont want your customer(front end) to directly interact with the chef(back end) right it will just go wrong.

##### Http Status
- Informal response (100 - 199)
- Successful response (200 - 299)
- Redirection response (300 - 399)
- Client error response (400 - 499)
- Server error response (500 - 599)

##### REST API URL Structure
![image](https://github.com/Elleined/rest-api-naming-convention-and-best-practices/assets/111877930/8982e496-d3e3-4b2d-a9d9-023b2ab28dcf)

##### Note: There are 4 ways you can get, post, put, delete a data in REST API 
  1. Path Variable
  2. Query Parameter
  3. Request Body
  4. Http Headers

###### What is Path Variable?
 - Path variable is the dynamic data in your API endpoint and commonly use to determine who is interacting with the server.
 - Example: /users/{id} the /{id} is the path variable 
###### What is Query Parameter 
 - Query parameter is the data needed to properly call the endpoint. It can be required or optional and commonly used for passing small amount of data and can also be used for filtering, sorting and pagination of the resource.
 - Example: /users?name=XYZ&sort=birthDate // All text that comes after the ? is the query parameter just like in calling a method in your programming languange you need to pass all the argument needed to properly call the method in this case is the api endpoint, and the symbol & you can just think of it as a separator or the comma in your method parameter and in this case is the api query parameter.
###### What is Request Body
 - Request Body is used to pass a big set of data and commonly represented as JSON, XML, and CSV.

###### HTTP headers

- HTTP headers let the client and the server pass additional information with an HTTP request or response. An HTTP header consists of its case-insensitive name followed by a colon (:), then by its value. Whitespace before the value is ignored. [[more info about headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)]
- Commonly used for api key authorization for better security when transporting data.

# REST API proper naming conventions and best practices
- REST API notes and Guide for writing proper REST API endpoints using proper naming conventions and best practices

##### Use plurals for resource collections
```
/users ✅
/user ❎
```

##### Specify the resource to access sub collection
```
/users/{id}/transactions
```

##### URI must be noun and avoid using verbs
 - Because using verbs in URI adds verbosity and should be represented via HTTP methods
```
/users/{id} ✅ // means get a specific resource in the collection of user
/users/getById/{id} ❎
```

##### Use HTTP method semantics
  ##### POST: Create a resource
  ##### GET: Retrieve a resource
  ##### PUT: Update the whole resource
  ##### PATCH: Update a specific data in resource
  ##### DELETE: Delete a resource
```
POST /users with request body          // returns the saved resource
GET /users                             // returns list/array of the resource
GET /users/{id}                        // returns the specific resource via id
PUT /users/{id} with request body      // returns the updated resources
PATCH /users/{id} with query parameter // returns the updated resource also
DELETE /users/{id}                     // returns no content http status
```

##### Do not use trailing forward slashes
 - Because every forward slash there should be something that you can do and using forward slash that do nothing is just nonsense
```
/users ✅
/users/ ❎
```

##### Use kebab case and lower-casing
 - To increase readability and scalability
```
/users/{id}/accounts/device-management ✅ // easy to read
/users/{id}/accounts/deviceManagement ❎ // hard to read
```

##### Dont use file extensions in URI
 - Because using file extension in URI is just confusing as hell and just adds in URI length. File extenstion should be in header Content-Type to specify what data that your api consumes and produce.

##### Always enable filtering, sorting, and pagination in your resource collections
```
/users?name=XYZ&sort=registrationDate&page=1&pageSize=5
```

# API Versioning
- API versioning is the practice of transparently managing changes to your API.
- Change is a natural part of API development. Sometimes, developers have to update their API's code to fix security vulnerabilities, while other changes introduce new features or functionality. Some changes do not affect consumers at all, while others, which are known as “breaking changes,” lead to backward-compatibility issues, such as unexpected errors and data corruption. API versioning ensures that these changes are rolled out successfully in order to preserve consumer trust while keeping the API secure, bug-free, and highly performant - [Postman](https://www.postman.com/api-platform/api-versioning/#:~:text=API%20versioning%20is%20the%20process,natural%20part%20of%20API%20development.).

## Standard for naming API Versions
- [SemVer (Semantic Versioning)](http://semver.org/)

### Major: For Whatever changes that causes breaking change.

### Minor: For whenever you add a new features that does not cause breaking change.

### Patch: For bug fixes and minor changes.

```
// Template
MAJOR.MINOR.PATCH

// Example
1.1.3
```

# API Building Steps
1. Model
   - Bidirectional Relationships  
   - PrimaryKeyIdentity class  
   - Proper Spring Data JPA annotation attributes and values
   - Use @SuperBuilder
     
3. Repository
   - Pageable JPQL Query of associated collections in the model
5. DTO
   - Use @SuperBuilder
   - Fields should be strictly identical in model class
   - Onlt the model that owns the @ManyToOne will have the references and the entity owns the OneToMany will not have reference to the list.
   
6. Request
7. Mapper
   - Include all the fields inside the @Mappings
   - Values must be taken from parameter not in a single object.
    
9. Service
   - Adding paging and sorting in all collections fetch methods
   
10. Exception
11. Controller
12. Populator
13. Scheduler
14. Unit Testing
    - [Unit testing in order](https://github.com/Elleined/junit-mockito-notes?tab=readme-ov-file#testing-in-chronological-order)
16. DTO HATEOUS Assembler
17. Postman Endpoints
    - Create a named host-ip-address, host-port, api-context-path, and base-url, where base-url is {{host-ip-address}}:{{host-port}}/{{api-context-path}}.
    - Create separate environment for your git branching commonly is main and dev.
    - Usage of random api the {{$random}}.
18. Caching with redis
20. Create jenkins workflow

# What is HATEOUS
- Hypermedia as the Engine of Application State.
- Makes API self-documenting and discoverable.
- It is a contraint in building RESTful services architecture where states that when you send json response payload in client it should also include related actions making your api self-documenting and the client can explore your api with minimal knowledge in your project.
- Commonly used for retrieving one-to-many, many-to-many or related entity resources in your database because instead of returning a whole bunch of data in one call you provide only the url for that resources for the client to fetch.

## HATEOUS provides
- Freedom to change api only in server side without touching client side api call making both project loosely coupled to each other.
- Fully control what client can do or behave because you are sending the related actions that client can only do.

# What is HyperMedia
- Just a link related to your API.
- Serve as documentation for programmer

# WebMvcLinkBuilder methods
- **linkTo()**: Add related link in representation model.
- **methodOn()**: add related method in linkTo
- **afford()**: add additional related link.

# Representation Model
- **add()**: add link to dto class.
- **addIf()**: add supplied link if guard is true.

# Link methods
- **withSelfRel()**: add the self relationship name.
- **withRel()**: add related relationship name.
- **withTitle()**: add title of the related url.
- **withType()**: add the httpmethod of related url.
- **withMedia**: add the preferred media type payload of related resource. Example "application/json"
- **withHref()**: manually contruct the url link of related resource.

# Hateous links needed in DTO
1. Self links
2. Related button links
3. Many to one relationships links
4. One to many relationships links

# Notes:
- Typically you extend the RepresentationModel class in your DTO classes.
- Only use controller class and methods in WebMvcLinkBuilder static method parameters.
- When you use same related relationship name in different links it will be return as an array under the same name.
- When you supply null in controller class method parameter annotated with @RequestParam and @PathVariable it will produce templated url.
- Final classes return types of controller method should be wrapped around ResponseEntity<Type> if not will throw an exception. Example: String and primitive type Wrapper class.
```
http://localhost:<port>/resource/{pathVariable}/accounts?key1={value1}&key2={value2}
```

# Basic usage of spring hateous
```
// With self reference
dto.add(linkTo(methodOn(controllerClass).controllerClassMethod())
 .withSelfRel("relation-name")
 .withTitle("apiCallTitle")
 .withType("httpAPICallMethod")
)

// With related resource reference
dto.add(linkTo(methodOn(controllerClass).controllerClassMethod())
 .withRel("relation-name")
 .withTitle("apiCallTitle")
 .withType("httpAPICallMethod")
)
```

#### [hateous project code sample](https://howtodoinjava.com/spring/spring-hateoas-tutorial/)

#### [Right way to build API](https://m.youtube.com/watch?v=CVBpYfPKGlE)
