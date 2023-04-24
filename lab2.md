# Lab report 2 - Daniil Katulevskiy A17481234

Here is my code for StringServer.java:

```java
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class StringSearchHandler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    ArrayList<String> words = new ArrayList<>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "Daniel's search system";

        } else if (url.getPath().equals("/search")) {
            //! SEARCH
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("a")){
                return String.join(", ", words);
            }

            else if (!parameters[0].equals("s")) {
                return "You forgot s= in your request!";
            }

            ArrayList<String> found = new ArrayList<>();
            for (String word : words) {
                if (word.toLowerCase().contains(parameters[1].toLowerCase())) {
                    found.add(word);
                }
            }
            String foundstr = String.join(", ", found);
            return String.format("Results found: %s", foundstr);
        } 

        else if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    words.add(parameters[1]);
                    String allStr = String.join("\n", words);
                    return allStr;
                }
                return "You forgot s= in your request!";
        }
        
        else {
            System.out.println("Path: " + url.getPath());
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new StringSearchHandler());
    }
}
```

The effect of ```add-message``` in query string is to concatenate a new line (\n) and the string after = to the running string, and then respond with the entire string so far.

Query should look like this:

```https://server.domain:port/add-message?s=<string>```

I already ran query ```/add-message?s=Hello```.\
Here are examples of ```add-message``` query usage:

![Image](String-server-2.png)
![Image](String-server-3.png)

