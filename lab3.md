# CSE 15L LAB REPORT 3
## PART 1-BUGS
### The Buggy Code
```
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
```
The code checks for the lowest number and stores it in a variable. It then compares all the other variables to the lowest variable and makes sure that there is no other variable with the same value as the lowest variable and adds all those numbers. However, when it comes to calculating the average, the code only subtracts 1 from the total number. But what if there are duplicates? Will it still work?
To find out, we write a test. 
### A failure inducing input
```
@Test
  public void testaverageWithoutLowest(){
    double [] arr={10,4,5,8,6,2,2};
    double avg=ArrayExamples.averageWithoutLowest(arr);
    assertEquals(6.6,avg,0.001);
  }
```
This test takes in an array with duplicate elements. This is the output:
```
JUnit version 4.13.2
.E
Time: 0.004
There was 1 failure:
1) testaverageWithoutLowest(ArrayTests)
java.lang.AssertionError: expected:<6.6> but was:<5.5>
```
The output prints out 5.5 but it was supposed to print out 6.6. This is the symptom of the problem. If we try a different test with no duplicate elements would we still get the wrong answer?
### An input that doesn't induce failure
```
@Test
  public void testaverageWithoutLowest(){
    double [] arr={10,4,5,8,6,2};
    double avg=ArrayExamples.averageWithoutLowest(arr);
    assertEquals(6.6,avg,0.001);
}
```
This input array gives the correct output and the test passes as follows:
```
JUnit version 4.13.2
..
Time: 0.004

OK (2 tests)
```
So we could conclude that the bug is in the code. Instead of returning `sum`/`arr.length-1`, we should create another variable to store the number of duplicates. We could call this `cnt`. If the lowest number has duplicates, we can store the duplicates in the `cnt` variable. 
We could keep incrementing the `cnt` variable. At the end we could return `sum`/`arr.length-cnt` for the average. 
### The corrected code 
```
static double averageWithoutLowest(double[] arr) {
    int cnt=0;
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
      else if(num==lowest){
        cnt++;

      }
    }
    return sum / (arr.length-cnt);
  }
```
### Working code output
#### Test case code:
```
@Test
  public void testaverageWithoutLowest(){
    double [] arr={10,4,5,8,6,2,2};
    double avg=ArrayExamples.averageWithoutLowest(arr);
    assertEquals(6.6,avg,0.001);

  }
```
#### Test case output:
```
JUnit version 4.13.2
.
Time: 0.004

OK (1 test)
```
The test case passed with duplicate elements! We could also check for a normal array with no duplicate elements. 
### Working code output
#### Test case code:
```
@Test
  public void testaverageWithoutLowest(){
    double [] arr={10,4,5,8,6,2};
    double avg=ArrayExamples.averageWithoutLowest(arr);
    assertEquals(6.6,avg,0.001);

  }
````
#### Test case output:
```
JUnit version 4.13.2
.
Time: 0.004

OK (1 test)
```
The test case passed without any duplicate elements as well! The bug has been fixed!

Conclusion:The bug in this code was the fact that we were returning `sum`/`arr.length-1` because we did not consider the possiblity of duplicate elements. Now that we did, by counting the duplicate elements and removing those many elements from the array, we found the correct average. 

## PART 2 - RESEARCHING COMMANDS
### find `-type`
The `-type` option allows you to search for files based on their type. The common types include `f` for regular files and `d` for directories.
#### Example 1:
Used the `-type f` option to look for all the files in `./technical/911report`. It's a more effiencient way of looking for files in `./technical/911report`. 
```
mallika@Mallikas-MacBook-Air docsearch % find ./technical/911report -type f
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```
#### Example 2:
Used the `-type d` option to look for all the directories in `./technical`. It is used to obtain the directories and look at them together in order to find something. 
```
mallika@Mallikas-MacBook-Air docsearch % find ./technical -type d

./technical
./technical/government
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Gen_Account_Office
./technical/government/Post_Rate_Comm
./technical/government/Media
./technical/plos
./technical/biomed
./technical/911report
```
Source: https://www.geeksforgeeks.org/find-command-in-linux-with-examples/

### find `-name`
The `-name` option allows searching for files whose name matches a given pattern. This option is case-sensitive.
#### Example 1
Used the `-name` option to find files with `.txt` extension in `./technical/911report`. It's a more efficient way of looking for 911 reports. 
```
mallika@Mallikas-MacBook-Air docsearch % find ./technical/911report  -name "*.txt"

