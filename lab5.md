# CSE 15L LAB REPORT 3
## PART 1-DEBUGGING SCENARIO
**Anakin Skywalker**: I'm trying to run the follwing command:
```
coder@a50d74bf837e:~$ javac Server.java Handler.java ChatServer.java
```
I'm getting the following error:
```
error: file not found: Server.java
Usage: javac <options> <source files>
use --help for a list of possible options
```
Could you please help me fix it?

**Obi-Wan Kenobi**: There may be a few things wrong with what you have done. Firstly, do you think you're in the correct directory? Do you think you need to use the `cd` command somewhere? Secondly, do you think you can make use of `shell` files somewhere? 

**Anakin Skywalker**: Yes! I may have forgotten to `cd` into the `chat-server` directory and run the `test.sh` file using `bash` command. Here are my commands:
```
coder@a50d74bf837e:~$ cd chat-server/
```
```
coder@a50d74bf837e:~/chat-server$ bash test.sh
```
This is what I got as the output:
```
JUnit version 4.13.2
..E.
Time: 0.141
There was 1 failure:
1) handleRequest2(HandlerTests)
org.junit.ComparisonFailure: expected:<[edwin: happy friday!

]> but was:<[Invalid parameters: name=edwin&message=happy friday!]>
        at org.junit.Assert.assertEquals(Assert.java:117)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at HandlerTests.handleRequest2(HandlerTests.java:22)

FAILURES!!!
Tests run: 3,  Failures: 1
```

**Obi-Wan Kenobi**: Yes! This means that there is an error somewhere in your file. Can you find the error now?

**Anakin Skywalker**: I am not being able to find the error in the `ChatServer` file. The code seems correct with me. Do you think you could help me please? This is the code in the `ChatServer.java` file:
```
import java.io.IOException;
import java.net.URI;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;

class ChatHandler implements URLHandler {
  String chatHistory = "";

  public String handleRequest(URI url) {

    // expect /chat?user=<name>&message=<string>
    if (url.getPath().equals("/chat")) {
      String[] params = url.getQuery().split("&");
      String[] shouldBeUser = params[0].split("=");
      String[] shouldBeMessage = params[1].split("=");
      if (shouldBeUser[0].equals("user") && shouldBeMessage[0].equals("message")) {
        String user = shouldBeUser[1];
        String message = shouldBeMessage[1];
        this.chatHistory += user + ": " + message + "\n\n";
        return this.chatHistory;
      } else {
        return "Invalid parameters: " + String.join("&", params);
      }
    }
    // expect /retrieve-history?file=<name>
    else if (url.getPath().equals("/retrieve-history")) {
      String[] params = url.getQuery().split("&");
      String[] shouldBeFile = params[0].split("=");
      if (shouldBeFile[0].equals("file")) {
        String fileName = shouldBeFile[1];
        // String fileName = shouldBeFileName[0]; // bug4: should be shouldBeFile[1]
        ChatHistoryReader reader = new ChatHistoryReader();
        try {
          String[] contents = reader.readFileAsArray("chathistory/" + fileName);
          for (String line : contents) {
            this.chatHistory += line + "\n\n";
          }
        } catch (IOException e) {
          System.err.println("Error reading file: " + e.getMessage());
        }
      }
      return this.chatHistory;
    }
    // expect /save?name=<name>
    else if (url.getPath().equals("/save")) {
      String[] params = url.getQuery().split("&");
      String[] shouldBeFileName = params[0].split("=");
      if (shouldBeFileName[0].equals("name")) {
        File directory = new File("chathistory");
        File file = new File(directory, shouldBeFileName[1]);

        try (BufferedWriter writer = new BufferedWriter(new FileWriter(file))) {
          writer.write(this.chatHistory);
          return "Data written to " + shouldBeFileName[1] + "in 'chat-history' folder.";
        } catch (IOException e) {
          e.printStackTrace();
          return "Error: Something wrong happen during file save, check StackTrace";
        }
      }
    }

    return "404 Not Found";
  }
}

class ChatServer {
  public static void main(String[] args) throws IOException {
    int port = Integer.parseInt(args[0]);
    Server.start(port, new ChatHandler());
  }
}
```

**Obi-Wan Kenobi**: The code in the file seems correct. Have you checked your test methods?

