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
For this step, I used the `git clone` command and for the SSH url(`git@github.com:Mallika1405/lab7.git`), I used the `Command-c` and `Command-v` keys on the keyboard. I pressed `<enter>` to get:
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
This made it much easier to understand the line numbers. Another command I used to reach the line with the bug(line 44) was `43j`. When my curosr was on line 1, the command `43j <enter>` moved the cursor down by 43 lines and it reached line 44. 

The bug in the code was that `index2` was not getting incremented in the last `while` loop and it was incrementing `index1` instead which should not have happened. So I fixed the bug by changing `index1` to `index2`. I did that by moving the `<right>` arrow key 11 times till I reached the `1` character in the word `index1`. I then used the `x` key to delete the `1`. I used the `i` key to insert 2 in that position and then used `<escape>` to escape the `insert` mode. This was the code after editing:
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
 44       index2 += 1;
 45     }
 46     return result;
 47   }
 48 
 49 
 50 }
 51 
```
After fixing the code, I used `<escape>` and `:wq` to save changes and exit `vim`. 

### Step 5: Run the tests, demonstrating that they now succeed
I used `<up> <up>` or the `<up>` arrow twice, followed by `<enter>` to get the `bash` command I had previously used- `bash test.sh`. 
I got the following output:
```
JUnit version 4.13.2
..
Time: 0.015

OK (2 tests)
```

### Step 6: Commit and push the resulting change to your Github account (you can pick any commit message!)
In order to commit to git, I used the command `git commit -a`. It then prompted me to enter a commit message as follows:
```

Fixed it!
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Committer: Mallika Dasgupta <mdasgupta@ieng6-203.ucsd.edu>
#
# On branch main
# Your branch is up to date with 'origin/main'.
#
# Changes to be committed:
#       modified:   ListExamples.java
#
```
I entered `Fixed it!` as my commit message. This was the summary it gave me once I finished. 
```
[mdasgupta@ieng6-203]:lab7:134$ git commit -a
[main ed04783] Fixed it!
 Committer: Mallika Dasgupta <mdasgupta@ieng6-203.ucsd.edu>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 1 insertion(+), 1 deletion(-)
```
It showed that I edited one file, `ListExamples.java` and made one insertion and one deletion. 
I used the `git push` to push changes to origin as follows:
```
[mdasgupta@ieng6-203]:lab7:135$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 297 bytes | 148.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:Mallika1405/lab7.git
   327ab1a..ed04783  main -> main
```
### Summary
#### Keypresses:
1. `<enter>` key was used to run a command after entering it into the terminal. 
2. `<up>` arrow key was used either to retrieve an old command from the command history in the terminal or it was used to navigate to a specific line in vim. 
3. `<down>` arrow key was used either to go back to a command that you have passed before from the command history in the terminal or to navigate to a specific line in vim. 
4. `<escape>` was used to exit a certain mode in vim like the inert mode. 
5. `x` was used to delete an element in vim. 
6. `i` was used to insert an element in vim. 

#### Commands:
1. `git clone` was used to clone the repository.
2. `cd` to be able to access the files in the directory.
3. `bash` to be able to run the `bash` file.
4. `vim` to open the vim editor on the file.
5. `:wq` to save changes and quit vim.
6. `:q!` to quit vim.
7. `git commit` opens up vim, waiting for edits and commits changes to git.
8. `git push` pushes changes to origin. 