./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```
#### Example 2
Used the `-name` to find `.txt` files with the word `journal` in the name in `./technical/plos`. It's useful for finding the journal files. 
```
mallika@Mallikas-MacBook-Air docsearch % find ./technical -name "journal.*.txt"  
./technical/plos/journal.pbio.0030032.txt
./technical/plos/journal.pbio.0020354.txt
./technical/plos/journal.pbio.0020156.txt
./technical/plos/journal.pbio.0020140.txt
./technical/plos/journal.pbio.0020183.txt
./technical/plos/journal.pbio.0020430.txt
./technical/plos/journal.pbio.0020394.txt
./technical/plos/journal.pbio.0020431.txt
./technical/plos/journal.pbio.0020419.txt
./technical/plos/journal.pbio.0020169.txt
./technical/plos/journal.pbio.0020035.txt
./technical/plos/journal.pbio.0030024.txt
./technical/plos/journal.pbio.0020223.txt
./technical/plos/journal.pbio.0020019.txt
./technical/plos/journal.pbio.0020145.txt
./technical/plos/journal.pbio.0020353.txt
./technical/plos/journal.pbio.0020347.txt
./technical/plos/journal.pbio.0020420.txt
./technical/plos/journal.pbio.0020346.txt
./technical/plos/journal.pbio.0020187.txt
```
Source: https://www.redhat.com/sysadmin/linux-find-command
        Class notes

### find `-size`
The `-size` option allows you to search for files by their size. You can specify sizes in blocks, kilobytes (k), megabytes (M), and so on.
#### Example 1
Used the `size` option to find files larger than 100KB in `./technical`. This command lists files over 100KB in size within the ./technical directory. It's useful for identifying large files that may need to be compressed or moved.
```
mallika@Mallikas-MacBook-Air docsearch % find ./technical -size +100k

./technical/government/About_LSC/commission_report.txt
./technical/government/About_LSC/State_Planning_Report.txt
./technical/government/Env_Prot_Agen/multi102902.txt
./technical/government/Env_Prot_Agen/ctm4-10.txt
./technical/government/Env_Prot_Agen/bill.txt
./technical/government/Env_Prot_Agen/tech_adden.txt
./technical/government/Gen_Account_Office/d0269g.txt
./technical/government/Gen_Account_Office/GovernmentAuditingStandards_yb2002ed.txt
./technical/government/Gen_Account_Office/Sept27-2002_d02966.txt
./technical/government/Gen_Account_Office/d01376g.txt
./technical/government/Gen_Account_Office/Statements_Feb28-1997_volume.txt
./technical/government/Gen_Account_Office/pe1019.txt
./technical/government/Gen_Account_Office/gg96118.txt
./technical/government/Gen_Account_Office/d01591sp.txt
./technical/government/Gen_Account_Office/im814.txt
./technical/government/Gen_Account_Office/ai9868.txt
./technical/government/Gen_Account_Office/May1998_ai98068.txt
./technical/government/Gen_Account_Office/d02701.txt
./technical/biomed/1471-2105-3-2.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-12.txt
```
#### Example 2
Used the `size` option to find files less than 2KB in `./technical`. It's useful for locating small files for quick processing or review.
```
mallika@Mallikas-MacBook-Air docsearch % find ./technical -size -2k

./technical
./technical/government
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Post_Rate_Comm
./technical/government/Media/Helping_Hands.txt
./technical/government/Media/Campaign_Pays.txt
./technical/government/Media/Fire_Victims_Sue.txt
./technical/government/Media/Court_Keeps_Judge_From.txt
./technical/government/Media/It_Pays_to_Know.txt
./technical/government/Media/Self-Help_Website.txt
./technical/government/Media/Justice_requests.txt
./technical/government/Media/Wilmington_lawyer.txt
./technical/government/Media/Lawyer_Web_Survey.txt
./technical/plos/pmed.0020048.txt
./technical/plos/pmed.0020028.txt
./technical/plos/pmed.0020191.txt
./technical/plos/pmed.0020226.txt
./technical/plos/pmed.0020192.txt
./technical/plos/pmed.0020157.txt
./technical/plos/pmed.0020082.txt
./technical/plos/pmed.0020120.txt
./technical/911report
```
Source: https://kb.iu.edu/d/admm

### find `-mtime`
The `-mtime` option is used to find files modified `n` days ago. The access time is updated whenever the file's contents are changed by any command or program.
#### Example 1:
Used the `mtime` option to find files modified 5 days ago in `./technical/911report`. This could be used to find recently modified files. 
```
mallika@Mallikas-MacBook-Air docsearch % find ./technical/911report  -mtime -5
./technical/911report
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```
#### Example 2:
Used the `mtime` option to find files modified more than 2 days ago in `./technical/plos`. This could be used to find files that were modified a while ago. 
```
mallika@Mallikas-MacBook-Air docsearch % find ./technical/plos  -mtime +2 

