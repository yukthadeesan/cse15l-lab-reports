# LAB REPORT 2
## PART 2


## reverseInPlace

Debugging the reverseInPlace method in the ArrayExamples file:

### Test

Starting off by testing a simple input array and expecting the output array to have reversed the order of elements inside the array.
```
  @Test
  public void testReverseInPlace2(){
    int[] input2 = { 1,2,3 };
    ArrayExamples.reverseInPlace(input2);
    assertArrayEquals(new int[]{ 3,2,1 }, input2);
  }
```

### Test Failure

I ran the test with the commands 
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
```
The test failed as shown in the screenshot

<img width="1219" alt="image" src="https://user-images.githubusercontent.com/114612660/195971699-93783597-e900-4734-a26c-8466c1fd99f1.png">

### Code Fix

The given code was just assigning values to the elements from the first index without saving them in prior so that the values can be assigned to elements from the last index. 
In the test that I ran, we had three elements in the array: {1, 2, 3}
The given menthod starts with the first element which is 1 and assigns the value 3 to it.
So now the array is {3,2,3}
Next it takes the second element and since (length-i-1)=i in this case, 2 stays put. 
Next, when it taked the third element, it tried to assign the value of the first element to the third element- in this case, the first element is 3, so the new array stays {3,2,3}
We require the array to be reversed and expect {3,2,1} which is why the test fails.

Debugged Code:
``` 
 static void reverseInPlace(int[] arr) {
   int j= arr.length/2;
   for(int i = 0; i < j; i += 1) {
     int temp= arr[i];
     arr[i] = arr[arr.length - i - 1];
     arr[arr.length - i - 1]= temp;
   }
 }
```

What I have done is: 
1. Create a for loop for indexing half of the length of the array 
2. Store these values in a new variable
3. Change the values of these indexes that are transversed to values from the last index (to reverse values)
4. Assign the values from the last indices to the new variable.


## averageWithoutLowest

Debugging the averageWithoutLowest method in the ArrayExamples file:

### Test

In this test, I try to have more than one lowest element in the array 
```
  @Test 
  public void averageWithoutLowestTest2(){
    double[] input3 = { 1.0, 2.0, 3.0, 4.0, 1.0, 1.0};
    double meanTest =ArrayExamples.averageWithoutLowest(input3);
    assertEquals(3, meanTest, 0);
  }
```

### Test Failure 

I ran the test with the commands 
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
```
The test failed as shown in the screenshot

<img width="1221" alt="image" src="https://user-images.githubusercontent.com/114612660/195971733-9260e597-7c22-4e2c-b6dc-f61d8b24053a.png">

### Code Fix

When you run the method, the sum variable excludes all the lowest values, but when you have to calculate the mean it counts all the the lowest values but one because it assumes that there can only be one lowest value.
So in the test since I had 3 values which were equal to 1 and lowest in the array, the mean was calculated as 9/5 which equals to 1.8 as opposed to 3.0 that we expect. That is why the test fails

Debugged Code:
```
static double averageWithoutLowest(double[] arr) {
   if(arr.length < 2) { return 0.0; }  
   double lowest= arr[0];
   for(double num: arr) {
     if(num < lowest) { lowest = num; }
   }
   double sum = 0;
   int count=0;
   for(double num: arr) {
     if(num== lowest) { count += 1;}
     if(num != lowest) { sum += num; }
   }
   return (double) sum / (arr.length- count);
 }
```
What I have done is: 
1. Create a new variable 'count' which counts all the lowest values in the array
2. Subtract count from the length of the array as that is the total number of elements that we have to calculate mean for. 
