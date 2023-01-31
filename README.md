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
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/122571192/215664533-b8dd5371-101f-4b97-b698-5e598f3a3a18.png">


- Second, after using /add-message using the code I wrote, I get two outputs. 
- First one is using /add-message?s=Hello
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/122571192/215665882-11e2ca06-8e62-410b-8d10-e3b4b7c7bbd0.png">

- In this screanshot, we are adding a string, which is "Hello" here, and the methods that were called in my code is, handleRequest. 
- The relevant arguments are the url, which is the name of the web we are creating. After that the string we are adding. 
- We already changed the value from int (which is the one we had in the lab), to a value of String, so the web accepts a string. Also, if we try to write a number, that number will be treated as a string, and not like am integer, whihc means we will not be able to write a number and increase it. 


- Second screenshot, was for using /add-message?s=How are you, and we get. 
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/122571192/215666911-ad5398a8-9c19-48df-8b02-25808cd4a09d.png">
- In this screanshot, we are adding another string to the one we had originally, which is "How are you" here, and the methods that were called in my code is, handleRequest. 
- However, we are making sure here that we are only adding and not replacing the previous method, as well as adding another line. 
- The relevant arguments are the url, which is the name of the web we are creating. After that the string we are adding. 
- Also, here seem reasning for the first picture applies here. 
-

**Part 2**
- Choose one of the bugs from lab 3


**Part 3**
- I find it very intersting that we can write a web server, and we can name it what we want. Also, I learned how to make one of either strings or numbers. 
- Also, I leanred how to to compile and run JUnit since it is an external library.
- I also leanred that using mac commands on a windows gives errors and vice versa because the command set for each operating systems is different. 



