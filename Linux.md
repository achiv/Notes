# Milestone #1 - The Linux Terminal
## pwd
* You can use the ```pwd``` command to print the working directory..
* The present working directory is ```/home/crio-user```. Each linux user gets their own home directory. All user home directories are in ```/home```. The username here is ```crio-user``` and hence the *"Home"* directory of ```crio-user``` is ```/home/crio-user```.

## ls 
* To list the contents of a directory, you use the ls command (short for list). When you run the ls command without any arguments, it lists the contents of the present working directory by default.

## cd
* You can change to a different directory using the cd command (short for change directory).

##### NOTE : The pound sign # is used to write comments. Everything after the first # is ignored.

* There is a symbol to denote a user’s home directory. The tilde (~) sign
* ```cd ~``` will take you to your home directory.
* ```ls ~``` will list the contents of your home directory.
* There is a symbol to denote a user’s previous directory. The hyphen (-) sign
* ```cd -``` will take you to the previous working directory

### Q. What if you execute the ```cd``` command without any destination? Can you try it and see where it takes you? 
* If you don’t provide any argument to the ```cd``` command, it defaults to the user’s home directory. The ```ls``` command defaults to the present working directory.

### Q. If the currently logged in user is ```linux-rocks```, which is the user’s home directory path?
* ```/home/linux-rocks```

### Q. What does the ```ls``` command do?
* List files, sub-directories and executables in a directory

### Q. What happens when you type ```cd ~```?
* Current working directory changed to the currently logged in user’s home directory

### Q. Which of the following commands list the contents of the user’s home directory irrespective of the current working directory? (Assume the logged in user is "linux-rocks")
* ```ls /home/linux-rocks```
* ```ls ~```

<hr>