./technical/plos
./technical/plos/pmed.0020273.txt
./technical/plos/journal.pbio.0030032.txt
./technical/plos/pmed.0020065.txt
./technical/plos/pmed.0020071.txt
./technical/plos/pmed.0020059.txt
./technical/plos/pmed.0010039.txt
./technical/plos/journal.pbio.0020354.txt
./technical/plos/pmed.0010010.txt
./technical/plos/journal.pbio.0020156.txt
./technical/plos/pmed.0020104.txt
./technical/plos/pmed.0020272.txt
./technical/plos/pmed.0020258.txt
./technical/plos/pmed.0020099.txt
./technical/plos/journal.pbio.0020140.txt
./technical/plos/journal.pbio.0020183.txt
./technical/plos/journal.pbio.0020430.txt
./technical/plos/journal.pbio.0020394.txt
./technical/plos/journal.pbio.0020431.txt
./technical/plos/journal.pbio.0020419.txt
./technical/plos/pmed.0010013.txt
./technical/plos/pmed.0020113.txt
./technical/plos/journal.pbio.0020169.txt
./technical/plos/pmed.0020098.txt
./technical/plos/journal.pbio.0020035.txt
./technical/plos/pmed.0020067.txt
./technical/plos/pmed.0020073.txt
./technical/plos/journal.pbio.0030024.txt
./technical/plos/journal.pbio.0020223.txt
./technical/plos/pmed.0020249.txt
./technical/plos/pmed.0020275.txt
./technical/plos/journal.pbio.0020019.txt
./technical/plos/pmed.0020088.txt
./technical/plos/journal.pbio.0020145.txt
./technical/plos/pmed.0020103.txt
./technical/plos/pmed.0020117.txt
./technical/plos/journal.pbio.0020353.txt
./technical/plos/journal.pbio.0020347.txt
./technical/plos/journal.pbio.0020420.txt
./technical/plos/journal.pbio.0020346.txt
./technical/plos/journal.pbio.0020187.txt
./technical/plos/pmed.0020116.txt
./technical/plos/pmed.0020102.txt
./technical/plos/journal.pbio.0020150.txt
./technical/plos/pmed.0020062.txt
./technical/plos/pmed.0020274.txt
./technical/plos/journal.pbio.0020232.txt
./technical/plos/journal.pbio.0030021.txt
./technical/plos/journal.pbio.0020224.txt
./technical/plos/pmed.0020048.txt
./technical/plos/pmed.0020060.txt
./technical/plos/pmed.0020074.txt
./technical/plos/journal.pbio.0020146.txt
./technical/plos/pmed.0020114.txt
./technical/plos/pmed.0010028.txt
./technical/plos/journal.pbio.0020350.txt
./technical/plos/journal.pbio.0020190.txt
./technical/plos/pmed.0010029.txt
./technical/plos/pmed.0020115.txt
./technical/plos/journal.pbio.0020147.txt
./technical/plos/pmed.0020075.txt
./technical/plos/pmed.0020061.txt
./technical/plos/pmed.0020210.txt
./technical/plos/pmed.0020238.txt
./technical/plos/journal.pbio.0030051.txt
./technical/plos/journal.pbio.0020068.txt
./technical/plos/journal.pbio.0020054.txt
./technical/plos/journal.pbio.0020040.txt
./technical/plos/pmed.0010066.txt
./technical/plos/journal.pbio.0030131.txt
./technical/plos/journal.pbio.0020337.txt
./technical/plos/pmed.0020198.txt
./technical/plos/pmed.0010067.txt
./technical/plos/journal.pbio.0020121.txt
./technical/plos/pmed.0020007.txt
./technical/plos/journal.pbio.0030050.txt
./technical/plos/pmed.0020239.txt
./technical/plos/journal.pbio.0020241.txt
./technical/plos/pmed.0020005.txt
./technical/plos/journal.pbio.0020043.txt
./technical/plos/pmed.0020039.txt
./technical/plos/pmed.0010071.txt
./technical/plos/journal.pbio.0030127.txt
./technical/plos/pmed.0010058.txt
./technical/plos/pmed.0010070.txt
./technical/plos/pmed.0010064.txt
./technical/plos/pmed.0020158.txt
./technical/plos/journal.pbio.0020042.txt
./technical/plos/journal.pbio.0020297.txt
./technical/plos/pmed.0020206.txt
./technical/plos/pmed.0020212.txt
./technical/plos/pmed.0020216.txt
./technical/plos/journal.pbio.0030094.txt
./technical/plos/journal.pbio.0020046.txt
./technical/plos/pmed.0020028.txt
./technical/plos/journal.pbio.0020052.txt
./technical/plos/pmed.0020148.txt
./technical/plos/pmed.0020160.txt
./technical/plos/pmed.0010048.txt
./technical/plos/pmed.0010060.txt
./technical/plos/journal.pbio.0030137.txt
./technical/plos/journal.pbio.0030136.txt
./technical/plos/pmed.0010061.txt
./technical/plos/pmed.0010049.txt
./technical/plos/pmed.0020161.txt
./technical/plos/journal.pbio.0020127.txt
./technical/plos/pmed.0020149.txt
./technical/plos/journal.pbio.0020133.txt
./technical/plos/pmed.0020015.txt
./technical/plos/journal.pbio.0020053.txt
./technical/plos/journal.pbio.0020047.txt
./technical/plos/pmed.0020203.txt
./technical/plos/journal.pbio.0030056.txt
./technical/plos/pmed.0020201.txt
./technical/plos/journal.pbio.0030097.txt
./technical/plos/pmed.0020017.txt
./technical/plos/journal.pbio.0020125.txt
./technical/plos/journal.pbio.0020440.txt
./technical/plos/pmed.0010062.txt
./technical/plos/pmed.0020189.txt
./technical/plos/pmed.0020162.txt
./technical/plos/pmed.0020016.txt
./technical/plos/pmed.0020002.txt
./technical/plos/pmed.0020200.txt
./technical/plos/pmed.0020231.txt
./technical/plos/journal.pbio.0020263.txt
./technical/plos/pmed.0020027.txt
./technical/plos/pmed.0020033.txt
./technical/plos/journal.pbio.0020101.txt
./technical/plos/pmed.0010047.txt
./technical/plos/journal.pbio.0030105.txt
./technical/plos/journal.pbio.0020302.txt
./technical/plos/pmed.0010046.txt
./technical/plos/pmed.0010052.txt
./technical/plos/pmed.0020191.txt
./technical/plos/journal.pbio.0020100.txt
./technical/plos/pmed.0020146.txt
./technical/plos/journal.pbio.0020262.txt
./technical/plos/journal.pbio.0030065.txt
./technical/plos/journal.pbio.0020276.txt
./technical/plos/pmed.0020232.txt
./technical/plos/pmed.0020226.txt
./technical/plos/pmed.0020024.txt
./technical/plos/pmed.0020018.txt
./technical/plos/pmed.0020144.txt
./technical/plos/pmed.0020150.txt
./technical/plos/journal.pbio.0020116.txt
./technical/plos/pmed.0020187.txt
./technical/plos/pmed.0010050.txt
./technical/plos/pmed.0010051.txt
./technical/plos/pmed.0020192.txt
./technical/plos/pmed.0010045.txt
./technical/plos/pmed.0020145.txt
./technical/plos/pmed.0020019.txt
./technical/plos/journal.pbio.0020063.txt
./technical/plos/journal.pbio.0030076.txt
./technical/plos/journal.pbio.0030062.txt
./technical/plos/pmed.0020237.txt
./technical/plos/journal.pbio.0020067.txt
./technical/plos/pmed.0020009.txt
./technical/plos/journal.pbio.0020073.txt
./technical/plos/pmed.0020035.txt
./technical/plos/pmed.0020021.txt
./technical/plos/journal.pbio.0020113.txt
./technical/plos/pmed.0020155.txt
./technical/plos/pmed.0010069.txt
./technical/plos/pmed.0010041.txt
./technical/plos/pmed.0020182.txt
./technical/plos/pmed.0020196.txt
./technical/plos/journal.pbio.0020311.txt
./technical/plos/journal.pbio.0030102.txt
./technical/plos/journal.pbio.0020310.txt
./technical/plos/pmed.0020197.txt
./technical/plos/pmed.0010068.txt
./technical/plos/pmed.0020140.txt
./technical/plos/journal.pbio.0020112.txt
./technical/plos/pmed.0020020.txt
./technical/plos/pmed.0020034.txt
./technical/plos/pmed.0020236.txt
./technical/plos/journal.pbio.0020272.txt
./technical/plos/pmed.0020208.txt
./technical/plos/journal.pbio.0020064.txt
./technical/plos/pmed.0020022.txt
./technical/plos/pmed.0020036.txt
./technical/plos/pmed.0010056.txt
./technical/plos/pmed.0020195.txt
./technical/plos/pmed.0010042.txt
./technical/plos/pmed.0020181.txt
./technical/plos/journal.pbio.0020306.txt
./technical/plos/journal.pbio.0030129.txt
./technical/plos/journal.pbio.0020307.txt
./technical/plos/pmed.0020180.txt
./technical/plos/pmed.0020194.txt
./technical/plos/pmed.0020157.txt
./technical/plos/journal.pbio.0020105.txt
./technical/plos/pmed.0020023.txt
./technical/plos/journal.pbio.0020071.txt
./technical/plos/pmed.0020235.txt
./technical/plos/journal.pbio.0020267.txt
./technical/plos/pmed.0020209.txt
./technical/plos/pmed.0020246.txt
./technical/plos/journal.pbio.0020228.txt
./technical/plos/journal.pbio.0020214.txt
./technical/plos/pmed.0020050.txt
./technical/plos/pmed.0020118.txt
./technical/plos/pmed.0010030.txt
./technical/plos/pmed.0010024.txt
./technical/plos/journal.pbio.0020348.txt
./technical/plos/journal.pbio.0020406.txt
./technical/plos/pmed.0010025.txt
./technical/plos/pmed.0020086.txt
./technical/plos/pmed.0020045.txt
./technical/plos/journal.pbio.0020215.txt
./technical/plos/pmed.0020247.txt
./technical/plos/pmed.0020047.txt
./technical/plos/journal.pbio.0020001.txt
./technical/plos/pmed.0020090.txt
./technical/plos/journal.pbio.0020161.txt
./technical/plos/journal.pbio.0020439.txt
./technical/plos/journal.pbio.0020404.txt
./technical/plos/pmed.0010026.txt
./technical/plos/journal.pbio.0020148.txt
./technical/plos/pmed.0020085.txt
./technical/plos/pmed.0020091.txt
./technical/plos/journal.pbio.0020028.txt
./technical/plos/journal.pbio.0020216.txt
./technical/plos/pmed.0020278.txt
./technical/plos/pmed.0020268.txt
./technical/plos/journal.pbio.0020206.txt
./technical/plos/journal.pbio.0020010.txt
./technical/plos/journal.pbio.0020164.txt
./technical/plos/pmed.0010022.txt
./technical/plos/pmed.0010036.txt
./technical/plos/journal.pbio.0020400.txt
./technical/plos/journal.pbio.0020401.txt
./technical/plos/pmed.0010023.txt
./technical/plos/pmed.0020123.txt
./technical/plos/pmed.0020094.txt
./technical/plos/journal.pbio.0020213.txt
./technical/plos/pmed.0020257.txt
./technical/plos/journal.pbio.0020013.txt
./technical/plos/pmed.0020055.txt
./technical/plos/pmed.0020082.txt
./technical/plos/pmed.0010021.txt
./technical/plos/pmed.0010034.txt
./technical/plos/pmed.0010008.txt
./technical/plos/pmed.0020120.txt
./technical/plos/journal.pbio.0020172.txt
./technical/plos/pmed.0020040.txt
./technical/plos/pmed.0020068.txt
./technical/plos/journal.pbio.0020012.txt
./technical/plos/pmed.0020281.txt
./technical/plos/pmed.0020242.txt
```
Source: https://www.geeksforgeeks.org/find-command-in-linux-with-examples/





