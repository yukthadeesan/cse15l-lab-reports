# LAB REPORT 1
My version of a tutorial to log into a course specific account
## Installing VScode
I already had VS Code downloaded on my laptop, but following the link [https://code.visualstudio.com/] was pretty straightforward
It looks something like this:
<img width="1440" alt="Screenshot 2022-09-30 at 9 25 20 PM" src="https://user-images.githubusercontent.com/114612660/193392417-55a479f2-8e6c-4aed-9ea9-991b1d0943b6.png">

## Remotely Connecting

To connect your account, simply use the command ssh cs15lfa22zz@ieng6.ucsd.edu (with your credentials) on the terminal and enter your password. 
When you enter your password, you should be connected to the server. 
<img width="1440" alt="Screenshot 2022-09-30 at 9 30 48 PM" src="https://user-images.githubusercontent.com/114612660/193392587-bee1fabc-4b6d-4a22-864e-73a151b22314.png">

## Trying Some Commands

Once you are connected to the server, try commands like cd, ls, pwd, rm, cat or any of the following ones that I have tried. You can try adding or deleting files as well.
<img width="1440" alt="Screenshot 2022-09-30 at 7 57 26 PM" src="https://user-images.githubusercontent.com/114612660/193392732-f3d5d622-2c58-4e42-aaf5-6df058e1be29.png">
<img width="1440" alt="Screenshot 2022-09-30 at 7 57 43 PM" src="https://user-images.githubusercontent.com/114612660/193392741-d56c00c6-d084-451c-8606-7ec5fbec4d5c.png">

## Moving Files with scp
Now you can run files from your computer on the server remotely. I tried creating a file called WhereAmI.java on my computer that looks like this:
<img width="591" alt="Screenshot 2022-09-30 at 9 40 20 PM" src="https://user-images.githubusercontent.com/114612660/193392853-7aca59a9-d6ab-480b-bc9b-c1262a59be59.png">

After that, trying to compile and run it on the client would look something like this.
<img width="1071" alt="Screenshot 2022-09-30 at 8 10 54 PM" src="https://user-images.githubusercontent.com/114612660/193392894-6455c99d-8ea4-44b6-84e4-ad5051d6adda.png">

With the same couple lines of code, you would also be able to run the file on the server. 

## SSH Keys
In this next step, we try to create two files, one public and one private. We do so because we will be able to access files without the interruption of having to enter the password while we are using it. WE try using the ssh keygen command to create twp files which we would be able to access with our personal username and path, and then use the public file. 
<img width="1440" alt="Screenshot 2022-09-30 at 9 13 52 PM" src="https://user-images.githubusercontent.com/114612660/193393023-cfd5e1d7-888d-4796-be57-088a90a80ad7.png">
 Unfortunately in this step, even though I tried multiple times to set up using ssh keygen and was able to follow through most of the lines of code, I was only able to access the private file, and had to enter the password every time. 


## Optimizing Remote Running
Now we will be able to run our code on file on the server. We can use the commands that we tried earlier on these files. You can also use the up-arrow to use previor commands or the ";" to write multiple commands on the same line. 
<img width="1440" alt="Screenshot 2022-09-30 at 9 15 37 PM" src="https://user-images.githubusercontent.com/114612660/193393003-67f9c82b-6834-4152-8d73-186a68965c2b.png">
