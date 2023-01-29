# Part One: Building a StringServer
## Objective
We were given the task to create a web server named `StringServer` that would keep a list of strings. The user would be able to add strings to that list by sending request via the URI. 
## Code
The webserver is composed of two files: 
* StringServerHandler.java - including `StringHttpHandler` class (with `handlerRequest` method, `printString` method) and `stringServer` class (with the `main` method).
  ```
  import java.io.IOException;
  import java.net.URI;
  import java.util.ArrayList;

  public class StringServerHandler implements URLHandler{

      ArrayList<String> stringArray = new ArrayList<String>();

      public String handleRequest (URI url){
          String toAdd = null;

          if (url.getPath().equals("/add-message")){
              if (url.getQuery()!=null){
                  String[] parameters = url.getQuery().split("=");
                  if (parameters[0].equals("s")){
                      toAdd = (String) parameters[1];
                  }
              }
              if (toAdd != null){
                  stringArray.add(toAdd);
                  return printString(stringArray);
              }
          }

          else if (stringArray.isEmpty()){
              return "The list is currently empty. :( \nTo add message, type a message after \"add-message?s=\" in the URL.";
          }

          return printString(stringArray);
      }

      public String printString(ArrayList<String> stringArray){
          String result = "";
          for (int i = 0; i<stringArray.size(); i++){
              result = result + stringArray.get(i) + "\n";
          }
          return result;
      }

  }

  class StringServer {
      public static void main(String[] args) throws IOException {
          if(args.length == 0){
              System.out.println("Missing port number! Try any number between 1024 to 49151");
              return;
          }

          int port = Integer.parseInt(args[0]);

          Server.start(port, new StringServerHandler());
      }
  }
  ```
*  Server.java - composed of `URLHandler` interface, `ServerHttpHandler` class and the `Server` class.
    ```
    // A simple web server using Java's built-in HttpServer

    // Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

    import java.io.IOException;
    import java.io.OutputStream;
    import java.net.InetSocketAddress;
    import java.net.URI;
    import com.sun.net.httpserver.HttpExchange;
    import com.sun.net.httpserver.HttpHandler;
    import com.sun.net.httpserver.HttpServer;

    interface URLHandler {
        String handleRequest(URI url);
    }

    class ServerHttpHandler implements HttpHandler {
        URLHandler handler;
        ServerHttpHandler(URLHandler handler) {
          this.handler = handler;
        }
        public void handle(final HttpExchange exchange) throws IOException {
            // form return body after being handled by program
            try {
                String ret = handler.handleRequest(exchange.getRequestURI());
                // form the return string and write it on the browser
                exchange.sendResponseHeaders(200, ret.getBytes().length);
                OutputStream os = exchange.getResponseBody();
                os.write(ret.getBytes());
                os.close();
            } catch(Exception e) {
                String response = e.toString();
                exchange.sendResponseHeaders(500, response.getBytes().length);
                OutputStream os = exchange.getResponseBody();
                os.write(response.getBytes());
                os.close();
            }
        }
    }

    public class Server {
        public static void start(int port, StringServerHandler handler) throws IOException {
            HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

            //create request entrypoint
            server.createContext("/", new ServerHttpHandler(handler));

            //start the server
            server.start();
            System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
        }
    }

    ```
## Running
To start the web server we open a new terminal on VS Code in the current working directory. To compile all classes in the directory, we enter:
```
javac *
```
We then run the program by running the class that contains the main method:
```
java StringServer <Port_Number>
```
*Note:* `<Port_Number>` *is replaced with a valid integer. In the case of the example below, port* `6565` *is used.*

When the program executes, a web server is online. We are given the message in the terminal:
```
Server Started! Visit http://localhost:6565 to visit.
```
At this point some values have been set, and will not change until the end of the session. The URI, along with the port number are set when executed, which would allow the user to access this server whenever the local host is and the port number is entered (as long as the program is running). 


We can now head over to our web browser to visit the web server. 

We start by visiting the web server without adding any queries at the end. 

<img width="600" alt="localhost_no_query" src="https://user-images.githubusercontent.com/83614302/215251981-152c2c84-8ae7-4f35-8f51-756965630389.png">

As you can see, our prompt is outputted. This is because `handleRequest` checks if there are any queries in the URI and whether there are any items in the arraylist. When there aren't any, the program will output this prompt. If the query was empty and there were items in the arraylist the list will be outputed as we will see below. 

The following images show what happens when we add a few elements to the arraylist through the URI.

<img width="600" alt="query_Cars" src="https://user-images.githubusercontent.com/83614302/215252323-b6ff8f9e-c7bb-43b5-971d-9bbf4920d0cd.png"> <img width="600" alt="query_Trains" src="https://user-images.githubusercontent.com/83614302/215252332-6e17c7dc-a9b6-4ae2-bcb3-1812eca436e8.png"> <img width="600" alt="query_Planes" src="https://user-images.githubusercontent.com/83614302/215252336-5877b3b7-0da4-4703-9a9c-a046946d898c.png">

