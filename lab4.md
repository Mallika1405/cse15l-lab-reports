# CSE 15L LAB REPORT 4
### Step 1: Log into ieng6
Logged into my ieng6 account using the following command:
```
ssh mdasgupta@ieng6.ucsd.edu
```
I then pressed `<enter>` to get the following output:
```
Last login: Tue Feb  6 15:48:16 2024 from 128.54.177.192
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-01-12_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/cs120wi24/cs120wi24dx/.snapshot/hourly.2024-01-29_1201: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-02-04_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-02-05_0010: Stale file handle
Hello mdasgupta, you are currently logged into ieng6-201.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   23:45:01   3   0.26,  0.49,  0.45
ieng6-202   23:45:01   10  0.05,  0.15,  0.16
ieng6-203   23:45:01   3   0.53,  0.34,  0.30

 

To begin work for one of your courses [ cs15lwi24 ], type its name 
at the command prompt.  (For example, "cs15lwi24", without the quotes).

To see all available software packages, type "prep -l" at the command prompt,
or "prep -h" for more options.
[mdasgupta@ieng6-201]:~:82$
```
### Step 2: Clone your fork of the repository from your Github account (using the SSH URL)
For this step, I used the `git clone` command and for the SSH url(`git@github.com:Mallika1405/lab7.git`), I used the `command+c` and `command+v` keys on the keyboard. I pressed `<enter>` to get:
```
[mdasgupta@ieng6-201]:~:116$ git clone git@github.com:Mallika1405/lab7.git
Cloning into 'lab7'...
remote: Enumerating objects: 58, done.
remote: Total 58 (delta 0), reused 0 (delta 0), pack-reused 58
Receiving objects: 100% (58/58), 376.39 KiB | 1.96 MiB/s, done.
Resolving deltas: 100% (21/21), done.
```
This means the directory has been cloned. 

### Step 3: Run the tests, demonstrating that they fail
First I used the `cd` command:
```
cd lab7/
```
I could now access the files in the `lab7` directory. To check the files in the directory I used the `ls` command to check the files and got the following output:
```
ListExamples.java  ListExamplesTests.java  lib  test.sh
```
These are the files in the `lab7` directory. In order to run the tests, in the file `test.sh`, I used the following command:
```
bash test.sh
```
The tests failed, producing the following output:
```
JUnit version 4.13.2
..E
Time: 0.526
There was 1 failure:
1) testMerge2(ListExamplesTests)
org.junit.runners.model.TestTimedOutException: test timed out after 500 milliseconds
	at java.lang.System.arraycopy(Native Method)
	at java.util.Arrays.copyOf(Arrays.java:3213)
	at java.util.Arrays.copyOf(Arrays.java:3181)
	at java.util.ArrayList.grow(ArrayList.java:267)
	at java.util.ArrayList.ensureExplicitCapacity(ArrayList.java:241)
	at java.util.ArrayList.ensureCapacityInternal(ArrayList.java:233)
	at java.util.ArrayList.add(ArrayList.java:464)
	at ListExamples.merge(ListExamples.java:42)
	at ListExamplesTests.testMerge2(ListExamplesTests.java:19)

FAILURES!!!
Tests run: 2,  Failures: 1
```
### Step 4: Edit the code file to fix the failing test
To edit the file in the terminal, I used the `vim` file editor. I ran the following command:
```
vim ListExamples.java
```
This opened the ListExamples.java file in the command line and allowed me to edit it. While editing it, I tried using the <down> arrow key 37 times in order to reach the line with the bug. However, I soon realised that that was not efficient. I then did the following:
```
<escape> :set number
```
This gave me all the line numbers of the code and my code now looked like this:
```
 1 import java.util.ArrayList;
  2 import java.util.List;
  3 
  4 interface StringChecker { boolean checkString(String s); }
  5 
  6 class ListExamples {
  7 
  8   // Returns a new list that has all the elements of the input list for which
  9   // the StringChecker returns true, and not the elements that return false, in
 10   // the same order they appeared in the input list;
 11   static List<String> filter(List<String> list, StringChecker sc) {
 12     List<String> result = new ArrayList<>();
 13     for(String s: list) {
 14       if(sc.checkString(s)) {
 15         result.add(0, s);
 16       }
 17     }
 18     return result;
 19   }
 20 
 21 
 22   // Takes two sorted list of strings (so "a" appears before "b" and so on),
 23   // and return a new list that has all the strings in both list in sorted order.
 24   static List<String> merge(List<String> list1, List<String> list2) {
 25     List<String> result = new ArrayList<>();
 26     int index1 = 0, index2 = 0;
 27     while(index1 < list1.size() && index2 < list2.size()) {
 28       if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
 29         result.add(list1.get(index1));
 30         index1 += 1;
 31       }
 32       else {
 33         result.add(list2.get(index2));
 34         index2 += 1;
 35       }
 36         }
 37     while(index1 < list1.size()) {
 38       result.add(list1.get(index1));
 39       index1 += 1;
 40     }
 41     while(index2 < list2.size()) {
 42       result.add(list2.get(index2));
 43       // change index1 below to index2 to fix test
 44       index1 += 1;
 45     }
 46     return result;
 47   }
 48 
 49 
 50 }
 51 
```








