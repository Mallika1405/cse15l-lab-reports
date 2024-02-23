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






