# cse15l-lab-reports
# **Servers and Bugs**
**Part1**
- First, I wrote a web server called StringServer, and below is the code of StringServer file. 

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    

    String name = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "StringServer:";
        } 
      
        else {
            System.out.println("Pzath: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    name += parameters[1]+"\n";
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
````

- Second, after using ``` /add-message ``` using the code I wrote, I get two outputs. 
- First one is using ```` /add-message?s=Hello ````
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/122571192/215665882-11e2ca06-8e62-410b-8d10-e3b4b7c7bbd0.png">

- In this screenshot, we are adding a string, which is "Hello" here, and the methods that were called in my code is, handleRequest. 
- The relevant arguments are the url, which is the name of the web we are creating. After that the string we are adding. 
- We already changed the value from int (which is the one we had in the lab), to a value of String, so the web accepts a string. The code will check the url, and when it finds the /add key word, it will add the string (message) to the existing array as a new element. Also, if we try to write a number, that number will be treated as a string, and not like an integer, which means we will not be able to write a number and increase it. 


- Second screenshot, was for using ```/add-message?s=How are you```, and we get. 
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/122571192/215666911-ad5398a8-9c19-48df-8b02-25808cd4a09d.png">
- In this screenshot, we are adding another string to the one we had originally, which is "How are you" here, and the methods that were called in my code is, handleRequest. 
- However, we are making sure here that we are only adding and not replacing the previous method, as well as adding another line. 
- The relevant arguments are the url, which is the name of the web we are creating. It will add the string (message) to teh array again as a new element of the array, which means it will add an index for this new element.The same reasoning for the first picture applies here. 


**Part 2**
- **Bug in Array reversed and reversedInPlace**
- The code of failure-inducing input for the buggy program

````
public void testReverseInPlace() {

    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{3}, ArrayExamples.reversed(input1));
    
	} 
 ````
    


- The code of input that doesn’t induce a failure:

````
public void testReverseInPlace() {

    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{3},(input1));
    
}

`````

- The symptom, as the output of running the tests:
- <img width="996" alt="Screenshot 2023-02-13 at 5 22 06 PM" src="https://user-images.githubusercontent.com/122571192/218613777-78523458-95e5-418c-851a-21251d157994.png">

- The bug before: 
- the reverseInPlace method:

````

static void reverseInPlace(int[] arr) {

    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }

  }
 ````
  
 - The bug of the reverse Method:

````
static int[] reversed(int[] arr) {


    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

`````

- After Fixing the reverseInPlace method:

```
  static void reverseInPlace(int[] arr) {
   
    for(int i = 0; i < arr.length /2; i++) {
       
      int j;
      j = arr[i];
      arr[i] = arr[arr.length - i -1];
      arr[arr.length - i - 1] = j;
    }
  }
  
  ```
  
  
- After Fixing the reversed method:

````
 static int[] reversed(int[] arr) {

    int[] newArray = new int[arr.length];
    int j = arr.length;
    for(int i = 0; i < arr.length; i ++) {
      
      newArray[j-1] = arr[i];
      j = j-1;
    }
    return newArray;
    
  }
  ````
  
  - Briefly describe why the fix addresses the issue.
  - For example, in the reverse method the new array created was never filled with the values from the original array. However, in order for us to fix that we first filled the new array created with the values from the previous one. Then we stored the length of the original array in a variable to be able to add the last element in the array later. We started filling the new array from end to begining by using (j-1), and j is the length of the original array, and to get to the last element we need to substract one.  



**Part 3**
- I find it very intersting that we can write a web server, and we can name it what we want. Also, I learned how to make one of either strings or numbers. 
- Also, I leanred how to to compile and run JUnit since it is an external library.
- I also leanred that using mac commands on a windows gives errors and vice versa because the command set for each operating systems is different. 



