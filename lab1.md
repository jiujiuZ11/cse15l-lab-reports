# Lab Report 1
## 1.The 'cd' Command
### a. With No Arguments
```
[user@sahara ~]$ cd
[user@sahara ~]$ pwd
/home
```
**Working Directory: /home**  
Having no arguments for command implies that the command is executed with its default behavior or settings.
There is no direct output.  
Running cd with no arguments takes you to your home directory.   
No error.  


### b. With a Directory Path argument
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
**Working Directory: /home/lecture1**  
"With a directory path argument" means I'm providing a specific directory location in the filesystem to that command. This directory location informs the command where to operate or what to act upon. In this case, lecture1.  
There is no direct output but the command navigates to the lecture1 directory from the current working directory.  
No error.  


### c. With a File Path Argument
```
[user@sahara ~/lecture1]$ cd lecture1/Hello.java
bash: cd: lecture1/Hello.java: No such file or directory
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
**Working Directory: /home/lecture1**  
"With a file path argument" means I'm specifying the location of a particular file in the filesystem for that command to act upon.  
This path directs the command to operate on or interact with that specific file. In this case, Hello.java.  
The out put is a error message indicating "No such file or directory".  
There is an error because we can't navigate to a file using cd.  


## 2. The 'ls' Command
### a. With No Arguments
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
**Working Directory: /home/lecture1**  
Out put:Hello.class  Hello.java  messages  README  
Running the ls command with no arguments will list the contents of the current working directory. 
No error.  

### b. With a Directory Path argument
```
[user@sahara ~/lecture1]$ ls /home/lecture1/messages
en-us.txt  es-mx.txt  jp-ja.txt  zh-cn.txt
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
**Working Directory: /home/lecture1**  
When giving a directory path to the ls command, it will list the contents of that specific directory rather than current workingLists all files within the messages directory inside lecture1.  
No error. 

### c. With a File Path Argument
```
[user@sahara ~/lecture1]$ ls Hello.java
Hello.java
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
**Working Directory: /home/lecture1**  
If I provide a file path to the ls command, it will simply display that file name if it exists.  
No error.  

## 3. The 'cat' Command
### a. With No Arguments
```
[user@sahara ~/lecture1]$ cat
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
**Working Directory: /home/lecture1**  
Running cat without arguments waits for input from the user. To exit, have to press CTRL+D. Display what you entered.
No error.

### b. With a Directory Path argument
```
[user@sahara ~/lecture1]$ cat lecture1/messages
cat: lecture1/messages: No such file or directory
[user@sahara ~/lecture1]$ cat messages
cat: messages: Is a directory
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
**Working Directory: /home/lecture1**  
Output: Error message indicating "Is a directory".  
'cat' expects a file path, not a directory path.
If provide a directory path to cat, it would result in an error, because cat expects file paths.

### c. With a File Path Argument
```
[user@sahara ~/lecture1]$ cat messages/en-us.txt
Hello World!
[user@sahara ~/lecture1]$ cat README
To use this program:

javac Hello.java
java Hello messages/en-us.txt
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
**Working Directory: /home/lecture1**  
The cat command is designed to display the contents of files. If you provide a file path to cat, it will show you the contents of that file. 
No error.  









