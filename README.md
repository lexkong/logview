# logview

### WHAT IS LOGVIEW?

logview is a sample tool for you to monitor your log files. It allow you specify your own "error" message via a awk file. Through this way, it is very flexible for you to specify your "error" message. Also, it can send the "error" message to your ttys or email according to your choose.

### FEATURES

+ Very efficient when monitor large log files, it has a suitable algorithm for these
   files

+ A high degree of customization, logview use a awk file to filter "error" messages.
   So, you can filter ANY string if you provided a suitable awk file.

+ Email and notice function, logview can email "error" messages to you or send "error"
   messages to your ttys.

+ Can set the monitoring frequency.

+ Set color theme.

+ Can monitor more than one files.

+ Other useful features.

"error"  message: the string you want to find out.You may take it as a wrong message or a right message.

### INSTALLATION

```
$ git clone https://github.com/alex8866/logview
$ cd logview
```
Just cp logview to your $PATH, eg: $HOME/bin

### USING LOGVIEW

This is a powerful tool to monitor log files, especially large log files. And it is easy to use, please do not scared by the huge output of `logview -h` or `logview --help`.

#### 1. Write your awk file

This script use a awk file to grep your "error" string, the script use it via `awk -f $awkfile $logfile`
If you do not want to write a awk file, you can use:
```
$ logview -a
```
to get an example awk file named: awk.example in your current directory, but please remember that awk.example only get the line which contains an "error" or "failed" word. (Not case-sensitive)

#### 2. A very simple logview command line (logview [ OPTIONS ] FILE1 -f FILE2 [ OUTPUT ] ...)

```
$ touch $HOME/logfile_name
$ logview awk.example -f $HOME/logfile_name
```

Open another terminal and run:

```
$ echo "error" >> $HOME/logfile_name
$ echo "ERROR" >> $HOME/logfile_name
$ echo "failed" >> $HOME/logfile_name
$ echo "FAILED" >> $HOME/logfile_name
```

Check your first terminal

#### 3. Some examples

First touch test file: error.txt and test.txt then run logview and wirte error messages in the two files

```
$ logview awk.example -f error.txt -f test.txt --font-color=red --font=bold -s 5s -c ./command -m lkong@redhat.com --mail-time=5m

testcommand

17:27:50|error.txt|error

testcommand

17:27:50|error.txt|error

$ cat command

echo testcommand
```

***What does this command mean?***

-f: specify the log file, so this command monitor two files: error.txt and test.txt

--font-color=red: With this option, the "error" message will be colored by red.

--font=bold, the font of the "error" message

-s 5s: specify the scan frequency. default is 5s, here I set it to 5s

-c ./command: When the "error" messages occurred, logview will call this script(print yesyes to standard output)

-m: mail the "error" messages to the mail list.

--mail-time=5m: sent the mail every 5 minutes


**Another example:**

```
$ logview awk.example -f error.txt -f test.txt --font-color=red --font=bold -s 5s -c ./command -m lkong@redhat.com --mail-time=5m errorfile.txt --notice=one

testcommand

Message from aaron@Alex on <no tty> at 17:43 ...

20131129 17:43:03| error

EOF

testcommand
```

***What does this command mean?***

errorfile.txt: Instead of print the "error" messages to the standard output, this command print the "error" message to file errorfile.txt. Note: This will be auto enabled when you provide the second file.

--notice=one: When the "error" messages occurred, logview will send the messages to your current tty. If you set --notice=all, it will send the messages to all your tty.

Notice: When you print the "error" messages to the standard output, the notice function will be auto disabled, even if you specify the --notice option. Because you select to print the "error" messages to the standard output, so you are always noticed by the standard output.

#### 4. Other useful functions
There are many powerful functions, you can use:

```
$ logview -h
```

to get more details

### TODO

+ Add more function or feature to this small tool.

+ Add analysis function to it, this can give you some useful information about the log

+ Improve it, make it smaller overhead.

### CAN I HELP?

If you have any idea or find any BUG, feel free to contact me.


### VERSION

0.0 - First version :)


###LICENSE

GNU GPL, see the LICENSE file for details.

### CONTACT

Alex

Email:
lkong@redhat.com

Please email me about problems, experiences, patches, fixes, etc.