When the URI is entered, it will be passed to the `handleRequest` method which would first distinguish whether there is a `/add-message` path. If so, the program will make sure that the query is formatted (as in has `?s=`) correctly. Once that is confirmed, the program will add the element in the query to the arraylist. Once that's done, the `handleRequest` method will call the `printString` method with the parameter of the arraylist. This method uses a for-loop to create a string with a new line for each element. This string can then be returned by `handleRequest` to be display on screen. The queries are values that can be changed everytime the user sends a new request, however, the arraylist keeps an record of all the string values inputted as it is an instance variable. 

Finally we can check the URI with no query again. Since there are elements in the arraylist, the program will print the list using the `printString` method.

<img width="597" alt="new_no_query" src="https://user-images.githubusercontent.com/83614302/215252762-ffc9bd8f-6000-4a26-be5d-e7efd213eb24.png">

# Part Two: Debugging methods
## Objective
During the lab session on Wednesday, we were given a set of programs which contained bugs in them. Bugs are flaws in the program (logical or syntactical) that produces undesired outputs. The following explain one of the bugs, and the process of ✨Debugging✨.
## Original Code
```
// Returns a *new* array with all the elements of the input array in reversed
// order
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}
```
## Bugs
Bugs may not be easy to spot, often there are no errors. They just happen quietly until you realise that the output isn't what you desired. So instead of getting to that point, we make a tester file. We will use JUnit to test this piece of code. We create a file called `ArrayTester.java` and import the following:
```
import static org.junit.Assert.*;
import org.junit.*;
```
Then we make a test method that tests a specific program method. Remember to add a `@Test` before the method to annotate our test method. Using `assertEquals(<ConstructiveMessage>, <ExpectedValue>, <ActualValue>)` we can see if the output of our program is what we want! 
*Note: Replace* `<ConstructiveMessage>` *with a constructive message,* `<ExpectedValue>` *with the desired value (whether it's an integer, string, or array), and* `<ActualValue>` *with either a variable or a method that returns a variable.*

To test the `reversed()` method, we used the following tests: 
```
@Test
public void testReversed() {
  int[] input1 = { 3, 5, 9 }; // failure inducing input
  int[] input2 = { 0, 0, 0 }; // non failure inducing input
  assertArrayEquals(new int[]{ 9, 5, 3 }, ArrayExamples.reversed(input1)); // failure inducing input
  assertArrayEquals(new int[]{ 0, 0, 0 }, ArrayExampls.reversed(input2)); // non failure inducing input
}
```

<img width="600" alt="Screen Shot 2023-01-29 at 12 10 33 PM" src="https://user-images.githubusercontent.com/83614302/215353230-74915b6f-5707-474a-9c8c-1733576448d5.png">


The test revealed that the `reverse` method wasn't outputting what it was supposed to. Instead of `9` as the first element, it got `0`. Given this, we return to the code and review it. After a scan, or if it's not visible yet, a trace using the same data set, and we find the issue. 

## Solution
<img width="600" alt="Screen Shot 2023-01-25 at 3 32 13 PM" src="https://user-images.githubusercontent.com/83614302/215253967-fdeb192e-2923-4a62-b043-a8c8559dcd8e.png">

The image above shows what was changed to fix the bug. The parts highlighted in red is what was removed and the parts in green are the lines rewritten. The issue with the previous code is that it was assigning the inputted array's element with elements in the `newArray` which results to an array with `0`s only. Furthermore, the modified array wasn't even returned/saved. To fix this bug, we switched the positions of the arrays and made the old array the new array at the very end. 

This would give us success in the test. 

<img width="600" alt="Screen Shot 2023-01-29 at 12 13 48 PM" src="https://user-images.githubusercontent.com/83614302/215353395-532cf4b1-5a0c-43fb-ad99-1d306bf5fed2.png">


# Part Three: Learning Achievements
In weeks 2 and 3, I learned the following in the CSE 15L course:
* The fundamentals of URLs:
  * HTTP(S) URLs = the protocol in which the web browser will use to view the content
  * Domain = the party that hosts the server `domain.com`
  * Path = allows for navigation within the server `/finder`
  * Query = allows for specific requests for the server `?q=CSE15L`
  * Anchor = navigates to a part/fragment of a page `#about-us`
* How to copy files on local machine to the remote ieng6 machines using `scp`
* How to clone git repositories `git clone <URL from github>` OR VS Code "clone repository" OR using Github Desktop
* Steps to set up a web server
* Testing and debugging

The lectures and labs have been very interesting and very intuitive. Enjoying the course so far! 

<sub><sup>A note to myself, ALWAYS COMMIT CHANGES every few minutes. This is the second time writing this whole lab report because the previous version got deleted when the page automatically refreshed 💀</sup></sub>
