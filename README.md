Working on the Command Line
================

A little ditty on using the command line, the most powerful tool in your developer toolbelt.

# Installation

### On Cloud9

Create a new Cloud9 workspace:

1. From your Cloud9 Dashboard, find in the upper left corner and click the green button, "Create New Workspace".
Select "Clone From URL".
2. In the "Source URL" form input, copy and paste in the following URL:

        https://github.com/OperationSpark/logging.git

3. In the environment selection box, select "Custom".
4. Finally, click the green button "Create".

Nice, you're in business...

---

# Lesson Steps

Because you'll be doing this so often, the first thing we're gonna do is look around and navigate a bit on the filesystem:

Look at the bottom of the screen, you'll see the bash terminal open in the Console View:

<img src="https://raw.githubusercontent.com/OperationSpark/javascript-wiki/master/images/c9-console.png" alt="The Console View">

If you're having trouble opening or finding the terminal on Cloud9, <a href="https://github.com/OperationSpark/javascript-wiki/wiki/The-Command-Line#user-content-opening-a-terminal-on-cloud9" target="_blank">follow these instructions here</a>


**TODO 1 : Looking Around with _Present Working Directory_ and _List Services_**

###pwd

Whenever you're using a terminal, you are doing so from within a directory on the filesystem.  You can always ask which directory you're in by running the command, `pwd`, which stands for present working directory.  Type, `pwd`, the press `return`:

````
myuser@the-command-line:~/workspace (master) $ pwd
/home/ubuntu/workspace
````

Awesome, the `pwd` command returns the path to our location where we're currently running the terminal.

###ls (List Services)

You'll often want to know what files are in this directory with you.  The _List Services_ command helps you see what files you have in your _present working directory_.  Type `ls` and hit `return`:

````
myuser@the-command-line:~/workspace (master) $ ls
README.md  files/
````

Cool, we can see that within our present working directory, we have the files `README.md` and a directory called `files`.

We know that the `README.md` is a file of the type `.md` (which stands for markdown, a simple formatting language), and we know that `files/` is a directory because the `ls` command formats its name with a trailing slash, the `/` character.  You can think of this `/` character as representing a directory divider.

Let's take advantage of some of the flags of the `ls` command to learn more about our files.  Try adding the `-a` flag to see any hidden files in our present working directory:

````
myuser@the-command-line:~/workspace (master) $ ls -a
./  ../  .c9/  .git/  .gitignore  README.md  files/
````

Whoa, quite a few!  We have `./`, which actually means the present working directory, next we have `../`, which represents the parent directory, finally `.c9`, a hidden directory of files for our Cloud9 workspace, `.git/` is another hidden directory used by our version control system, git, next is `.gitignore`, another file used by git, than our two remaining files we've already seen.  Wow!  That's a lot of extra info!

Alright, let's use one more flag on the `ls` command, the `-l` flag, which stand for _long form_:

````
myuser@the-command-line:~/workspace (master) $ ls -l
-rw-rw-r-- 1 ubuntu ubuntu 3298 Dec 10 03:35 README.md
drwxr-xr-x 4 ubuntu ubuntu 4096 Dec  9 23:49 files/
````

Okay!  For the breakdown of the information returned by `ls -l`, here a blurb from the `info` page for `ls`:

