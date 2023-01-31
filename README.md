# cse15l-lab-reports
# **Servers and Bugs**
**Part1**
- First, I wrote a web server called StringServer, and below is the code of StringServer file. 

import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    //int num = 0;
    String name = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "StringServer:";
        } 
        /*else if (url.getPath().equals("/increment")) {
            num += 1;
            return String.format("Number incremented!");
        } */
        else {
            System.out.println("Pzath: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    name += parameters[1]+"\n";
                    //return String.format("Number increased by %s! It's now %d", parameters[1], num);
                    return name;
                }
            }
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

        Server.start(port, new Handler());
    }
}

- Also, here is a screenshor of the code as well. 
<img width="568" alt="image"https://github.com/AyahNasser/cse15l-Lab-report2.git">

