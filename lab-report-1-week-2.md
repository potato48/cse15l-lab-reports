

# Lab Report 1
![If no work, oops](amogus.png)



## Installing VScode 
---
Go to the following link and follow the instructions to download Visual Studio Code for your operating system. 
[https://code.visualstudio.com/](https://code.visualstudio.com/)

After VS Code is installed, you should be able to start VS Code and arrive a window that looks similar to the picture shown below.

![OOPS!](image24.png)
  
  

## Remotely Connecting
---
If you are on Windows, you must first install the OpenSSH client which can be found by going to Windows' Settings > Apps & Features > Optional Features 

![OOPS!](openssh.png)

Then look up your account for CSE15L at:
[https://sdacs.ucsd.edu/~icc/index.php](https://sdacs.ucsd.edu/~icc/index.php)

In Visual Studio Code, enter the following command in a terminal with the brackets replaced with the corresponding letters in your account:
```
$ ssh cs15lwi22[]@ieng6.ucsd.edu
```

If it is your first time connecting to this server, you'll likely get a message asking if you want to continue connecting. Type in `yes`, hit enter, and type in and enter your password. Your terminal should then look something like the following image along with the lines about the previously mentioned message:
![OOPS!](image47.png)

## Trying Some Commands
---
Now that you are connected to the server, you can try out various commands and see what they do. Here are some you can try out:
- cd ~
- cd
- ls -lat
- ls -a
- cp /home/linux/ieng6/cs15lwi22/public/hello.txt ~/
- cat /home/linux/ieng6/cs15lwi22/public/hello.txt

Running `cd ssh` for instance moves the directory that you're in.
![OOPS!](cd.png)

Running `ls` prints out all the files and folders within the directory that you're in.
![OOPS!](ls.png)

You can also enter the command `exit` to log out of the remote server.  
![oops](exit.png)

## Moving Files with scp
---
First create a file on your computer called WhereAmI.java with the following code:
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
Running it with `java` and `javac` on your computer will give you details about your own computer like:  
![OOPS!](examplewhere.png)

Next, in the same terminal in the directory where you created the file, run the following command with your own username (in place of the brackets):  
`scp WhereAmI.java cs15lwi22[]]@ieng6.ucsd.edu:~/`

If you then connect to the server like before and enter `ls`, the WhereAmI.java file should be there. While connected to the server, you can then run `java` and `javac` and it will run on the server's computer.
  
  
## Setting an SSH Key
---
On your computer, enter the following command to generate an SSH key:  
`ssh-keygen -t ed25519`  
Hit enter twice to save the file with no passphrase. Your terminal should look something like this:
![OOPS!](sshdone1.png)  
Then enter the following commands:
```
Start-Service ssh-agent
ssh-add []
```
The brackets should be replaced with the location of the private ssh key (without .pub). It can be found on the line "Your identification has been saved in..."  
  
Next run the following command to copy the public ssh key (the one ending in .pub) to the server with the brackets replaced with the location of the public key (location found on the line below where the terminal printed the private key location):  
`scp [] cs15lwi22@ieng6.ucsd.edu:~/.ssh/authorized_keys`  
  
Now you should be able to run `ssh` or `scp` without entering your password.
![OOPS!](image47.png)

## Optimizing Remote Running
---

Using quotes (""), semi-colons (;), and the up and down arrow keys can help you optimize your time spent running and testing programs remotely. The arrow keys will cycle through your most recently entered commands in reverse chronological order.  

Quotes can used in conjunction with `ssh` to run a command on the server and immediately disconnect:
![OOPS!](quotes.png)  

Semi-colons can be used to run serveral commands using the same line:  
![OOPS!](multi.png)  

If you want to run multiple commands directly on the server, use semi-colons within quotes:
![oops](multi2.png)  
The command shown in the picture runs the following three commands on the server directly before disconnecting:  
```
javac WhereAmI.java
java WhereAmI.java
ls
```



