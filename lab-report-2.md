# LAB REPORT 2

## PART 1

## Search Engine
### Code

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {

    ArrayList<String> stringList= new ArrayList<>();

    public String handleRequest(URI url) {

        if (url.getPath().equals("/")) {
            String strToReturn= "";
            for(int i=0; i< stringList.size(); i++){
                strToReturn+=stringList.get(i);
            }
            return "String List: "+ strToReturn;
        } 
        else if (url.getPath().contains("/add")) {
            String[] parameters = url.getQuery().split("=");
            if(parameters[0].contains("s")){
            stringList.add((parameters[1]));
            return String.format("String added!");
            }
            else{
                return "invalid command";
            }
        }
        else if (url.getPath().contains("/search")){
            String strToReturnNew= "";
            String[] parameters = url.getQuery().split("=");
            if(parameters[0].contains("s")){
            for(int i=0; i< stringList.size(); i++){
                if(stringList.get(i).contains(parameters[1])){
                strToReturnNew += (stringList.get(i)+" ");
                }    
            }
            if(strToReturnNew.isEmpty()){
                return "No strings with the given substring was found.";
            }
            else{
            return "Strings found are: "+strToReturnNew;}
            }                  
            else{
                return "invalid command";
            }
        }
        else{
        return "404 Not Found!";
        }
    }
}

class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
#### Compiling the code using the following commands, 

<img width="497" alt="image" src="https://user-images.githubusercontent.com/114612660/198813241-b6e0ba10-746e-412f-873d-96e3efa271b7.png">

this calls the main method which opens the URL handler and the method handleRequest.
Copying the link to a browser, 

<img width="402" alt="image" src="https://user-images.githubusercontent.com/114612660/198813229-f85fe56e-4c61-4b8c-bd29-1adf7f0b16be.png">

the handleRequest method takes the url that was created as an argument and runs through the first if loop in the method and produces an empty list of strings

#### Implementing the add command for a few words:

<img width="419" alt="image" src="https://user-images.githubusercontent.com/114612660/198813277-e3b930fb-e872-4856-a412-40a88a72690b.png">

<img width="360" alt="image" src="https://user-images.githubusercontent.com/114612660/198813283-7de4a62c-88be-4156-a5a7-d16da8154456.png">

<img width="344" alt="image" src="https://user-images.githubusercontent.com/114612660/198813289-c786da4e-236b-495c-a815-9991a06ebfe2.png">

<img width="360" alt="image" src="https://user-images.githubusercontent.com/114612660/198813304-9205df11-2d7e-4221-b6c6-afa31e6b5ba8.png">

<img width="432" alt="image" src="https://user-images.githubusercontent.com/114612660/198813313-597bd7ff-ed7d-4d86-b8db-2644647d5e17.png">

all these words are added to our initial list by running through the second else if loop that asks the list to add the given string. So our list currently contains the strings: "music", "for", "a", "sushi", "restaurant".

#### Implementing the query to find words:

<img width="370" alt="image" src="https://user-images.githubusercontent.com/114612660/198813332-b2f7ba4c-037e-4b95-a77a-81e8ad345038.png">

Here, the given substring to search was given as "us", so the method iterates through the list to find strings that contain the given substring. In this case, the strings "music" and "sushi" contained the given substring so it returns the strings. 

#### Implementing commands that throw an error:

I am just trying to enter a few invalid commands to make sure that the program does not misinterpret any other commands. It should throw out an error like the following.

<img width="382" alt="image" src="https://user-images.githubusercontent.com/114612660/198813361-6e896fcb-041c-4a9c-b356-28ec66eac9e1.png">

<img width="377" alt="image" src="https://user-images.githubusercontent.com/114612660/198813385-e8b862a8-0f8e-4d17-a917-5134dcfd6fd5.png">




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

As it says in the screenshot, the output is expected to be {3,2,1} but the given code produces the list **{3,2,3}** which is the **symptom**
That is why it says the list differs at the second index. I have written more about why the code produces this output under 'code fix'. 

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

In this case, the **symptom** of the code is **1.8** as opposed to the value 3 that we are supposed to get.
More about why the test fails is written in the 'code fix' below. 

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
