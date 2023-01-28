# Part One: Building a StringServer
## Objective
We were given the task to create a web server named `StringServer` that would keep a list of strings. The user would be able to add strings to that list by sending request via the URI. 
## Code
The webserver is composed of two files: 
* StringServerHandler.java - including `ServerHttpHandler` class (with `handlerRequest` method, `printString` method) and `stringServer` class (with the `main` method).
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
To start the web server we open a new terminal on VS Code in the current working directory. To all classes in the directory, we enter:
```
javac *
```
We then run the program by running the class that contains the main method:
```
java StringServer <Port_Number>
```
*Note: <Port_Number> is replaced with a valid integer. In the case of the example below, port `6565` is used.*

When the program executes, a web server is online. We are given the message in the terminal:
```
Server Started! Visit http://localhost:6565 to visit.
```

We can now head over to our web browser to visit the webserver. 

We start by visiting the web server without adding any queries at the end. 

<img width="600" alt="localhost_no_query" src="https://user-images.githubusercontent.com/83614302/215251981-152c2c84-8ae7-4f35-8f51-756965630389.png">

As you can see our prompt is outputted. This is because handleRequest checks if there are any queries in the URI and if there are any items in the arraylist that was initialised at execution. When there aren't any, the program will output this prompt. If the query was empty and there were items in the arraylist the list will be output it as we will see below. 

The next image shows when we add a few elements to the arraylist through the URI.

<img width="600" alt="query_Cars" src="https://user-images.githubusercontent.com/83614302/215252323-b6ff8f9e-c7bb-43b5-971d-9bbf4920d0cd.png"> <img width="600" alt="query_Trains" src="https://user-images.githubusercontent.com/83614302/215252332-6e17c7dc-a9b6-4ae2-bcb3-1812eca436e8.png"> <img width="600" alt="query_Planes" src="https://user-images.githubusercontent.com/83614302/215252336-5877b3b7-0da4-4703-9a9c-a046946d898c.png">

When the URI is entered, it will be passed to the `handleRequest` method which would first distinguish whether there `/add-message` is the path. If so, the program will make sure that the query is formatted (as in has `?s=`) correctly. Once that is confirmed, the program will add the element in the query to the arraylist. Once that's done, the `handleRequest` method will call the `printString` method with the parameter of the arraylist. This method uses a for-loop to create a string with a new line for each element. This string can then be returned by `handleRequest` to display on screen. 

Finally we can check the URI with no query again. Since there are elements in the arraylist, the program will print the list using the `printString` method.
<img width="597" alt="new_no_query" src="https://user-images.githubusercontent.com/83614302/215252762-ffc9bd8f-6000-4a26-be5d-e7efd213eb24.png">

# Part Two: Debugging methods
## Objective
During the lab session on Wednesday, we were given a set of programs which contained bug in them. Bugs are flaws in the program (logical or syntactical) that produces undesired outputs. The following explain one of the bugs, and the process of ✨ Debugging ✨.
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
Then we make a test method that tests a specific program method. Remember to add a `@Test` before the method to annotate our test method. Using `assertEqual(<ConstructiveMessage>, <ExpectedValue>, <ActualValue>)` we can see if the ourput of our program is what we want! 
*Note: Replace `<ConstructiveMessage>` with a constructive message, `<ExpectedValue>` with the desired value (whether it's an integer, string, or array), and `<ActualValue>` with either a variable or a method that returns a variable.*

To test the `reversed()` method, we used the following tests: 
```
@Test
public void testReversed() {
  int[] input1 = { 3, 5, 9 };
  assertArrayEquals(new int[]{ 9, 5, 3 }, ArrayExamples.reversed(input1));
}
```

## Solution
# Part Three: Leanring Achievements