> In addition to the name of each file, print the file type,
     permissions, number of hard links, owner name, group name, size in bytes, and timestamp (by default, the modification time).  For files with a time more than six months old or in the future, the timestamp contains the year instead of the time of day.  If the timestamp contains today's date with the year rather than a time of day, the file's time is in the future, which means you probably have clock skew problems which may break programs like `make' that rely on file times.

One more trick: some commands will let us apply multiple flags at once. Let's see how `ls` will handle both `a` and `l` flags together:

````
myuser@the-command-line:~/workspace (master) $ ls -al
total 28
drwxrwxr-x  5 ubuntu ubuntu 4096 Dec  9 23:34 ./
drwxr-xr-x 23 ubuntu ubuntu 4096 Dec  9 23:22 ../
drwxr-xr-x  3 ubuntu ubuntu 4096 Dec  9 23:22 .c9/
drwxrwxr-x  8 ubuntu ubuntu 4096 Dec  9 23:22 .git/
-rw-rw-r--  1 ubuntu ubuntu  592 Dec  9 23:24 .gitignore
-rw-rw-r--  1 ubuntu ubuntu 3298 Dec 10 03:35 README.md
drwxr-xr-x  4 ubuntu ubuntu 4096 Dec  9 23:49 files/
````

You get the point- we've requested to also show all hidden files as well as the long form details of each file in our present working directory!

**TODO 2 Navigating the Filesystem**

###cd (Change Directories)

Probably the thing you'll do most often on the commannd line is navigate.  To change directories, you use the `cd` command, which stands for _change directory_

From our `workspace`, let's change directories into our `files` directory.

````
myuser@the-command-line:~/workspace (master) $ cd files
myuser@the-command-line:~/workspace/files (master) $
````

Excellent!  We've moved into the `files` directory, and the prompt now tells us our new location with the path in blue, `~/workspace/files`.

We can now use `ls` to look around this new loation:

````
myuser@the-command-line:~/workspace/files (master) $ ls
letters/  names/
````

Looky there, we have two directories in here!  Let's step inside the `letters` directory:

````
myuser@the-command-line:~/workspace/files (master) $ cd letters
myuser@the-command-line:~/workspace/files/letters (master) $
````

Fine, we're now inside the `letters`.  What's your next move?  Look around, of course:

````
myuser@the-command-line:~/workspace/files/letters (master) $ ls
dad/  mom/
````

Ok, two other directories, and now, instead of moving inside either of those two directories, let's peer into them from the outside.  The `ls` command can take a path to a directory on which you want to list services:

````
myuser@the-command-line:~/workspace/files/letters (master) $ ls mom/
mom-one.txt  mom-two.txt
````

Nice, we just looked inside the `mom` directory from our present working directory, and not from inside of the `mom` directory, and in there we see we've written 2 letters to mom!  Aren't we great?

Ok, now how do we move back up the filesystem?  Easy, we use `cd ..` to go back up on directory:

````
myuser@the-command-line:~/workspace/files/letters (master) $ cd ..
myuser@the-command-line:~/workspace/files
````

Sweet, we went back upstairs one level:

````
myuser@the-command-line:~/workspace/files (master) $ cd ../../
myuser@the-command-line:~
````

Whoa, see what we did there?  We used navigated backwards 2 directories by typing `../`, twice.  Alright though, we've gone too far, so let's go back to our workspace directory, BUT, before we do, let's learn about _auto-completion_:

###Auto Completion

Typing long file names can be a drag and slow us down, so bash offers us auto completion.  When addressing files or directories, we can begin to type the name of the file, and press the `tab` key, and if we've typed enough of the name that there's no other conflict in selecting the rest of the name uniquely, bash will auto select the name of the file for us.  This will save you hours of productivity!

Try typing `cd wo`, then press `tab`, and bash should fill-in the directory name, `workspace`.  Press enter to change into the `workspace` directory:

````
myuser@the-command-line:~ (master) $ cd workspace
myuser@the-command-line:~/workspace (master) $
````

If there's a conflict, and you hit tab, the first time you press tab, nothing will happen, the second time, you may here a beep, then bash will display the choices, but narrowed to your search criteria.

Cool, let's peer inside some files.  First, jump into the directory at `~/workspace/files/letters/dad`.  Use the `cd` command with auto complete to get you there faster:

````
myuser@the-command-line:~/workspace (master) $ cd files/letters/dad/
myuser@the-command-line:~/workspace/files/letters/dad (master) $ 
````

###cat (catenate)

We can use the `cat` command (short for catenate, a synonym of concatenate) to output contents of a file to the terminal, and can be used to concatenate and list files.

Let's see what we wrote to dad in our first letter to him.  First, though, let's try our auto complete: start typing `cat dad-`, then press `tab`, twice:

````
myuser@the-command-line:~/workspace/files/letters/dad (master) $ cat dad-
dad-one.txt  dad-two.txt
jfraboni@the-command-line:~/workspace/files/letters/dad (master) $ cat dad-
````

...bash will present you with the remaining possible choices, and return you to where you were in the typing sequence!  Neat!

````
myuser@the-command-line:~/workspace/files/letters/dad (master) $ cat dad-one.txt
Dad,

One Lorem ipsum dolor sit amet, vivendo intellegam ne duo. Ubique aliquam vulputate et pro. No sea mentitum signiferumque, ei has eleifend tincidunt. Ei enim nostrum inimicus sed, quod sensibus no ius, dico viderer scriptorem duo ne. Ut sale sadipscing mei, quaeque principes ad vix. Causae maiestatis vim id, cu nec omittantur vituperatoribus.

Etc...
````

Cool, we just printed the contents of our letter to the screen!  `cat` can do some neat things, though not always as intended - check this out, we'll use the `pipe` and `redirect` features with another command `sed` (stream editor), to create a form letter:

````
myuser@the-command-line:~/workspace/files/letters/dad (master) $ cat dad-two.txt | sed s/Dad/Mom/ | sed s/Two/Three/ > ../mom/mom-three.txt
````

Running this rather long set of commands will create a file called `mom-three.txt` in the `mom` directory, and you'll notice that the word `Dad` has been replaced with `Mom`, and the letter `Two` replaced with the letter `Three`!

Are you seeing some possiblities here?


We can use `cat` to actually concatenate files, which was its original purpose:

````
myuser@the-command-line:~/workspace/files/letters/dad (master) $ cd ~/workspace/files/names/
myuser@the-command-line:~/workspace/files/names (master) $ cat 2015-boys.txt 2015-girls.txt > 2015.txt
````

Cool!!! A new file was created, concatenating all the girls and boys from 2015 into one file called `2015.txt`!