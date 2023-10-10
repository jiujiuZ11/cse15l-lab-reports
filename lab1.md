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


