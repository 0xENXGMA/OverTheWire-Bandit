# OverTheWire - Bandit

- [OverTheWire - Bandit](#overthewire---bandit)
  - [Level 0](#level-0)
  - [Level 0 → Level 1](#level-0--level-1)
  - [Level 1 → Level 2](#level-1--level-2)
  - [Level 2 → Level 3](#level-2--level-3)
  - [Level 3 → Level 4](#level-3--level-4)
  - [Level 4 → Level 5](#level-4--level-5)
  - [Level 5 → Level 6](#level-5--level-6)
  - [Level 6 → Level 7](#level-6--level-7)
  - [Level 7 → Level 8](#level-7--level-8)
  - [Level 8 → Level 9](#level-8--level-9)
  - [Level 9 → Level 10](#level-9--level-10)
  - [Level 10 → Level 11](#level-10--level-11)
  - [Level 11 → Level 12](#level-11--level-12)
  - [Level 12 → Level 13](#level-12--level-13)
  - [Level 13 → Level 14](#level-13--level-14)
  - [Level 14 → Level 15](#level-14--level-15)
  - [Level 15 → Level 16](#level-15--level-16)
  - [Level 16 → Level 17](#level-16--level-17)
  - [Level 17 → Level 18](#level-17--level-18)
  - [Level 18 → Level 19](#level-18--level-19)
  - [Level 19 → Level 20](#level-19--level-20)
  - [Level 20 → Level 21](#level-20--level-21)
  - [Level 21 → Level 22](#level-21--level-22)
  - [Level 22 → Level 23](#level-22--level-23)
  - [Level 23 → Level 24](#level-23--level-24)
  - [Level 24 → Level 25](#level-24--level-25)
  - [Level 25 → Level 26](#level-25--level-26)
  - [Level 26 → Level 27](#level-26--level-27)
  - [Level 27 → Level 28](#level-27--level-28)
  - [Level 28 → Level 29](#level-28--level-29)
  - [Level 29 → Level 30](#level-29--level-30)
  - [Level 30 → Level 31](#level-30--level-31)
  - [Level 31 → Level 32](#level-31--level-32)
  - [Level 32 → Level 33](#level-32--level-33)
  - [Level 33 → Level 34](#level-33--level-34)

## Level 0

### Level Goal

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The *username* is **bandit0** and the *password* is **bandit0**.

### Solution

For this first level we must connect to the user **bandit0** with the data provided, we can do it with the following command:

``sshpass -p 'bandit0' ssh bandit0@bandit.labs.overthewire.org -p 2220``

**Remember to use port 2220 to connect.**

## Level 0 → Level 1

### Level Goal

The password for the next level is stored in a file called readme located in the home directory.

### Solution

Once connected, we must look for the content of the file called readme, this file is located in the personal directory of the user **bandit0**.
To view it we can use the command:

```
bandit0@bandit:~$ cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```

There we have the password of the user **bandit1** and so we can continue with the next level.

## Level 1 → Level 2

### Level Goal

The password for the next level is stored in a file called **-** located in the home directory.

### Solution

First of all to view the files in the current directory we can use the ``ls`` command:

```
bandit1@bandit:~$ ls
-
```

If we try to display the file as we did before, i.e. ``cat -``. We will not be able to, because bash interprets the dash as an option of the cat command.
However, we can display the file in several ways:

We can use the absolute path of the file, using the command ``pwd`` we can see what is the actual path where the file is located.

```
bandit1@bandit:~$ pwd
/home/bandit1
```

So, the path to the file would be ``/home/bandit1/-``, if we now try to display the file by providing the absolute path, we will see that it works.

We can also display it using the relative path ``./-``.

## Level 2 → Level 3

### Level Goal

The password for the next level is stored in a file called spaces in this filename located in the home directory

### Solution

To be able to display files containing spaces, we must insert the file name between quotes so that bash interprets it as a text string.
In this case it would be like this.

```
bandit2@bandit:~$ cat "spaces in this filename"
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```

## Level 3 → Level 4

### Level Goal

The password for the next level is stored in a hidden file in the inhere directory.

### Solution

At this level, the file is hidden inside the **inhere** directory, using the command ``cd`` we can enter this directory. 
```
bandit3@bandit:~$ cd inhere/
```

In order to list the hidden files from directory we can use ``ls`` with the option ``-a`` that shows the hidden files.

```
bandit3@bandit:~/inhere$ ls -a
. ..  .hidden
```

Once we find the file we can view it with cat, like this:

```
bandit3@bandit:~/inhere$ cat .hidden 
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```

## Level 4 → Level 5

### Level Goal

The password for the next level is stored in the **only human-readable** file in the **inhere** directory.

### Solution

If we list the files inside the **inhere** directory we can see that there are several:
```
bandit4@bandit:~/inhere$ ls        
-file00 -file01 -file02 -file03 -file03 -file04 -file05 -file06 -file07 -file08 -file09 -file09
```

In order to find the **only human-readable** file we can do it using the ``file`` command to see the file type. For example:

```
bandit4@bandit:~/inhere$ file ./-file00
./-file00: data
```

**As you can see we use the *relative path* of the file since it starts with a **dash** and it won't work as we saw in **Level 1****

While the ``file`` command reports what type of file each one is, instead of running the command each time with each file. We can make use of **bash wildcard characters**. In this case we can use the ``*``.

For example:

```
bandit4@bandit:~/inhere$ file ./-file*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: Non-ISO extended-ASCII text, with no line terminators
```

As you can see ``-file*`` includes all the files that begin with the name **-file**, as in our case all the files are called the same and only the number at the end changes, so we replace the number with ``*``.

Now that we know that the file that is **only human-readable** is **-file07**, we can visualize it:

```
bandit4@bandit:~/inhere$ cat ./-file07
lrIWWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```

But you may be wondering, what if the file names do not have the same name pattern?

In this case we can make use of the ``find`` command, with this command we can search for all kinds of files whether they are directories, links, and so on.
 For example:

```
bandit4@bandit:~/inhere$ find . -type f
./-file03
./-file06
./-file08
./-file07
./-file04
./-file00
./-file01
./-file02
./-file09
./-file05
```


As you can see in the command we indicate the current directory (**inhere**) with a **.** and the file type ``-type``, in this case as they are files is **-f** (if they were directories it would be **-d**).

But then as we can see, this only shows us the files that it has found in the current directory, but does not tell us the type of file it is.
For this we can chain the ``xargs`` command with the use of a pipe ``|`` **(This allows you to redirect the output of one command to the input of another)**\
``xargs`` is used to execute a command on the standard input. In this case our input is the result of the ``find . -type -f``
Then ``xargs`` will execute ``xargs file`` to see the type of each of the files.

So the complete command would be as follows:

```
bandit4@bandit:~/inhere$ find . -type f | xargs file
./-file03: data
./-file06: data
./-file08: data
./-file07: ASCII text
./-file04: data
./-file00: data
./-file01: data
./-file02: data
./-file09: Non-ISO extended-ASCII text, with no line terminators
./-file05: data
```

## Level 5 → Level 6

### Level Goal

The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:

- Human-readable
- 1033 bytes in size
- Not executable

### Solution

In this level we can see that there are several directories inside the **inhere** directory, if we had to look for this file manually it would take a long time.
For this we are going to use again the **find** command that we used in **Level 4**.
To do this we have to use some additional options that the ``find`` command provides us with:

**-type f** → file type\
**-readable** → human-readable\
**! -executable** → non-executable\
**-size** → specify file/directory size\

So the actual command would be:

```
bandit5@bandit:~/inhere$ find . -type f -readable -size 1033c ! -executable
./maybehere07/.file2
```

**c stands for *bytes***

As a result, the file ``./maybehere07/.file2`` is the one that contains the password for the next level.

```
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```

## Level 6 → Level 7

### Level Goal

The password for the next level is stored **somewhere** on the server and has all of the following properties:

- Owned by user **bandit7**
- Owned by group **bandit6**
- 33 bytes in size

### Solution

Here we can make use of the find command again, with new options:

**-user** → specify the owner of the file\
**-group** → specify the group the file belongs to\
**-size** → specify file/directory size\

The complete command would be:

``find / -type f -user bandit7 -group bandit6 -size 33c``.

If we launch the command like this, it will throw a lot of errors because we do not have enough permissions to search certain directories.
If we want to hide these errors to make it less annoying we can redirect the errors to ``/dev/null``. This is like a black hole in the system where everything that is sent is discarded.

So the actual command would look like this:

```
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2> /dev/null
/var/lib/dpkg/info/bandit7.password
```

**2> is the method to redirect only the errors to /dev/null and thus not display them in the console**.

Now we can view the password that contains the file we have found:

```
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```

If you want to learn more about redirections in Linux, click [here](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)

## Level 7 → Level 8

### Level Goal

The password for the next level is stored in the file **data.txt** next to the word **millionth**.

### Solution

If we run ``cat data.txt`` we will see a bunch of nonsense.

```
bandit7@bandit:~$ cat data.txt
Worcester's fyKdWWh7VVgusiIKPygHJe6TlkDHhLHl
arousal r8mfBurE2OvHu8NFQc7mJ2x14iNjwkin
counterespionage's 4jmzYqFkqwciprPrJleFCI9tyjbXBtdt
Willard's ctbhPNPRDGAll4Whhsrz3Mwv6qJHM8Et
midwife Kk9VZkoTUNUfmIa031vovUN2UKksZ56S
<SNIP>
```

We know that the password is next to the word **millionth** so we can filter for that word by using the ``grep`` command in conjunction with the ``cat`` command.

```
bandit7@bandit:~$ cat data.txt | grep millionth
millionth     TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```

If we do this we will see the password next to the word millionth. If we want to keep only the password we can do it using the command ``awk``.

This command is used to process and manipulate data in text files.
In our case we want to keep the password alone, for this we are going to do it with the following command:

``awk '{print $NF}'``

**$NF is a predefined variable of the ``awk`` command that refers to the last field of a line of text, which in our case is the password.**

So the complete command would look like this:

```
bandit7@bandit:~$ cat data.txt | grep millionth | awk '{print $NF}'
TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```

## Level 8 → Level 9

### Level Goal

The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only **once**.

### Solution

At this level, we have to look for the password in a **data.txt** file where several lines of text are repeated and the only one that is not repeated is the password.
For this we can use the commands **sort** and **uniq**.
The **sort** command is used to sort the lines of a text file while the **uniq** command removes the lines that are repeated.

The command would be:
```
bandit8@bandit:~$ cat data.txt | sort | uniq -u
EN632PlfYiZbn3PhVVK3XOGSlNInNE00t
```

**The -u option refers to *unique lines***

## Level 9 → Level 10

### Level Goal

The password for the next level is stored in the file **data.txt** in one of the few **human-readable strings**, preceded by several '=' characters.

### Solution

The statement at this level tells us that there are only a few **human-readable strings**. If we try to ``cat`` the file **data.txt** we will see a bunch of nonsense.
For this we can use the **strings** command which is used to extract **human-readable strings** from a file.

Now that we have filtered out the **human-readable strings** we can filter out the '=' with the ``grep`` command.

```
bandit9@bandit:~$ strings data.txt | grep ====
4========== the#
========== password
========== is
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```

As we can see the password is the last line of the output, we can keep the last line by adding the command ``tail -n 1``. 

```
bandit9@bandit:~$ strings data.txt | grep ==== | tail -n 1
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```

Now we just need to get rid of the '=', for this we can do it with the command ``cut``.

```
bandit9@bandit:~$ strings data.txt | grep ==== | tail -n 1 | cut -d " " -f 2
G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```

**-d refers to the delimiter that separates both the '=' field and the password, in our case it is a single space. While -f indicates the field we want to keep, i.e. the second field which is the password.**

## Level 10 → Level 11

### Level Goal

The password for the next level is stored in the file **data.txt**, which contains **base64** encoded data.

### Solution

This level is pretty straight forward, we know that **data.txt** is base64 encoded.
To decode it we can use the ``base64`` command with the **-d** option which means **decode**.

```
bandit10@bandit:~$ base64 -d data.txt 
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
```

## Level 11 → Level 12

### Level Goal

The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

### Solution

This level is a bit tricky. We know that the letters have been rotated 13 positions i.e. the letter A is represented as the letter N and so on with each letter.

a b c d e f g h i j k l m n . . .\
<small>1 2 3 4 5 6 7 8 9 10 11 12 13</small>\
↑&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↑

To rotate the letters we can use the ``tr`` command, which is used to replace or delete characters. In our case we are going to translate them **13 positions**.

```
bandit11@bandit:~$ cat data.txt | tr [A-Za-z] [N-ZA-Mn-za-m]
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```

**[A-Za-z]** → We are going to include all the letters from a to z, whether they are upper or lower case.\
**[N-ZA-Mn-za-m]** → We replace them starting from the letter that is in the 13th position, which in this case is N until we return to the letter M and thus encompass all the letters.

## Level 12 → Level 13

### Level Goal

The password for the next level is stored in the file **data.txt**, which is a **hexdump** of a file that has been **repeatedly compressed**. For this level it may be useful to create a directory under ``/tmp`` in which you can work using ``mkdir``.

### Solution

Before doing anything, we are simply going to copy the content of the **data.txt** file and we are going to bring it to our Linux machine, to be able to manipulate it better.

Now, as we know that the **data.txt** file is a hexdump, so the first thing we should do is to convert it back to binary. To do this we can use the command ``xxd``, this command is useful both to convert files to hexadecimal and vice versa.

``cat data.txt | xxd -r``.

Now we should direct the output of this command to a file, for this we can use the command ``tee``, which is used to read the standard input and direct it to the file we want.

``cat data.txt | xxd -r | tee data``.

If we look at what type of file **data** is, we can see that it is a **gzip** file.

```
bandit12@bandit:/tmp/tmp.hGq2Gp5nI4$ file data
data: gzip compressed data, was "data2.bin", last modified: Sun Apr 23 18:04:23 2023, max compression, from Unix, original size modulo 2^32 581
```

We could extract it using the command ``7z x data``, but as we know that there are several files compressed one inside the other, we are going to make a small script to decompress all of them for us.

```
#!/bin/bash

first_file_name="data"
decompressed_file_name="$(7z l data | tail -n 3 | head -n 1 | awk '{print $NF}')"

7z x $first_file_name &> /dev/null

while [ $decompressed_file_name ]; do
  echo -e "\n[+] New file decompressed: $decompressed_file_name"
  7z x $decompressed_file_name &>/dev/null
  decompressed_file_name="$(7z l $decompressed_file_name 2>/dev/null | tail -n 3 | head -n 1 | awk 'NF{print $NF}')"
done
```

**We will save this script as, script.sh and give it execution permissions with the command ``chmod + x``.**

#### SCRIPT EXPLAINED
----
First we store in the variable **first_file_name** the name of the first file we are going to start decompressing, if you remember, when we previously converted the file from hexadecimal to binary, we named it **data** using the command ``tee``.

**decompressed_file_name** simply stores the name of the next uncompressed file inside **data**.

Here we can see the command working step by step:

```
7z l data

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,8 CPUs AMD Ryzen 7 1700 Eight-Core Processor           (800F11),ASM,AES-NI)

Scanning the drive for archives:
1 file, 614 bytes (1 KiB)

Listing archive: data

--
Path = data
Type = gzip
Headers Size = 20

   Date      Time    Attr         Size   Compressed  Name
------------------- ----- ------------ ------------  ------------------------
2023-04-23 20:04:23 .....          581          614  data2.bin
------------------- ----- ------------ ------------  ------------------------
2023-04-23 20:04:23                581          614  1 files
```

**This command provides us with the ability to see what file is inside *data*, so we can see that the following compressed file is called ***data2.bin*****

```
7z l data | tail -n 3
2023-04-23 20:04:23 .....          581          614  data2.bin
------------------- ----- ------------ ------------  ------------------------
2023-04-23 20:04:23                581          614  1 files
```

**Then with the ``tail`` command we can keep the last 3 lines of the output.**


```
7z l data | tail -n 3 | head -n 1
2023-04-23 20:04:23 .....          581          614  data2.bin
```

**Now, with the ``head`` command we keep the first line, which contains the name of the next compressed file.**

```
7z l data | tail -n 3 | head -n 1 | awk '{print $NF}'
data2.bin
```

**Lastly, with the ``awk`` command that we used before in Level 7, we keep the last field of the line, which is the name of the compressed file *data2.bin*.**

Now moving on to the rest of the script.

``7z x $first_file_name &> /dev/null`` → Unzip the **data** file and don't show any message in the output, so we send it to **/dev/null** using ``&>``.

The while loop part is simpler than it looks, it would read like this.

As long as the ``$decompressed_file_name`` variable has content, meaning that there is a compressed file inside another compressed file, we will print ``New file decompressed: $decompressed_file_name`` with the name of the new decompressed file. If the next decompressed file is not a ``.gzip. .tar...etc`` the while loop will stop since the command ``7z l`` that we used to get the name of the next file won't work, because is not a **compressed file**.

``7z x $decompressed_file_name &>/dev/null`` → decompresses the file we decompressed before starting the while loop, that is, the **data2.bin**.
And finally we replace the value of the variable **decompressed_file_name** with the value of the new decompressed file that we have just decompressed before inside the while loop.

Once we run the script the last unzipped file, in our case **data9.bin** will be the one that stores the password of the following level.

```
./script.sh

[+] New file decompressed: data2.bin

[+] New file decompressed: data2

[+] New file decompressed: data4.bin

[+] New file decompressed: data5.bin

[+] New file decompressed: data6.bin

[+] New file decompressed: data6

[+] New file decompressed: data8.bin

[+] New file decompressed: data9.bin
```

```
cat data9.bin
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```

## Level 13 → Level 14

### Level Goal

The password for the next level is stored in **/etc/bandit_pass/bandit14** and can only be read by user **bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level.

### Solution

At this level, we know that the password is located at **/etc/bandit_pass/bandit14**, but since only the user **bandit14** can access it as they are the owner, and we are **bandit13**, we won't be able to view it.

However, they provide us with an **SSH private key** to be able to access it as the user **bandit14**.

Since this private key belongs to the user **bandit14**, we can use it to log in as the user **bandit14** via SSH, without providing a password.
We can do this using the following command:

``ssh -i sshkey.private bandit14@localhost -p 2220``

**Remember to connect using port 2220**

Once inside as the user **bandit14**, we can now view the password for this user in the directory **/etc/bandit_pass/bandit14**.

```
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14 
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
```

## Level 14 → Level 15

### Level Goal

The password for the next level can be retrieved by submitting the password of the **current level** to **port 30000** on **localhost**.

### Solution

For this level, we know that if we send the password of the **current level** to **port 30000**, this port will provide us with the password for the next level.
To do this, we need to establish a connection to port 30000, which we can achieve using the ``nc`` (netcat) command. This command is used to create network connections and transfer data through different protocols.

```
bandit14@bandit:~$ nc localhost 30000
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq ← Current Level Password
Correct!
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
```

**We open a connection to port 30000 on the local machine and provide the password of the current level.**

## Level 15 → Level 16

### Level Goal

The password for the next level can be retrieved by submitting the password of the **current level** to **port 30001** on **localhost** using **SSL encryption**.

### Solution

In this level, the task is quite similar to the previous one, with a slight twist. Now, we need to apply the same approach but on **port 30001** and utilizing **SSL encryption** for secure communication.

However, a challenge arises: the traditional ``nc`` command can't be used here as it lacks the capability to establish encrypted connections with **SSL**. To tackle this, we turn to a command called ``ncat``, which stands as an upgraded and more secure counterpart to the ``nc`` command we employed in the previous level.

```
bandit15@bandit:~$ ncat --ssl localhost 30001
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
Correct!
JQttfApK4SeyHwDlI9SXGR50qclOAil1
```
## Level 16 → Level 17

### Level Goal

The credentials for the next level can be retrieved by submitting the password of the **current level** to a port on **localhost** in the **range 31000 to 32000**. First find out which of these ports have a server **listening** on them. Then find out which of those speak **SSL** and which **don't**. There is only **1 server** that will give the next credentials, the others will simply send back to you whatever you send to it.

### Solution

This level can be done in two ways, manually, by creating a script by hand that tries to connect to ports between 31000 and 32000. Or, we can use the ``nmap`` command, which allows us to scan port ranges.

Let's do it manually first, to understand how the process itself works.

#### SCRIPT EXPLAINED

```
#!/bin/bash

for port in $(seq 31000 32000); do
  (echo '' > /dev/tcp/127.0.0.1/$port) 2>/dev/null && echo "[+] $port - OPEN" &
done; wait
```


`for port in $(seq 31000 32000); do` → Starts a loop that loops through port numbers from 31000 to 32000 (inclusive).

`(echo '' > /dev/tcp/127.0.0.1/$port)` → Attempts to open a connection to the port specified in the loopback IP address (127.0.0.1) using the special `/dev/tcp` device. If the port is open and accepting connections, this will succeed and no error message will be generated.

`2>/dev/null` → Redirects error messages to `/dev/null`, which means that error messages will not be displayed in the output.

`&&` → Is a logical operator indicating that the following command will only be executed if the previous command succeeds.

`echo "[+] $port - OPEN"` → If the connection to the port is successful, this command prints a message indicating that the port is open.

`&` → Places the command in the background, allowing multiple commands to run simultaneously in parallel.

`wait` → Wait for all background processes to complete before terminating the script.

**Remember to give execution permissions to the script**

Once we run it we will be able to see which ports are open in that range.

```
bandit16@bandit:/tmp/tmp.2sAmNXpiZY$ ./script.sh 
[+] 31046 - OPEN
[+] 31518 - OPEN
[+] 31691 - OPEN
[+] 31790 - OPEN
[+] 31960 - OPEN
```

Now we only have to send the password of the current level each port until we find the port that returns the password of the next level, this can be done using the ``ncat`` command and the ``--ssl`` option.

```
bandit16@bandit:/tmp/tmp.2sAmNXpiZY$ ncat --ssl localhost 31790
JQttfApK4SeyHwDlI9SXGR50qclOAil1
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
<SNIP>
```

Port **31790** has provided us with an **SSH private key**, so let's create an **id_rsa** file and paste the private key into it. Remember to give write and read permissions only to the owner of the file. Only the owner should have these permissions for security reasons.

```
bandit16@bandit:/tmp/tmp.2sAmNXpiZY$ chmod 600 id_rsa 
bandit16@bandit:/tmp/tmp.2sAmNXpiZY$ ls -l
total 8
-rw------- 1 bandit16 bandit16 bandit16 1675 Aug 26 08:46 id_rsa
```
Now we can use this private key to connect to the user **bandit17**.

``ssh -i id_rsa bandit17@localhost -p 2220``

We can now see the **bandit17** password in **/etc/bandit_pass/bandit17**

```
bandit17@bandit:~$ cat /etc/bandit_pass/bandit17
VwOSWtCA7lRKkTfbr2IDh6awj9RNZM5e
```
----

Now we are going to do the same thing we did with the script but with the ``nmap`` command.
This command is quite simple:

```
bandit16@bandit:/tmp/tmp.2sAmNXpiZY$ nmap localhost -p31000-32000
Starting Nmap 7.80 ( https://nmap.org ) at 2023-08-26 08:50 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00016s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds
```

## Level 17 → Level 18

### Level Goal

There are **2 files** in the **home directory**: **passwords.old** and **passwords.new**. The password for the next level is in **passwords.new** and is the **only line** that has been **changed** between **passwords.old** and **passwords.new**

### Solution

At this level we have to compare the content of the passwords.new and passwords.old files. Since we know that one of the lines is not the same and this should be in the passwords.new file.

For this we are going to use the ``diff`` command which is used to show the differences between files.

```
bandit17@bandit:~$ diff passwords.new passwords.old
42c42 ← **This indicates that the difference is on line 42. The letter "c" in the middle stands for "change "**.
< hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
---
> glZreTEH1V3cGKL6g4conYqZqaEj0mte
```

``< hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg`` → This line is preceded by **<**, which means that this line is present only in the first file **passwords.new**

So the password is **hga5tuuCLF6fF6fFzUpnagiMN8ssu9LFrdg**

## Level 18 → Level 19

### Level Goal

The password for the next level is stored in a file **readme** in the **home directory**. Unfortunately, someone has modified **.bashrc** to log you out when you log in with **SSH**.

### Solution

If we try to connect to this level via SSH, we can see that we are expelled and we are not allowed to connect. This happens because when we connect by SSH it loads the .bashrc file which is the file that loads the bash configuration.
As we do not have access to bash because it expels us, we can inject a command through ssh to execute it before it loads the .bashrc file.

We are going to try to open a bash as soon as we connect by SSH.

``sshpass -p 'hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg' ssh bandit18@bandit.labs.overthewire.org -p 2220 bash``

Once we are in the bash, we can see the file **readme** in the **home directory**.

```
cat readme 
awhqfNnAbc1naukrpqDYcF95h7HoMTrC
```

## Level 19 → Level 20

### Level Goal

To gain access to the next level, you should use the **setuid binary** in the **home directory**. Execute it **without arguments** to find out how to use it. The password for this level can be found in the usual place **/etc/bandit_pass**, after you have used the setuid binary.

### Solution

First of all it tells us that we have to use the setuid binary that we have in the home directory. The **setuid** is a special permission that allows a program to be executed with the same privileges as the owner of the file.

If we see what are the permissions of the setuid binary

```
bandit19@bandit:~$ ls -l
total 16
-rwsr-x--- 1 bandit20 bandit19 bandit19 14876 Apr 23 18:04 bandit20-do
```

**We can see that the owner **bandit20** has read, write and active setuid permissions.

If we could run a bash using this binary we could see the password found in **/etc/bandit_pass/bandit20**.

If we try to view it as the user **bandit19**, we will see that we do not have sufficient permissions.

```
bandit19@bandit:~$ cat /etc/bandit_pass/bandit20
cat: /etc/bandit_pass/bandit20: Permission denied
```

Let's run the binary without arguments, to see what it asks for

```
bandit19@bandit:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do id
```

**The command simply runs the command we want as another user, in this case *bandit20***

So if we try to view the **/etc/bandit_pass/bandit20** file again using the binary, we will be able to see the password of **bandit20**.

```
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
VxCazJaVykI6W36BkBU0mJTCM8rR95XT
```

## Level 20 → Level 21

### Level Goal

There is a **setuid binary** in the **home directory** that does the following: it makes a connection to **localhost** on the **port** you specify as a commandline argument. It then reads a line of text from the connection and compares it to the **password** in the previous level (**bandit20**). If the password is correct, it will transmit the password for the next level (**bandit21**).

### Solution

For this level we have to provide the password of the current level when we establish a connection with a random port, so that it returns the password of the next level.

We will have to have two SSH sessions from **bandit20**, in one we will open the port we want and in the other we will connect to that port and we will provide the password.
This can be done with the command ``nc``.

To open the port we must use several options of the ``nc`` command

``nc -nltp 4444``

-n → Means do not apply DNS resolution, so it will use IP addresses instead of domain names.

-l → Means that the port will be listening for a connection.

-t → Means it will use TCP protocol.

-p 4444 → Specifies the port number to open.

Once it is open, we can go to the other SSH session and use the setuid binary again to connect to the port we just opened (**4444**) 

Now we go back to the session where we opened the port and provide the current level password.

```
bandit20@bandit:~$ nc -nltp 4444
VxCazJaVykI6W36BkBU0mJTCM8rR95XT
NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
```

**As we can see, it returns the password for the next level**.

## Level 21 → Level 22

### Level Goal

A program is running automatically at regular intervals from **cron**, the **time-based job scheduler**. Look in **/etc/cron.d/** for the **configuration** and see what **command** is being executed.

### Solution

At this level, a program is running at regular intervals. To identify which program is executing, we can go to the directory **/etc/cron.d/** and search for the file **bandit22**.

If we view the file, we will see the following:

```
bandit21@bandit:~$ cat /etc/cron.d/cronjob_bandit22 
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

**As we can see, it's executing a script every minute located at /usr/bin/cronjob_bandit22.sh**

Let's view the content of the script to understand its function:

```
bandit21@bandit:~$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

**We can see that it's granting read permissions to groups and other users, including us *bandit21*. We can also see that it's redirecting the content of /etc/bandit_pass/bandit22 to the temporary file. From this, we can deduce that this temporal file includes the password for *bandit22*.**

Therefore, we could view that temporary file to obtain the password for the next level:

```
bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
```

## Level 22 → Level 23

### Level Goal

A program is running automatically at regular intervals from **cron**, the **time-based job scheduler**. Look in **/etc/cron.d/** for the **configuration** and see what **command** is being executed.

### Solution

This level is very similar to the previous one. Let's see which program is being executed by cron from its configuration file, which in this case would be that of **bandit23**.

```
bandit22@bandit:~$ cat /etc/cron.d/cronjob_bandit23 
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```

Now that we know the program's path, let's also view this one.

```
bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

#### SCRIPT EXPLAINED

This script creates a temporary file in the **/tmp** directory that contains the password of the user **bandit23**.

The variable `$myname` will always contain **bandit23**, as this is the user with execute permissions on the script. Thus, they are the only one who can run `whoami` within the script.

```
bandit22@bandit:~$ ls -l /usr/bin/cronjob_bandit23.sh
-rwxr-x--- 1 bandit23 bandit22 211 Apr 23 18:04 /usr/bin/cronjob_bandit23.sh
```

The name of the temporary file containing the password is the MD5 hash value of the string "I am user bandit23" without the trailing dash at the end. That's why the `cut -d` command is used to keep only the first field, which is the hash value.

When we execute this command by replacing `$myname` with **bandit23**, we see this output:

```
bandit22@bandit:~$ echo I am user bandit23 | md5sum  | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
```

``cat /etc/bandit_pass/$myname > /tmp/$mytarget`` → It simply copies the password value from **/etc/bandit_pass/bandit23** to **/tmp/8ca319486bfbbc3663ea0fbe81326349** (The name of this temporal file is the hash that we saw before).

If we perform `cat` on that temporary file, we can see the password for the next level:

```
bandit22@bandit:~$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G
```

## Level 23 → Level 24

### Level Goal

A program is running automatically at regular intervals from **cron**, the **time-based job scheduler**. Look in **/etc/cron.d/** for the **configuration** and see what **command** is being executed.

**NOTE** → This level requires you to create your own first shell-script.

**NOTE 2** → Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

### Solution

We're doing the same thing as in the previous level, let's visualize the **cron** configuration of the file **bandit24**.

```
bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

Now that we know where the script is located, let's view it.

```
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo || exit 1
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -rf ./$i
    fi
done
```

This Bash script aims to execute and delete scripts in the directory `/var/spool` of the current user (obtained using `whoami`). The `/var/spool` directory is a directory in Unix systems where files are temporarily stored for processing by various services or systems.

Remember that this script is being executed as **bandit24** which means that everything that this scripts executed has the permissions of **bandit24**

Here's the step-by-step breakdown of the script:

`myname=$(whoami)` → Assigns the current username to `myname` variable using the `whoami` command.

`cd /var/spool/$myname/foo || exit 1` → Changes to the directory `/var/spool/$myname/foo`. If the directory change fails (for example, if the directory doesn't exist), the script exits with an exit code of 1 using `exit 1`.

`echo "Executing and deleting all scripts in /var/spool/$myname/foo:"` → Displays a message indicating that all scripts in the directory are being executed and deleted.
The `for i in * .*;` loop iterates over all files and directories (including hidden ones) in the current directory (`/var/spool/$myname/foo`).

`if [ "$i" != "." -a "$i" != ".." ];` → Checks if the file is not the current directory (`.`) or the parent directory (`..`). This prevents the script from handling special directories.

`echo "Handling $i"` → Displays a message indicating that the current file or directory is being handled.

`owner="$(stat --format "%U" ./$i)"` → Uses the `stat` command to get the owner of the current file and assigns it to the `owner` variable.

`if [ "${owner}" = "bandit23" ]; then` → Checks if the owner of the file is "bandit23".

`timeout -s 9 60 ./$i` → Uses the `timeout` command to execute the current file with a time limit of 60 seconds and signal 9 (SIGKILL) handling if the limit is exceeded.

`rm -rf ./$i` → Deletes the current file or directory after it's been handled.

In summary, this script iterates through files in the directory `/var/spool/bandit24/foo`, checks if the owner is **bandit23**, and if so, executes the file within a time limit before removing it. This approach is used to manage and execute temporary scripts stored in the `/var/spool` directory of the user **bandit24**.

Therefore, we could create a script that will run **cron** as the user **bandit24** and thereby be able to view the password for **bandit24** in the directory **/etc/bandit_pass/bandit24**.

```
bandit23@bandit:/var/spool/bandit24/foo$ cat /tmp/script.sh
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/passwd.txt
```

**We create the script in /tmp and then copy it to the directory where the script we saw earlier runs the scripts, which is */var/spool/bandit24/foo***

Once the script is executed, it will create a file in `/tmp/passwd.txt` that contains the password for the next level.

```
bandit23@bandit:/var/spool/bandit24/foo$ cat /tmp/passwd.txt
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar
```

## Level 24 → Level 25

### Level Goal

A **daemon** is listening on **port 30002** and will give you the password for **bandit25** if given the password for **bandit24** and a secret numeric **4-digit pincode**. There is no way to retrieve the pincode except by going through all of the **10000 combinations**, called **brute-forcing**.

### Solution

In this level, we need to provide the password for the current level and a secret numeric **4-digit pincode** ranging from **0 to 9999**. If we attempt to connect to port **30002** using the `nc` command as we did in previous levels, we will see the following:

```
bandit24@bandit:~$ nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
```

It's asking us for the password of this level and the pin separated by a space.

Since we don't know the pin and only know the range it falls within, we can use a for loop to facilitate the pin search.

```
bandit24@bandit:~$ for ping in {0000..9999}; do echo $ping; done
0000
0001
0002
0003
0004
<SNIP>
```

Now that we have all possible combinations, let's add the current level's password to the output as well and redirect it to a file in **/tmp**.

But first, let's create the temporary directory:

```
bandit24@bandit:~$ mktemp -d
/tmp/tmp.DThJ6DTaDD
```

And inside this directory, we'll redirect to a file:

```
bandit24@bandit:/tmp/tmp.DThJ6DTaDD$ for ping in {0000..9999}; do echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $ping"; done > combinations.txt
```

If we `cat` this file, we'll see the following:

```
bandit24@bandit:/tmp/tmp.DThJ6DTaDD$ cat combinations.txt
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 0000
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 0001
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 0002
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 0003
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 0004
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 0005
<SNIP>
```

Now we'll split it into several files with 2000 lines each, to avoid overloading the port while bruteforcing. For this, we'll use the `split` command:

``bandit24@bandit:/tmp/tmp.DThJ6DTaDD$ split -l 2000 combinations.txt combinations_part_``

Now we can `cat` each of these files we just created and pass them to the `nc` command we used earlier through a pipeline:

```
bandit24@bandit:/tmp/tmp.DThJ6DTaDD$ cat combinations_part_ae | nc localhost 30002 | grep -vE "Wrong|Please enter"
Correct!
The password of user bandit25 is p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d

Exiting.
```

**In my case, the last file that contained the last 2000 combinations (8000-9999) was the one containing the correct pin.**

## Level 25 → Level 26

### Level Goal

Logging in to **bandit26** from **bandit25** should be fairly easy… The shell for user **bandit26** is not **/bin/bash**, but something else. Find out what it is, how it works and how to break out of it.

### Solution

We know that the user **bandit26** shell is not **/bin/bash**. We can verify this by checking the **/etc/passwd** file, which contains information about users, groups and their respective shells.

```
bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

We can see that the shell for user **bandit26** is located at **/usr/bin/showtext**. If we try to view the content of this file using `cat`, we will see the following:

```
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```

We have an **SSH key** for user **bandit26** in the **home directory** of user **bandit25**:

```
bandit25@bandit:~$ ls
bandit26.sshkey
```

We can use this key to connect to **bandit26**, but this won't work as it will close the connection. This is because the user is not using a regular shell; instead, they are executing ``more ~/text.txt`` command on a file in the **home directory** of user **bandit26**.

To escape from the ``more`` command, we can use a function of this command that allows us to enter **interactive mode**. This will let us open a shell. To do this, we need to shrink the terminal window to make ``more`` enter command mode.

Once in command mode, press the **v** key to enter **vim**. Now that we are inside **vim** as user **bandit26**, we will change the shell to **/bin/bash**. To do this, execute the following command:

``:set shell=/bin/bash``

Once set, execute ``:shell``, and this should give us a functional bash shell as user **bandit26**.

Now we can view the password for the next level:

```
bandit26@bandit:~$ cat /etc/bandit_pass/bandit26
c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1
```

## Level 26 → Level 27

### Level Goal

Good job getting a shell! Now hurry and grab the password for **bandit27**

### Solution

Now that we are in the user **bandit26**, if we check which files we have in our **home directory**, we will see that we have a setuid binary file, from which we can benefit to execute commands as the user **bandit27**.

```
bandit26@bandit:~$ ls -l bandit27-do 
-rwsr-x--- 1 bandit27 bandit26 14876 Apr 23 18:04 bandit27-do
```

So, we will view the password of **bandit27** like this:

```
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS
```

## Level 27 → Level 28

### Level Goal

There is a git repository at **ssh://bandit27-git@localhost/home/bandit27-git/repo** via the **port 2220**. The password for the user **bandit27-git** is the same as for the user **bandit27**.

### Solution

This level is quite simple, we just have to clone the git repository ``ssh://bandit27-git@localhost/home/bandit27-git/repo`` and once cloned, search for the password in it.

But before cloning, let's create a temporary directory to clone the repository from there:

```
bandit27@bandit:~$ mktemp -d
/tmp/tmp.8bBogeQq8U
```

Now we can proceed with the cloning:

```
bandit27@bandit:/tmp/tmp.8bBogeQq8U$ git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo         
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
<SNIP>
```

**Remember to use port 2220 when cloning the repository.**

Let's enter the ``/repo`` repository and view the **README** file which contains the password for the next level:

```
bandit27@bandit:/tmp/tmp.8bBogeQq8U/repo$ cat README 
The password to the next level is: AVanL161y9rsbcJIsFHuw35rjaOM19nR
```

## Level 28 → Level 29

### Level Goal

There is a git repository at **ssh://bandit28-git@localhost/home/bandit28-git/repo** via the **port 2220**. The password for the user **bandit28-git** is the same as for the user **bandit28**.

### Solution

Let's create a temporary directory again to work from there:

```
bandit28@bandit:~$ mktemp -d
/tmp/tmp.MQqDCik6Ys
```

And now let's download the repository for **bandit28**:

```
bandit28@bandit:/tmp/tmp.MQqDCik6Ys$ git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
<SNIP>
```

If we read the **README** file inside the downloaded repository, we will see that the password is hidden:

```
bandit28@bandit:/tmp/tmp.MQqDCik6Ys/repo$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

We can check if this repository has had any commits that might have modified the password field in this file. To do this, we can use the command ``git log``:

```
bandit28@bandit:/tmp/tmp.MQqDCik6Ys/repo$ git log
commit 899ba88df296331cc01f30d022c006775d467f28 (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Apr 23 18:04:39 2023 +0000

    fix info leak ← Here it indicates that something related to an information leak has been modified, giving us a hint that it might be the password.

commit abcff758fa6343a0d002a1c0add1ad8c71b88534
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Apr 23 18:04:39 2023 +0000

    add missing data

commit c0a8c3cf093fba65f4ee0e1fe2a530b799508c78
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Apr 23 18:04:39 2023 +0000

    initial commit of README.md
```

We can see the commit related to the information leak using the ``git show`` command followed by the commit identifier:

```
bandit28@bandit:/tmp/tmp.MQqDCik6Ys/repo$ git show 899ba88df296331cc01f30d022c006775d467f28
commit 899ba88df296331cc01f30d022c006775d467f28 (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Apr 23 18:04:39 2023 +0000

    fix info leak

diff --git a/README.md b/README.md
index b302105..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S
+- password: xxxxxxxxxx
```

**We can see the password in plain text before it was hidden.**

## Level 29 → Level 30

### Level Goal

There is a git repository at **ssh://bandit29-git@localhost/home/bandit29-git/repo** via the **port 2220**. The password for the user **bandit29-git** is the same as for the user **bandit29**.

### Solution

We clone the repository again into a temporary directory:

```
bandit29@bandit:/tmp/tmp.f2ocPWUjw0$ git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
<SNIP>
```

If we try to view the **README** file of the downloaded repository, we can see the following:

```
bandit29@bandit:/tmp/tmp.f2ocPWUjw0/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

The `<no passwords in production!>` message gives us a hint that passwords are not allowed to be stored in this branch of the repository.

Therefore, we can proceed to check the available branches in the repository using the command ``git branch -a``:

```
bandit29@bandit:/tmp/tmp.f2ocPWUjw0/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```

We can try the 'dev' branch to see if we can find the password there. To do this, we use the command ``git checkout dev``:

```
bandit29@bandit:/tmp/tmp.f2ocPWUjw0/repo$ git checkout dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
Switched to a new branch 'dev'
```

Now, if we attempt to view the **README** file again, we will be able to see the password:

```
bandit29@bandit:/tmp/tmp.f2ocPWUjw0/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS
```

## Level 30 → Level 31

### Level Goal

There is a git repository at **ssh://bandit30-git@localhost/home/bandit30-git/repo** via the **port 2220**. The password for the user **bandit30-git** is the same as for the user **bandit30**.

### Solution

Once the repository is downloaded, we see that the README file doesn't contain anything useful:

```
bandit30@bandit:/tmp/tmp.hPfkiw6EoY/repo$ cat README.md 
just an empty file... muahaha
```

If we try to view the commits in the repository, we won't see much:

```
bandit30@bandit:/tmp/tmp.hPfkiw6EoY/repo$ git log
commit 59530d30d299ff2e3e9719c096ebf46a65cc1424 (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Apr 23 18:04:42 2023 +0000

    initial commit of README.md
```

And the same goes for listing the branches:

```
bandit30@bandit:/tmp/tmp.hPfkiw6EoY/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
```

Therefore, the only option left is to list the tags. Tags are specific references in the history of a Git repository that point to specific points in time.

To view the tags, we can use the ``git tag`` command:

```
bandit30@bandit:/tmp/tmp.hPfkiw6EoY/repo$ git tag
secret
```

If we check the tag called **secret** we will see that it contains the password for the next level:

```
bandit30@bandit:/tmp/tmp.hPfkiw6EoY/repo$ git show secret 
OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt
```
## Level 31 → Level 32

### Level Goal

There is a git repository at **ssh://bandit31-git@localhost/home/bandit31-git/repo** via the **port 2220**. The password for the user **bandit31-git** is the same as for the user **bandit31**.

### Solution

In this level, if we read the **README** file, we can see that it asks us to push a file to the remote repository:

```
bandit31@bandit:/tmp/tmp.KNIFmrreT7/repo$ cat README.md 
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

First, let's create the **key.txt** file with the content '**May I come in?**'.

Once created, we'll add it to the repository using the command ``git add -f key.txt``.

Next, we need to commit it with a description of the change we're making in the repository:

```
bandit31@bandit:/tmp/tmp.KNIFmrreT7/repo$ git commit -m "Create a new file"
[master a1dd92e] Create a new file
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt
```

Now, we have to push it to the **master** branch using the following command:

```
bandit31@bandit:/tmp/tmp.KNIFmrreT7/repo$ git push -u origin master
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit31/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password: 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 326 bytes | 326.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: ### Attempting to validate files... ####
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
remote: Well done! Here is the password for the next level: 
remote: rmCBvG56y58BXzv98yZGdO7ATVL5dW8y
```

**Once pushed, we will see the password in the output.**

## Level 32 → Level 33

### Level Goal

After all this git stuff its time for another escape. Good luck!

### Solution

Once we connect via **SSH** to this level, we notice that it welcomes us with a **different shell**. Regardless of the command we type, it returns the name of the command in uppercase:

```
WELCOME TO THE UPPERCASE SHELL
>> ls
sh: 1: LS: Permission denied
>> test
sh: 1: TEST: Permission denied
```

We know it's not a bash shell because when we view the `$SHELL` variable, it returns the following:

```
>> $SHELL
WELCOME TO THE UPPERCASE SHELL
```

In Linux, there are several variables that refer to different functionalities of the shell. One variable that can be useful in this situation is the `$0` variable, which refers to the default shell.

If we execute this variable, we can revert back to a **bash** shell:

```
>> $0
$ whoami
bandit33
```

Now we can view the password for the next level:

```
$ cat /etc/bandit_pass/bandit33 
odHo63fHiFqcWWJG9rLiLDtPm45KzUKy
```

## Level 33 → Level 34

### Level Goal

At this moment, level 34 does not exist yet.

### Solution

All you can do at this level is to congratulate yourself and view the **README** file in the **home directory**.

```
bandit33@bandit:~$ cat README.txt 
Congratulations on solving the last level of this game!

At this moment, there are no more levels to play in this game. However, we are constantly working
on new levels and will most likely expand this game with more levels soon.
Keep an eye out for an announcement on our usual communication channels!
In the meantime, you could play some of our other wargames.

If you have an idea for an awesome new level, please let us know!
```