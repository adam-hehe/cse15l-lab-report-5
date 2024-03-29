# Lab Report 5 - Putting it All Together (Week 9)

## Part 1 – Debugging Scenario

## The original post from a student with a screenshot showing a symptom and a description of a guess at the bug/some sense of what the failure-inducing input is.**

**Help !! Sorting algorithm not working correctly**
```
-labReport/
  SortingAlgorithm.java
  CustomTester.java
  test.sh  
```
**Code for Sorting Algorithm**
```java
public class SortingAlgorithm {
    int[] array = {3, 5, 2, 4, 1};

    public void bubbleSort(int[] arr) {
        int swap;
        for(int i = 0; i < arr.length; i++) {
            for(int j = i; j < arr.length; j++) {
                if(arr[i] < arr[j]) {
                    swap = arr[i];
                    arr[i] = arr[j];
                    arr[j] = swap;
                }
            }
        }
    }
}
```
**Code for Failing Tests**
```java
import static org.junit.Assert.*;
import org.junit.*;

public class CustomTest {
    @Test
    public void testSorted() {
        int[] sortedArr = {1, 2, 3, 4, 5};
        int[] expectedArr = {1, 2, 3, 4, 5};
        SortingAlgorithm sorter = new SortingAlgorithm();

        sorter.bubbleSort(sortedArr);
        assertArrayEquals(expectedArr, sortedArr);
    }

    @Test
    public void testBackwards() {
        int[] backwardsArr = {5, 4, 3, 2, 1};
        int[] expectedArr = {1, 2, 3, 4, 5};
        SortingAlgorithm sorter = new SortingAlgorithm();

        sorter.bubbleSort(backwardsArr);
        assertArrayEquals(expectedArr, backwardsArr);
    }

    @Test
    public void testUnsorted() {
        int[] unsortedArr = {3, 1, 5, 4, 2};
        int[] expectedArr = {1, 2, 3, 4, 5};
        SortingAlgorithm sorter = new SortingAlgorithm();

        sorter.bubbleSort(unsortedArr);
        assertArrayEquals(expectedArr, unsortedArr);
    }
}
```

```java
  javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java  
  java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore CustomTest
```
All three test cases are failing and it states `expected [1] but was [5]`. Maybe there is an issue with the indexing thats causing elements to shift even when they are not supposed to?


**A response from a TA asking a leading question or suggesting a command to try**

Try running your algorithm through jdb, use the `step` command and the `print` command to see if you notice any unintentional changes that happen with each loop iteration.

**Another screenshot/terminal output showing what information the student got from trying that, and a clear description of what the bug is.**
![Image](image3.png)
5 showing up as the first element
![Image](image1.png)
The array ends up being sorted in revese order

It looks like the program is actually sorting the algorithm in reverse order, to fix this I changed the less than sign to a greater than sign in the if statement. The command lines I used to find the bug was to first start the jdb and `stop in SortingAlgorithm.bubbleSort`, then I used the step method and the check the values of each individual element in the array using `print arr[num]`.

## Part 2 – Reflection

One thing I learned that I found really useful was jdb. I didn't know about it before and was first introduced to it in this class. I feel like because able to debug efficiently is really important and can save a lot of time. Jdb is a tool that I see worth getting more familiar with.



