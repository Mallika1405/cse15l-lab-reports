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

