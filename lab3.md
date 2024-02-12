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


