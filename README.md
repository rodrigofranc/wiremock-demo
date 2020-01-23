### Introduction

>**WireMock**  is a library for stubbing and mocking web services. It constructs a HTTP server that we could connect to as we would to an actual web service.
When a  [WireMock](http://wiremock.org/)  server is in action, we can set up expectations, call the service, and then verify its behaviors.

#### Necessary files

To run our server, we need the standalone JAR provided by Wiremock, we can download this file with the following command:

` wget http://repo1.maven.org/maven2/com/github/tomakehurst/wiremock-standalone/2.5.1/wiremock-standalone-2.5.1.jar `

For test and run our server, we can do:

`java -jar wiremock-standalone-2.5.1.jar `

#### Requests and response mapping

Once we have raised the server, we will see two new directories: **mapping** and **__files**

- mapping: contains files in JSON format with the combinations of request you attend and the responses you have to give.
- __files: Contains the files with the content of the responses, and which are referenced from the mappings.

To create our first mapping, we add a json file in mapping folder with the following content:

````json
{
    "request": {
        "method": "GET",
        "url": "/movies"
    },
    "response": {
        "status": 200,
        "bodyFileName": "response_ok_movies.json",
        "headers": {
			"Content-Type": "application/json"
	    }
	}
}
````

The `bodyFileName` field indicates the path to the `json` format file in the __files directory, add the file `response_ok_movies.json` with the following content:

```json
{
	"movies": [{
		"id": "1",
		"title": "Inception",
		"year": 2010,
		"genre": "Action, Adventure, Sci-Fi, Thriller",
		"director":"Christopher Nolan"
	},
	{
		"id": "2",
		"title": "Matrix",
		"year": 1999,
		"genre": "Action, Drama, Fantasy, Thriller",
		"director": "Lana Wachowski, Lilly Wachowski"
	}]
}
```
In this mapping we are indicating a request of type **GET** and status code **200** to the path `/movies`, which will response with a list of movies.

For each mapping we would like to have, it will only be necessary to add our json file into the mapping directory.

### Request Matching

Wiremock supports matching of requests to stubs and verification queries using the following attributes:

-   URL
-   HTTP Method
-   Query parameters
-   Headers
-   Basic authentication (a special case of header matching)
-   Cookies
-   Request body
-   Multipart/form-data

See this link for full description about [Request Matching](http://wiremock.org/docs/request-matching/)
