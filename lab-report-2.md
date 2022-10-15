# LAB REPORT 2
##PART 2


##reverseInPlace

Debugging the reverseInPlace method in the ArrayExamples file:
Starting off by testing a simple input array and expecting the output array to have reversed the order of elements inside the array.
```
  @Test
  public void testReverseInPlace2(){
    int[] input2 = { 1,2,3 };
    ArrayExamples.reverseInPlace(input2);
    assertArrayEquals(new int[]{ 3,2,1 }, input2);
  }
```
When I ran the test with the commands 
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
```
The test failed as shown in the screenshot

<img width="1219" alt="image" src="https://user-images.githubusercontent.com/114612660/195971699-93783597-e900-4734-a26c-8466c1fd99f1.png">

code fix
``` 
 // debugged code
 static void reverseInPlace(int[] arr) {
   int j= arr.length/2;
   for(int i = 0; i < j; i += 1) {
     int temp= arr[i];
     arr[i] = arr[arr.length - i - 1];
     arr[arr.length - i - 1]= temp;
   }
 }
```

average without lowest

<img width="914" alt="image" src="https://user-images.githubusercontent.com/114612660/195971718-ed60a196-2629-43b9-9051-b72a436c4a94.png">

failure
<img width="1221" alt="image" src="https://user-images.githubusercontent.com/114612660/195971733-9260e597-7c22-4e2c-b6dc-f61d8b24053a.png">

code fix
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
