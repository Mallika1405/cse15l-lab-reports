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
**Anakin Skywalker**: Yes! I forgot I had to `cd` into the `chat-server` directory and run the `test.sh` file using `bash` command. Here are my commands:
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