**Anakin Skywalker**: No I did not think of that! I checked my test files and it appears there was an error in the second test method `handleRequest2`. This is the code of the test methods.
```
import static org.junit.Assert.*;
import org.junit.*;
import java.net.URI;

public class HandlerTests {
  @Test
  public void handleRequest1() throws Exception {
    ChatHandler h = new ChatHandler();
    String url = "http://localhost:4000/chat?user=joe&message=hi";
    URI input = new URI(url);
    String expected = "joe: hi\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequest2() throws Exception {
    ChatHandler h = new ChatHandler();
    // NOTE: %20 is the way to put a space in the parameters of a URL
    String url = "http://localhost:4000/chat?name=edwin&message=happy%20friday!";
    URI input = new URI(url);
    String expected = "edwin: happy friday!\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequestMulti() throws Exception {
    ChatHandler h = new ChatHandler();
    String url1 = "http://localhost:4000/chat?user=onat&message=good%20luck";
    String url2 = "http://localhost:4000/chat?user=edwin&message=with%20your%20demo!";
    URI input1 = new URI(url1);
    URI input2 = new URI(url2);
    String expected = "onat: good luck\n\nedwin: with your demo!\n\n";
    h.handleRequest(input1);
    assertEquals(expected, h.handleRequest(input2));
  }
}
```
I accidentally put the URL as `"http://localhost:4000/chat?name=edwin&message=happy%20friday!"` where I put `name=edwin` instead of `user=edwin`. The correct URL was supposed to be `"http://localhost:4000/chat?user=edwin&message=happy%20friday!"`. This is the corrected code:
```
import static org.junit.Assert.*;
import org.junit.*;
import java.net.URI;

public class HandlerTests {
  @Test
  public void handleRequest1() throws Exception {
    ChatHandler h = new ChatHandler();
    String url = "http://localhost:4000/chat?user=joe&message=hi";
    URI input = new URI(url);
    String expected = "joe: hi\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequest2() throws Exception {
    ChatHandler h = new ChatHandler();
    // NOTE: %20 is the way to put a space in the parameters of a URL
    String url = "http://localhost:4000/chat?user=edwin&message=happy%20friday!";
    URI input = new URI(url);
    String expected = "edwin: happy friday!\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequestMulti() throws Exception {
    ChatHandler h = new ChatHandler();
    String url1 = "http://localhost:4000/chat?user=onat&message=good%20luck";
    String url2 = "http://localhost:4000/chat?user=edwin&message=with%20your%20demo!";
    URI input1 = new URI(url1);
    URI input2 = new URI(url2);
    String expected = "onat: good luck\n\nedwin: with your demo!\n\n";
    h.handleRequest(input1);
    assertEquals(expected, h.handleRequest(input2));
  }
}
```
This was the output I got:
```
...
Time: 0.296

OK (3 tests)
```
The tests passed successfully! Thank you so much Obi-Wan!

**Obi-Wan Kenobi**: I'm glad it worked Anakin! Would you mind sending me your file structure?

**Anakin Skywalker**: Sure. Here is my file structure:
```
coder@a50d74bf837e:~$ ls -R
.:
chat-server       root-output.txt       test-success-output.txt
query-output.txt  test-fail-output.txt

./chat-server:
ChatHandler.class        HandlerTests.class       session.log
chathistory              HandlerTests.java        test-fail-output.txt
ChatHistoryReader.class  lib                      test.sh
ChatHistoryReader.java   Server.class             URLHandler.class
ChatServer.class         ServerHttpHandler.class
ChatServer.java          Server.java

./chat-server/chathistory:
chathistory1.txt  chathistory2.txt  chathistory3.txt

./chat-server/lib:
hamcrest-core-1.3.jar  junit-4.13.2.jar
```

**Obi-Wan Kenobi**: Thank you Anakin!

## PART 2-REFLECTION
In the second half of the quarter I learnt a lot about `vim`. Initially I thought it was inconvenient to use but as I went deeper and learnt more about the different commands you could use, I started enjoying using the `vim` text editor! I also learnt a lot about using `jdb` and different commands I could use to debug my program. This process made debugging a lot easier. However, my favorite part about the second half of the quarter was learning how `gradescope` works and how our code gets checked for errors!