# Milestone #2 - File system and Files
## The Linux Directory Structure
![Linux Dir](https://raw.githubusercontent.com/achiv/Notes/main/images/Linux_dir.png)
![Linux Table](https://raw.githubusercontent.com/achiv/Notes/main/images/Linux_table.png)

## File Permissions
```
bash: ./run.sh: Permission Denied
```

![Linux Permissions](https://raw.githubusercontent.com/achiv/Notes/main/images/Linux_perm.png)

* ```chmod``` command lets us change the access mode of a file. To add executable permission, we use ```chmod +x <filename>```.
```
chmod +x run.sh
```

### Q. Find a command that prints out all sub-directories and files recursively
* ```ls -R <directory>```
* ```tree <directory>```

### Q. Try to remove the write permission for the ```run.sh``` file. Will you be able to edit the file after this?
* Use ```chmod -w run.sh``` in the directory where the file is to remove write permission. Open the file for editing using a text editor. Eg: ```nano run.sh```. Make some changes and hit ```Ctrl-X``` to try saving & closing the changes. Enter ```Y``` when asked to save modified buffer (basically changes made) and then hit ```Enter``` to overwrite the current file.
* The editor won’t allow to save any changes made

### Q. We looked at how to change the access mode for a file using ```chmod```. Can you find out how we can change the owner of a file?
* Use the ```chown``` command to change file ownership. ```chown root run.sh``` tells to change ownership of the ```run.sh``` file to root user. Using ```sudo``` might ask you to enter a password.

### Q. The ```-l``` flag used with ```ls``` lists the contents in long form whereas ```-t``` flag sorts the files according to their modification time. What if we need to do both?
* We can use multiple flags along with the commands at a time. The usage could be like below
```
$ ls -l -t
$ ls -lt
```

### Q. Which of the following commands can list the contents of the /var/log directory?
* ```ls /var/log```
* ```cd /; ls var/log```
* ```cd /var; ls log```
* ```cd /var/log; ls```

### Q. Which is the parent directory of all the directories in the Linux file system?
* ```/```
* The root directory

### Q. Find out which of the below commands can be used to create a symbolic link?
* ```ln```

### Q. Which of the following is true regarding the contents of the ```/bin``` folder?
* Contains executable files
* Contains files like ```pwd```, ```ls```, ```cd```

### Q. The ```ls -l``` command lists contents of a directory in the long format. What does the ```ls -lh``` command do? (Hint: Use man page)
* List directory content details (like file size) in human readable format

### Q. Which of the following can be used to see previously executed commands?
* ```history```
* ```UP arrow```

### Q. Which of the following commands give read access to the "run.sh" file for users in the same group as that of the file?
* ```chmod +r run.sh```
* ```chmod g+r run.sh```
* ```chmod 444 run.sh``` (read-all)
* ```chmod 777 run.sh``` (all-all)

### Q. Which of the following data does "```ls -l```" not display?
* File creation date

### Q. What is the file permission needed if the owner and group can read and write only, but others cannot read, write or execute?
* ```rw-rw----```

<hr>

# Milestone #3 - Files and Directories
## mkdir
* ```mkdir``` is the command we need to make directories in Linux and we feed it the name of the new directory we want to create. 

## touch
Now, we need to add files. That’d be the ```touch``` command.

### Q. To create the ```dir1/subdir1``` directory, we can use ```mkdir dir1```, ```cd``` to ```dir1``` and then execute ```mkdir dir1/subdir1```. Can you find out if it’s possible to create the ```dir1/subdir1``` directories using a single ```mkdir``` call?
* We can use the ```-p``` flag with the mkdir call to create nested directories.
```
$ mkdir -p dir1/subdir
```

### Q. Does Linux provide some command to just move files from one directory to another rather than having us to do a copy first & then remove the original?
* Use the ```mv``` command to move files from one directory to another
```
$ mv run.sh dir1/subdir1/
```

### Q. On second thoughts, we decide to remove the subdir2 directory. How would you delete a directory?
* Use the ```rmdir``` command to delete an empty directory. If the file has contents, ```rm -rf``` command will have to be used. ```-r``` recursively deletes files in the directory.
```
$ rmdir dir1/subdir1
$ rm -r dir1/subdir1/
```

### Q. Which command will take you to the previous working directory? (Previous working directory != Parent directory)
* ```cd -```

### Q. How do you delete a directory named backup?
* ```rmdir backup```
* ```rm -rf backup```

### Q. How do you rename a file? 
* ```mv oldfile newfile```

### Q. Current working directory is ```/home/crio-user/Downloads/videos/series/english/got/season100/episode1```. Which of the below commands will take us to the ```/home/crio-user/Downloads/videos/series/english/got/season100/episode2``` directory?
* ```cd /home/crio-user/Downloads/videos/series/english/got/season100/episode2```
* ```cd ../episode2```
* ```cd ..; cd episode2```

<hr>

# Milestone #4 - Manipulating Files
## echo
* ```echo``` command is used to print out the value provided to it. By default, it prints the value to the terminal which is the "standard output". Try running ```echo 'Congratulations on running a bash script'```.

## grep
* ```grep``` command is used to filter/search for text using strings or patterns. It’s usage is ```grep <pattern> <file>```

## awk
* It uses space as a field separator (by default space is used as field separator but other field separators can be specified) and separates text into columns

## Feeding Output of a command to the Input of another
```
$ grep Memfree /proc/meminfo
MemFree: 1024 kB
$ grep MemFree /proc/meminfo > memFreeLine.txt
$ cat memFreeLine.txt
MemFree: 1024 kB
```

#### NOTE : Piping is a type of redirection in Linux used to send output of one command to input of another command. We had earlier written the output of ```grep``` to a file & then used it as input to ```awk```. Instead of this, we can use the Linux pipe operator (```|```) to redirect output of ```grep``` directly to input of ```awk```.

```
$ grep MemFree /proc/meminfo > memFreeLine.txt | awk '{print $2}' memFreeLine.txt
1024
```

### Q. We came across a couple of ways to redirect the output of a command. ```>``` operator writes output of a command to a file. Try running ```echo "Hello" > hello.txt``` command two times and cat content of hello.txt. Does it contain one Hello or two? How can we append data rather than overwrite it here when using redirection?
* The ```>``` operator overwrites data in the file and hence only one “Hello” will be saved. Use ```>>``` to append data.

### Q. The ```|``` operator sends output of a command as input to another. What if we needed to print the output of the first command to the terminal as well as redirect it to a file?
* The ```tee``` command is used to redirect output both to the terminal as well. Just like the shape of alphabet T, it redirects to the file as well as to the terminal.
```
$ cat hello.txt
Hello
Hello
$ wc hello.txt | tee count.txt
2 2 12 hello.txt
$ cat count.txt
2 2 12 hello.txt
```

### Q. What if I need to see the first 20 lines of the ```/var/log/syslog``` file? Is there some command that lets us fetch some lines from the starting of the file?
* Use the ```head``` command to view some lines of a file from the starting

### Q. What if you want to see contents of a file getting printed to screen as and when the file is being written to?
* Use the ```tail``` command to watch changes made to a file.

### Q. How do you continuously print lines that are being appended to file.log?
* ```tail -f file.log```

<hr>

# Milestone #5
### DATA ANALYSIS (need Advaned Linux)

<hr>

# Milestone #6
## Useful Shortcuts
* ```up arrow``` key → will bring up the last command that was executed. Each press will bring up the previous command executed.
* ```history``` → will print out a list of the previous commands executed.
* ```tab key``` → pressing the tab key can be used to auto-complete the directory and file names while typing paths or filenames.

<hr>




