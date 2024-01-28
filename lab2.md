# CSE 15L LAB REPORT 2
## TASK 1: Building a ChatServer
### i)The code for the ChatServer:
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
class Handler implements URLHandler{
    ArrayList<String> arr=new ArrayList<>();
    public String handleRequest(URI url){
        if(url.getPath().equals("/add-message")){
            String query=url.getQuery();
            String [] param=query.split("&");
            String messageParam=param[0];
            String userParam=param[1];

            if(messageParam.startsWith("s=") && userParam.startsWith("user=")){
                String message=messageParam.substring(2);
                String user=userParam.substring(5);
                arr.add(user+": "+message);
                return ChatHistory();


            }
        }
        return "404 Not Found!";
        
    }
    public String ChatHistory(){
        String allMessages="";
        for(String s:arr){
            allMessages+=s+"\n";
        }
        return allMessages;
    }
    

}

class ChatServer{
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
### ii)Output 1:
![Code Output1](https://github.com/Mallika1405/cse15l-lab-reports/blob/main/Screenshot%202024-01-27%20at%201.25.34%20PM.png)

#### Q1)What methods in your code are called?
My code uses 3 methods:
- `handleRequest`:This method is in the Handler class and is called when the server receives a request to the /add-message path.
- `ChatHistory`:This method is in the Handler class and is called within handleRequest to construct and return the full chat history after a new message is added.
- `main`:This method is in the ChatServer class andis the entry point of the ChatServer program. It is called when the server application is started.

#### Q2)What are the relevant arguments to those methods, and the values of any relevant fields of the class?
- For `handleRequest`(URI url):The URI url part takes in a URL as the argument. The URL in this case would be https://0-0-0-0-4001-ptlc58ci4hbh3djvp2vh064cj4.us.edusercontent.com/add-message?s=Hello&user=jpolitz. 
- For `ChatHistory()`: There are no arguments for this method. It iterates over the arr ArrayList filed to build the chat history. 
- For `main(String [] args)`: This method takes in the arguments from the command-line where `args[0]` is expected to be the port number on which the Server should listen.

#### Q3)How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
In the `Handler` class, the `arr` ArrayList field is initially empty but upon receving the request, the `handleRequest` method parses the query and constructs the message `"jpolitz: Hello"` and adds it to the ArrayList `arr`. 
When it comes to local variables, the following variables get updated:
- `query`:This variable will hold the full query string `s=Hello&user=jpolitz` extracted from the url.
- `param`:This array will be populated with the split results of the query string `["s=Hello", "user=jpolitz"]`.
- `messageParam`:This variable will hold the message part of the query, `s=Hello`.
- `userParam`: This variable will hold the user part of the query, `user=jpolitz`.
- `message`:After extracting the substring from messageParam, this will hold `Hello`.
- `user`:After extracting the substring from userParam, this will hold `jpolitz`.
- `allMessages`: This variable is in the ChatHistory method and is a string that starts as an empty string and accumulates all chat messages from the ArrayList `arr`. After the request, it will hold `jpolitz: Hello\n`.
In the `ChatServer` class, the main method accepts the port number as `args[0]`.

### iii)Output 2:
![Code Output2](https://github.com/Mallika1405/cse15l-lab-reports/blob/main/Screenshot%202024-01-27%20at%204.49.59%20PM.png)

#### Q1)What methods in your code are called?
- `handleRequest`:This method is in the Handler class and is called when the server receives a request to the /add-message path.
- `ChatHistory`:This method is in the Handler class and is called within handleRequest to construct and return the full chat history after a new message is added.
- `main`:This method is in the ChatServer class andis the entry point of the ChatServer program. It is called when the server application is started.

#### Q2)What are the relevant arguments to those methods, and the values of any relevant fields of the class?
- For `handleRequest`(URI url):The URI url part takes in a URL as the argument. The URL in this case would be https://0-0-0-0-4000-nou3pmcv69uk2c3jq74t5i6btk.us.edusercontent.com/add-message?s=Hi!How%20are%20you&user=Mallika
- For `ChatHistory()`: There are no arguments for this method. It iterates over the arr ArrayList filed to build the chat history. 
- For `main(String [] args)`: This method takes in the arguments from the command-line where `args[0]` is expected to be the port number on which the Server should listen.

#### Q3)How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
In the `Handler` class, the `arr` ArrayList field initially has the previous message but upon receving the request, the `handleRequest` method parses the query and constructs the message `"Mallika: Hi!How are you"` and adds it to the ArrayList `arr`. 
When it comes to local variables, the following variables get updated:
- `query`:This variable will hold the full query string `s=Hi%20How%20are%20you&user=Mallika` extracted from the url.
- `param`:This array will be populated with the split results of the query string `["s=Hi%20How%20are%20you", "user=Mallika]`.
- `messageParam`:This variable will hold the message part of the query, `s=Hi%20How%20are%20you`.
- `userParam`: This variable will hold the user part of the query, `user=Mallika`.
- `message`:After extracting the substring from messageParam, this will hold `Hi!How+are+you`.
- `user`:After extracting the substring from userParam, this will hold `Mallika`.
- `allMessages`: This variable is in the ChatHistory method and is a string that starts as an empty string and accumulates all chat messages from the ArrayList `arr`. After the request, it will hold `jpolitz: Hello\n`, `Mallika: Hi!How+are+you`.
In the `ChatServer` class, the main method accepts the port number as `args[0]`. This value won't change because the port will be the same until it is changed in the terminal.

## TASK 2: SSH Key

### i)Private Key using ls
![Private Key](https://github.com/Mallika1405/cse15l-lab-reports/blob/main/Screenshot%202024-01-27%20at%205.11.03%20PM.png)

### ii)Public Key using ls
![Public Key](https://github.com/Mallika1405/cse15l-lab-reports/blob/main/Screenshot%202024-01-27%20at%205.12.49%20PM.png)

### iii) ieng without being asked for a password
![No password](https://github.com/Mallika1405/cse15l-lab-reports/blob/main/Screenshot%202024-01-27%20at%202.14.04%20PM.png)

## TASK 3: What I learnt this week









