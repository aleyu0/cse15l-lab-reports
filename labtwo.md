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
*Note: <Port_Number> is replaced with a valid integer.*

## Explaination
# Part Two: Debugging methods
## Objective
## Original Code
## Bugs
## Solution
# Part Three: Leanring Achievements
