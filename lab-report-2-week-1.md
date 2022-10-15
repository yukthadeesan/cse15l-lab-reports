# LAB REPORT 1
My version of a tutorial to log into a course specific account
## Installing VScode
I already had VS Code downloaded on my laptop, but following the link [VSCode](https://code.visualstudio.com/) was pretty straightforward. The homepage looks something like this:

<img width="1440" alt="Screenshot 2022-09-30 at 9 25 20 PM" src="https://user-images.githubusercontent.com/114612660/193392417-55a479f2-8e6c-4aed-9ea9-991b1d0943b6.png">

## Remotely Connecting

To connect your account, use the command `ssh cs15lfa22zz@ieng6.ucsd.edu` (with your credentials) on the terminal and enter your password. You will be able to find your credentials on your UCSD accounts page. Before connecting to the remote server, change the password for your course account (cse15l account) and you should be able to get this page:

<img width="747" alt="password change" src="https://user-images.githubusercontent.com/114612660/195961967-7e197ae1-e307-49ed-be7a-5debed7fda95.png">


After giving 15-60 minutes for the password to get updated, you type in the command:
`ssh cs15lfa22zz@ieng6.ucsd.edu`
in the terminal and you will be prompted to enter your password.

<img width="1440" alt="Screenshot 2022-09-30 at 9 30 48 PM" src="https://user-images.githubusercontent.com/114612660/193392587-bee1fabc-4b6d-4a22-864e-73a151b22314.png">

Just remember that you type in the password that there will be no response and will remain blank, but your password will be taken as input and you will be able to login and connect to the server. 

## Trying Some Commands

Once you are connected to the server, you can try commands like 
```
cd ~
cd
ls -lat
ls -a
cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/
cat /home/linux/ieng6/cs15lfa22/public/hello.txt
```
or any of the following ones that I have tried.
You can try adding or deleting files using 
`rm` <filename> as well.
 
<img width="1440" alt="Screenshot 2022-09-30 at 7 57 26 PM" src="https://user-images.githubusercontent.com/114612660/193392732-f3d5d622-2c58-4e42-aaf5-6df058e1be29.png">
<img width="1440" alt="Screenshot 2022-09-30 at 7 57 43 PM" src="https://user-images.githubusercontent.com/114612660/193392741-d56c00c6-d084-451c-8606-7ec5fbec4d5c.png">

## Moving Files with scp
Now you can run files from your computer on the server remotely. I tried creating a file called WhereAmI.java on my computer that looks like this:
```
 class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```
 
After that, trying to compile and run it on the client (your own computer) would look something like this:
 
<img width="1071" alt="Screenshot 2022-09-30 at 8 10 54 PM" src="https://user-images.githubusercontent.com/114612660/193392894-6455c99d-8ea4-44b6-84e4-ad5051d6adda.png">
 
 Now, we use the command `ssh cs15lfa22zz@ieng6.ucsd.edu` to connect to the server and compile the code with 
 ```
javac WhereAmI.java
java WhereAmI
 ```
 This is the ouput as shown in the remote server:
 
 <img width="940" alt="image" src="https://user-images.githubusercontent.com/114612660/195962763-0b0811e3-0fbc-478d-b4f2-759377bc0d6c.png">

 We have successfuly created a connection to the server so that a program can be run from both the client as well as the server. 
 

## SSH Keys
In this next step, we try to create two files, storing a public key on the server and a private key on the client (on your personal computer). We do so because we will be able to access files without the interruption of having to enter the password while we are using it. We try using the `ssh-keygen` command to create two files which we would be able to access with our personal username and path, and then use the public file. 
 
 <img width="807" alt="image" src="https://user-images.githubusercontent.com/114612660/195968451-a56b8568-2e01-4a5f-9dad-749a47869623.png">
 
 This shows you information about where the public and private keys are saved and you can select where you want to store them on your computer. I have saved my file in `/Users/yukthadeesan/.ssh/id_rsa`
 
 Now on the server, if you run the command `mkdir .ssh`
 and back on client `scp (public filepath) cs15lfa22@ieng6.ucsd.edu:~/.ssh/authorized_keys` (with your username and filepath), you will be able to login to the server without having to enter your password, i.e. just by hitting 'enter'
 
 <img width="780" alt="image" src="https://user-images.githubusercontent.com/114612660/195968750-f3aa2c0c-cff2-48dd-b9a5-bf6816e3508c.png">


## Optimizing Remote Running
Now we will be able to run our code on file on the server. We can use the commands that we tried earlier on these files. You can also use the up-arrow to use previor commands or the ";" to write multiple commands on the same line. I have tried out some commands like
 ```
  cp WhereAmI.java OtherMain.java; javac OtherMain.java; java WhereAmI
 ```
<img width="1440" alt="Screenshot 2022-09-30 at 9 15 37 PM" src="https://user-images.githubusercontent.com/114612660/193393003-67f9c82b-6834-4152-8d73-186a68965c2b.png">
