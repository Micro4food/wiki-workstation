# wiki-workstation

Welcome to the wiki of the workstation of Micro4food!


# Accessing the workstation

## VSCode
You need a program on your PC where you can access the **terminal via a command line**. There are many different programs for this, but I use Visual Studio Code. With this program you can also copy files from the workstation to your own computer and read and write files and scripts at the same time. 
 
### Download VScode
https://code.visualstudio.com/
### Install git bash 
you need the program to be able to read shell bash files, which is the programming language for linux. <br />
Here is a tutorial to select bash as your default language: <br />
**https://git-scm.com/downloads**<br />


### Install the extension ssh FS 
https://marketplace.visualstudio.com/items?itemName=Kelvin.vscode-sshfs <br />
This extension  makes it possible to acces the workstation in a folder format similar to a windows setup. It connects to the workstation via a ssh connection

Configure the connection to the workstation in ssh FS<br />

Fill in these fields:<br />
"Name": what you want the connection to be called. Can be anything eg. #Workstation” or your username<br />
“Host”: type in the IP address of the workstation: **10.11.200.20** <br />
“root” this is which directory you want to connect to. Write `/data01/$USER` <br />
“username”. your username <br />
“password” – choose prompt. You will have to type it in every time you want to log in. It is not recommended to put the password in this configuration, as it is not very safe. <br />

![ssh FS](https://github.com/SchoofsKelvin/vscode-sshfs/raw/HEAD/media/config-editor.png)

4.	Log in<br />
If you are not working connected to Scientific Network SouthTyrol, you need to access it first through the University VPN<br />
Log in using an ssh connection directly via the terminal: 


### Log in via terminal
```
$ ssh -X $USER@10.11.200.20
```
### Log in via ssh fs to access folder 
In SSH FS, right click on the configured connection (upper left corner) and select **Add as workspace folder**<br />
At prompt, put in password<br />	
In the explorer, right click on the Workspace folder and click on **“open remote SSH terminal”**. It will not require a password prompt, since you already typed it in when you logged in to workspace folder. It should have started a terminal directly in `/data01/$USER` <br />	

First time you log in – change the password!<br />
```
$ passwd
```
![change password](https://cdn.mos.cms.futurecdn.net/LU7wmpZXnggLT85ZLYK5Gh-970-80.png)

## File transfer
You can transfer files to/from the workstation through VScode, but a quicker and more controlled way is through a file sharing program like **Filezilla** or **WinSCP**. Access the workstation with the same configurations as for VScode. 

# The Linux terminal
To learn how to navigate the linux terminal, please do a tutorial for the basic commands. For example how to move through the directories, copy, move and delete files, list directories and files and so on. <br />
https://ubuntu.com/tutorials/command-line-for-beginners#1-overview<br />

For example, you need to know how to move in the terminal 
```
$ mv
$ cd 
```

How to list read, copy, delete files, make directories etc
```
$ ls
$ nano
$ cp
$ rm
$ mkdir
```


# User storage

### /data01/$USER
every user also has a directory in /data01/$USER <br />
This is where you store your data, scripts, log files, intermediate files and results.<br />
For now this is unlimited, but if we are many that uses the workstation there will be a limit of 3-4TB of data storage per person. <br />
**You are only supposed to be able to write files in these two directories, if you can do it somewhere else, let Systemadmin (Lena) know immediately!**<br />
The files are backed up daily, so if you delete something irreplaceable (like raw data not stored somewhere else or files created in a stochastic way and can’t be reproduced) let sysadmin know. Generally things that will generate the same output and done quickly you don’t need to restore, just rerun.

### /home/$USER
Every new user has a directory (folder) in /home/$USER <br />
this has limited storage and is only used for configuration files. <br />
**DON’T DO ANY ANALYSES OR STORE DATA IN THE /HOME FOLDER**

### A note on storage:
In order to save space, use symbolic (soft) links to eg. raw data. <br />
```
$ ln -s /path/to/file.fasq.gz /path/to/where/you/want/to/put/it
```
Always compress big files to save space! <br />
Compress fastq files to fastq.gz (most software can work with this, otherwise use zcat to pipe the compressed file through a command without decompressing it first:
 ```
 $ zcat file.gz | software -options >out.example). 
 ```
 It's the same with bam files, which are binary version of sam files (alignment files). Also, sorted bam files take up much less space while compressed, so use `samtools sort` to sort them


 
# Running bioinformatic analyses and scripts with conda
All software is installed by the System Administrator (Lena). This is to prevent the accidental removal or changing of important software or files. 

If you want a new software downloaded, please send Lena an email.

Software is run through the environment manager program called **Anaconda3**. You therefore have to “activate” an environment where the software is excecutable before you can use it: 
```
$ conda activate bowtie2                        # activate the environment with the software
$ bowtie2 sample.fastq reference.fa             # run your script
$ conda deactivate bowtie2                      # deactivate the environment 
```
To find a list of environments/software installed on the workstation:
```
$ conda list
```

# Use of computing resources
CPU/threads and RAM memory <br />
To speed up your jobs, bioinformatic software usually have options that specify how much resources to use. There is usually a default value, but software can run many times faster with a higher CPU usage. Check in the options of the software, it is often specified with `-t` or `--thread` but can be something different. 


# Tips and tricks
Use the tab button to auto complete the name of a file or directory in the terminal<br />
Ctrl+arrow button will jump through separated fields in any text, including the terminal (also in word files)<br />
For loops are your friend. Instead of running the same analysis on different samples one after another, create a loop that will automatically start one job after the first one is finished

For all that is holy, **remember to make comments in your scripts**. You will not remember what a command is for or how to run it after a few months. 
