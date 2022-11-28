# LAB REPORT 5  

## CODE: grade.sh

```
err() {
  echo $1
  exit 1
}

DIR="student_submission"
CP=".\
:lib/hamcrest-core-1.3.jar\
:lib/junit-4.13.2.jar"

test ! -z "$1" \
|| err "Please supply a git repsitory"

rm -rf "${DIR}"
git clone $1 "${DIR}"

if [ -e ${DIR}/ListExamples.java ]  
  then 
    echo "File was found"
  else
    err "File NOT found: ListExamples.java"
fi 

cp TestListExamples.java "${DIR}"
cp -r lib "${DIR}"
cd "${DIR}"

javac -cp "${CP}" *.java  2> ../error.txt
if [ $? -eq 0 ] 
  then 
    echo "File Compiled!"
else
  err "Compilation FAILED!"
fi

java -cp "${CP}" org.junit.runner.JUnitCore TestListExamples \
> ../report.txt

echo "Report saved to: report.txt"

total_tests=$(head -n 2 ../report.txt | tail -n 1 | grep -o "\." | wc -l)
number_of_tests_failed=$(head -n 2 ../report.txt | tail -n 1 | grep -o ".E" | wc -l)

echo "$number_of_tests_failed" tests failed.
echo Score: "$(($total_tests - $number_of_tests_failed))" out of $total_tests

exit
```

## Examples
 
Here are a few examples of student submission repositories tested against the grader. Their outputs on the browser as well as on the terminal have been attached. 
To open the grader on the browser, I used:
```
javac GradeServer.java Server.java
java GradeServer 5028
```

### [Student submission 1](https://github.com/ucsd-cse15l-f22/list-methods-lab3)
The reported grade was loaded in the [URL](http://localhost:5028/grade?repo=https://github.com/ucsd-cse15l-f22/list-methods-lab3) <br />
**Output in browser:**

<img width="801" alt="image" src="https://user-images.githubusercontent.com/114612660/204251345-b28298f4-b158-4a11-9b8a-d6f25100f487.png">

**Output in terminal:**

<img width="1008" alt="image" src="https://user-images.githubusercontent.com/114612660/204249907-037ad74c-c336-45bc-b801-c2def824e60b.png">


### [Student submission 2](https://github.com/ucsd-cse15l-f22/list-methods-corrected)
The reported grade was loaded in the [URL](http://localhost:5028/grade?repo=https://github.com/ucsd-cse15l-f22/list-methods-corrected) <br />
**Output in browser:**

<img width="794" alt="image" src="https://user-images.githubusercontent.com/114612660/204282445-cac7788d-85ab-4c1e-9fac-2652ba71193f.png">

**Output in terminal:**

<img width="1027" alt="image" src="https://user-images.githubusercontent.com/114612660/204250178-f45dad75-7932-42fb-9c15-25a0c47151e3.png">


### [Student submission 3](https://github.com/ucsd-cse15l-f22/list-methods-compile-error)
The reported grade was loaded in the [URL](http://localhost:5028/grade?repo=https://github.com/ucsd-cse15l-f22/list-methods-compile-error)<br />
**Output in browser:**

<img width="954" alt="image" src="https://user-images.githubusercontent.com/114612660/204282633-1eda464f-2eea-4793-b57e-5c2e7047148d.png">

**Output in terminal:**

<img width="1046" alt="image" src="https://user-images.githubusercontent.com/114612660/204250098-5a69abf0-88d1-4c81-aa9b-4df4a9a3c026.png">


### [Student submission 4](https://github.com/ucsd-cse15l-f22/list-methods-filename)
The reported grade was loaded in the [URL](http://localhost:5028/grade?repo=https://github.com/ucsd-cse15l-f22/list-methods-filename)<br />
**Output in browser:**

<img width="749" alt="image" src="https://user-images.githubusercontent.com/114612660/204282716-268ff14e-79d3-45e5-9b32-57364fe03c92.png">

**Output in terminal:**

<img width="1032" alt="image" src="https://user-images.githubusercontent.com/114612660/204250412-700e275b-a532-4920-a2c0-2fd25f046722.png">

## Tracing the code

Tracing the `grade.sh` code for [Student submission 3](https://github.com/ucsd-cse15l-f22/list-methods-compile-error): 
* In the first few lines of code (lines 1-3) I have created a function which will produce an error message and set return code 1 which indicates exit status failure.
* In line 11, the test is used to check if a repository has been entered in the terminal. If it is left empty, (for example, the command `bash grade.sh `) it will produce the given error message. In this file, since we have given the link to a repository, the exit code is 0 and there is NO error message. 
* In line 17, the 'if' statement is used check whether the submission contains the file *ListExamples.java*. In this case, the condition is TRUE, the exit code is 0 and so the **stdout is: "File was found"**.
* In line 28, the code compiles the directory and redirects the standard error to a text file called *error.txt*. This student submission has a syntax error and cannot be compiled so the exit code is 1 after it runs through line 28.
* Starting from line 29, another 'if' loop is used to check whether the file can be compiled or not. The if statement returns FALSE in this case because the exit code in the previous line was nonzero. It reads the else statement in line 32 and the error message is printed out. 

**stderr:**

<img width="467" alt="image" src="https://user-images.githubusercontent.com/114612660/204297385-c265ac48-2588-4654-9380-807491b3fd9d.png">

**stdout:**

```
File was found
Compilation FAILED!
```
All the lines after line 36 depend on the file being compiled and therefore do not run. 
The final output in the browser is:

<img width="954" alt="image" src="https://user-images.githubusercontent.com/114612660/204282633-1eda464f-2eea-4793-b57e-5c2e7047148d.png">














