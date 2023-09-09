# What is REST API
 - Is a stateless tranfer protocol that uses HTTP method to interact with the server. meaning the client should pass all the required data needed to call the server via api endpoint without the client or the backend maintain some state to interact to each other example using HTTPSession or cookies.

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

##### Note: There are 3 ways you can get, post, put, delete a data in REST API 
  1. Path Variable
  2. Query Parameter
  3. Request Body

###### What is Path Variable?
 - Path variable is the dynamic data in your API endpoint and commonly use to determine who is interacting with the server.
 - Example: /users/{id} the /{id} is the path variable 
###### What is Query Parameter 
 - Query parameter is the data needed to properly call the endpoint. It can be required or optional and commonly used for passing small amount of data and can also be used for filtering, sorting and pagination of the resource.
 - Example: /users?name=XYZ&sort=birthDate // All text that comes after the ? is the query parameter just like in calling a method in your programming languange you need to pass all the argument needed to properly call the method in this case is the api endpoint, and the symbol & you can just think of it as a separator or the comma in your method parameter and in this case is the api query parameter.
###### What is Request Body
 - Request Body is used to pass a big set of data and commonly represented as JSON, XML, and CSV.

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
POST /users with request body
GET /users
GET /users/{id}
PUT /users/{id} with request body
PATCH /users/{id} with request params
DELETE /users/{id}
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
 
