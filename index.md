# CSE 15L LAB REPORT 1  
## 1)Using the `cd` command
### i)Using `cd` with no arguments
When I ran `cd` with no arguments, using the code below,
This is a test

```
[user@sahara ~]$ cd
```
I got the following output.
```
[user@sahara ~]$
```
Working directory: The working directory was the `home` directory, represented by `~`.

Explanation: When `cd` is run without any arguments, it changes to the `home` directory. In this case, it was already in the `home` directory and hence it just remained in the `home` directory in the output.

Error: This is not an error. 

### ii)Using `cd` with a directory as an argument
When I ran `cd` with a directory as an argument using the code below, 
```
[user@sahara ~]$ cd lecture1
```
I got the following output,
```
[user@sahara ~/lecture1]$
```
Working directory: The working directory when the command was entered was the `home` directory, represented by `~`. When the command was entered the working directory was switched to the `lecture1` directory. 

Explanation: The `cd` command with a directory as the argument, changes the working directory to the specified directory, which in this case, is `lecture1`. 

Error: This is not an error. 

### iii)Using `cd` with a file as an argument
When I ran `cd` with a file as an argument using the code below, 
```
[user@sahara ~/lecture1]$ cd Hello.java
```
I got the following output,
```
bash: cd: Hello.java: Not a directory
```
Working directory: The working directory in this case was the `lecture1` directory. 

Explanation: `cd` stands for Change Directory. As the name suggests, the command `cd` is used to change directories, not files. Hence when the name of a file is entered as an argument, it results in an error. 

Error: This results in an error because `cd` is used to change directories and not files. 

## 2)Using the `ls` command
### i)Using the `ls` command with no arguments
When I ran `ls` with no arguments using the code below, 
```
[user@sahara ~]$ ls
```
I got the following output, 
```
cse15l-lab-reports  lecture1
```
Working directory: The working directory in this case was the `home` directory, represented by `~`. 

Explanation: The command `ls` lists the contents(files and directories) of the current directory and in this case, it lists the folders present in the `home` directory. 

Error: This is not an error. 

### ii)Using `ls` with a directory as an argument
When I ran the `ls` command with a directory as an argument using the code below, 
```
[user@sahara ~]$ ls lecture1
```
I got the following output, 
```
Hello.class  Hello.java  messages  README
```
Working directory: In this case the working directory was the `home` directory. 

Explanation: The command `ls` lists the contents of the directory passed in as the argument. In this case, the directory `lecture1` was passed in as the argument, and hence it displayed the files present in the `lecture1` directory. 

Error: This is not an error. 

### iii)Using `ls` with a file as an argument
When I ran the `ls` command with a file as an argument using the code below, 
```
[user@sahara ~]$ cd lecture1
```
I got the following output, 
```
Hello.java
```
Working directory: The working directory was the `lecture1` directory. 

Explanation: The `ls` command followed by a file name will list that file if it exists in the current working directory. Since `Hello.java` is listed as the output, it confirms that the file is present in the `lecture1` directory. The command executed successfully and the output is simply the confirmation that the file exists.

Error: This is not an error. 

## 3)Using the `cat` command
### i)Using the `cat` command with no arguments
When I ran the `cat` command with no arguments using the code below, 
```
[user@sahara ~/lecture1]$ cat
```
I got the following output, 
```
hello
hello
```
Working directory: The working directory was the `home` directory. 

Explanation: When I first ran this command, it gave me no output and no prompt for the nect command. On entering the word `hello`, it repeated that word back. The `cat` command with no arguments, usually reads from the standard input and it repeats the word given. 

Error: This is not an error. 

### ii)Using the 'cat' command with a directory as an argument
When I ran the `cat` command with a directory as an argument using the code below, 
```
[user@sahara ~]$ cat lecture1
```
I got the following output, 
```
cat: lecture1: Is a directory
```
Working directory: The working directory was the `home` directory. 

Explanation: The `cat` command expects file names as arguments. Since `lecture1` is a directory, the `cat` command cannot read it and hence throws an error.

Error: This is an error because `cat` expects files as arguments, not directories. 

### iii) Using the `cat` command with a file as an argument
When I ran the `cat` command with a file as an argument using the code below, 
```
[user@sahara ~/lecture1]$ cat Hello.java
```
I got the following output, 
```
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}
```
Working directory: In this case, the working directory was the `lecture1` directory. 

Explanation: The `cat` command is intended to display the contents of a file passed in as the argument. In this case the file passed in as the argument is the `Hello.java` file. It displays the contents of the file as the output. 

Error: This is not an error. 









