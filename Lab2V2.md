1.
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String chat = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return chat;
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s") && parameters[1].contains("user")) {
                    chat = chat + String.format("%1$s: %2$s \n", parameters[2], parameters[1].substring(0, parameters[1].length() - 5));
                }

                return chat;

            }
            return "404 Not Found!";
        }
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```
![image](https://github.com/TeddyNguyen150/CSE15LLab2V2/assets/156158048/51142424-01ed-47b9-a524-a29d665b5634)
The handleRequest method is called, and the URI arguement provides both the user and the string needed for the chat server. 
For this request, the URI class is used in order to get strings to put in the chat server.

![image](https://github.com/TeddyNguyen150/CSE15LLab2V2/assets/156158048/54b16858-0972-4177-91d1-96a6eb60a36a)
The handleRequest method is called again, but this time a new line is formed because a new line was formed last time the handleRequst method was called.

2.
![image](https://github.com/TeddyNguyen150/CSE15LLab2V2/assets/156158048/b614a469-fd51-4811-a02a-884015f00865)

![image](https://github.com/TeddyNguyen150/CSE15LLab2V2/assets/156158048/cb44172f-4f93-4dc4-be29-28ca9e283204)

![image](https://github.com/TeddyNguyen150/CSE15LLab2V2/assets/156158048/050fd4d5-78ea-4b91-95e2-2948e938c5e0)


3.
I learned that URLs aren't as complicated as I initially thought, it's just the hash codes that is just a bit confusing.
I also learned that it's pretty easy to connect to a remote server, given that it's already set up.
