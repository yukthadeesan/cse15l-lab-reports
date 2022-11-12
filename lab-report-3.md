# LAB REPORT 3

Some command line options for the command `find` with examples:

##  COMMAND OPTION 1
## **find -inum**

This command option returns the file (with its path) given its inode number. While sorting files, this command will be useful to find files using the inode number.   

### Example 1
Finding the file associated with the inode number '30566700' 

```
$ find technical/911report -inum 30566700 
```
Output:
```
technical/911report/chapter-7.txt
```
To check if I received the correct output, I traced back and looked at the file's inode number using the `ls -i` command:
```
ls -i technical/911report/chapter-7.txt
```
Output:
```
30566700 technical/911report/chapter-7.txt
```
### Example 2
Finding the file associated with the inode number '30567556' 
```
$ find technical  -inum 30567556
```
Output:
```
technical/government/About_LSC/Strategic_report.txt
```
Tracing back to cross-check:
```
ls -i technical/government/About_LSC/Strategic_report.txt
```
Output:
```
30567556 technical/government/About_LSC/Strategic_report.txt
```
### Example 3
Finding the file associated with the inode number '30567406' 
```
$ find technical  -inum 30567406
```
Output:
```
technical/biomed/cc3.txt
```
Tracing back to cross-check:
```
$ ls -i technical/biomed/cc3.txt
```
Output:
```
30567406 technical/biomed/cc3.txt
```

## COMMAND OPTION 2
## **find -maxdepth & find -mindepth**

The command option maxdepth finds files/directories that are in directory levels upto the given number. 
Here are three examples using the maxdepth command option:

### Example 4
Finding "biomed" in directory levels 1 and 2. (upto 2 levels)
```
$ find technical -maxdepth 2 -name "biomed"
```
Output:
```
technical/biomed
```
### Example 5
Finding files starting with "chapter" in directory level 1. 
```
$ find technical -maxdepth 1 -name "chapter*"
```
Output:
```
```
Files starting with "chapter" do not exist in directory level 1, hence the null output. 

### Example 6
Finding files starting with "chapter" in directory levels 1 and 2. Output shows all files that pass the criteria with their path. 
```
$ find technical -maxdepth 2 -name "chapter*"
```
Output:
```
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-13.1.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-3.txt
technical/911report/chapter-2.txt
technical/911report/chapter-1.txt
technical/911report/chapter-5.txt
technical/911report/chapter-6.txt
technical/911report/chapter-7.txt
technical/911report/chapter-9.txt
technical/911report/chapter-8.txt
technical/911report/chapter-12.txt
technical/911report/chapter-10.txt
technical/911report/chapter-11.txt
```
The command option mindepth finds files/directories that are in directory levels from the given number and above. 
Here are three examples using the mindepth command option:

### Example 7
Finding files with "biomed" in directory levels 3 and above.
```
$ find technical -mindepth 3 -name "biomed"
```
Output:
```
```
Files with "biomed" do not exist in directory levels 3 and up, hence the null output.

### Example 8
Finding files starting with "pmed" in directory levels 3 and above.
```
$ find technical -mindepth 3 -name "pmed*"
```
Output:
```
```
Files starting with "pmed" do not exist in directory levels 3 and up, hence the null output. 

### Example 9
Finding files starting with "d" in directory levels 3 and above. Output shows all files that pass the criteria with their path.
```
$ find technical -mindepth 3 -name "d*"
```
Output:
```
technical/government/About_LSC/diversity_priorities.txt
technical/government/Gen_Account_Office/d0269g.txt
technical/government/Gen_Account_Office/d01376g.txt
technical/government/Gen_Account_Office/d01121g.txt
technical/government/Gen_Account_Office/d03419sp.txt
technical/government/Gen_Account_Office/d03273g.txt
technical/government/Gen_Account_Office/d03232sp.txt
technical/government/Gen_Account_Office/d01591sp.txt
technical/government/Gen_Account_Office/d01145g.txt
technical/government/Gen_Account_Office/d01186g.txt
technical/government/Gen_Account_Office/d02701.txt
technical/government/Media/defend_yourself.txt
```
## COMMAND OPTION 3
## **find -type**
This command option is used to find all items of a certain type, either directory or file under a directory. 
Here are three examples using -type. 

### Example 10
Finding all **directories** under technical. 
```
$ find technical -type d
```
Output:
```
technical
technical/government
technical/government/About_LSC
technical/government/Env_Prot_Agen
technical/government/Alcohol_Problems
technical/government/Gen_Account_Office
technical/government/Post_Rate_Comm
technical/government/Media
technical/plos
technical/biomed
technical/911report
```
### Example 11
Finding all **files** under "911report". 
```
$ find technical/911report  -type f
```
Output:
```
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-13.1.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-3.txt
technical/911report/chapter-2.txt
technical/911report/chapter-1.txt
technical/911report/chapter-5.txt
technical/911report/chapter-6.txt
technical/911report/chapter-7.txt
technical/911report/chapter-9.txt
technical/911report/chapter-8.txt
technical/911report/preface.txt
technical/911report/chapter-12.txt
technical/911report/chapter-10.txt
technical/911report/chapter-11.txt
```
### Example 12
Finding all **directories** under "government" directory
```
$ find technical/government -type d
```
Output:
```
technical/government
technical/government/About_LSC
technical/government/Env_Prot_Agen
technical/government/Alcohol_Problems
technical/government/Gen_Account_Office
technical/government/Post_Rate_Comm
technical/government/Media
```
