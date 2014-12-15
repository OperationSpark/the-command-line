Working on the Command Line
================

A little ditty on using the command line, the most powerful tool in your developer toolbelt.

# Installation

### On Cloud9

Create a new Cloud9 workspace:

1. From your Cloud9 Dashboard, find in the upper left corner and click the green button, "Create New Workspace".
Select "Clone From URL".
2. In the "Source URL" form input, copy and paste in the following URL:

        https://github.com/OperationSpark/the-command-line.git

3. In the environment selection box, select "Custom".
4. Finally, click the green button "Create".

Nice, you're in business...

---

# Lesson Steps

Because you'll be doing this so often, the first thing we're gonna do is look around and navigate a bit on the filesystem:

Look at the bottom of the screen, you'll see the bash terminal open in the Console View:

<img src="https://raw.githubusercontent.com/OperationSpark/javascript-wiki/master/images/c9-console.png" alt="The Console View">

If you're having trouble opening or finding the terminal on Cloud9, <a href="https://github.com/OperationSpark/javascript-wiki/wiki/The-Command-Line#user-content-opening-a-terminal-on-cloud9" target="_blank">follow these instructions here</a>

Firstly, select the Console View to give the bash terminal the focus, you'll know it has the focus becasue the cursor at the end of the prompt will turn black.

##Looking Around with _Present Working Directory_ and _List Services_

###pwd Present Working Directory

Whenever you're using a terminal, you are doing so from within a directory on the filesystem.  You can always ask which directory you're in by running the command, `pwd`, which stands for present working directory.  Type, `pwd`, the press `return`:

####TODO 1 :
````
myuser@the-command-line:~/workspace (master) $ pwd
/home/ubuntu/workspace
````

Awesome, the `pwd` command returns the path to our location where we're currently running the terminal.

###ls List Services

You'll often want to know what files are in this directory with you.  The _List Services_ command helps you see what files you have in your _present working directory_.  Type `ls` and hit `return`:

####TODO 2 :
````
myuser@the-command-line:~/workspace (master) $ ls
README.md  files/
````

Cool, we can see that within our present working directory, we have the files `README.md` and a directory called `files`.

We know that the `README.md` is a file of the type `.md` (which stands for markdown, a simple formatting language), and we know that `files/` is a directory because the `ls` command formats its name with a trailing slash, the `/` character.  You can think of this `/` character as representing a directory divider.

Let's take advantage of some of the flags of the `ls` command to learn more about our files.  Try adding the `-a` flag to see any hidden files in our present working directory:

####TODO 3 :

````
myuser@the-command-line:~/workspace (master) $ ls -a
./  ../  .c9/  .git/  .gitignore  README.md  files/
````

Whoa, quite a few!  We have `./`, which actually means the present working directory, next we have `../`, which represents the parent directory, finally `.c9`, a hidden directory of files for our Cloud9 workspace, `.git/` is another hidden directory used by our version control system, git, next is `.gitignore`, another file used by git, than our two remaining files we've already seen.  Wow!  That's a lot of extra info!

Alright, let's use one more flag on the `ls` command, the `-l` flag, which stand for _long form_:

####TODO 4 :
````
myuser@the-command-line:~/workspace (master) $ ls -l
-rw-rw-r-- 1 ubuntu ubuntu 3298 Dec 10 03:35 README.md
drwxr-xr-x 4 ubuntu ubuntu 4096 Dec  9 23:49 files/
````

Okay!  For the breakdown of the information returned by `ls -l`, here a blurb from the `info` page for `ls`:

> In addition to the name of each file, print the file type,
     permissions, number of hard links, owner name, group name, size in bytes, and timestamp (by default, the modification time).  For files with a time more than six months old or in the future, the timestamp contains the year instead of the time of day.  If the timestamp contains today's date with the year rather than a time of day, the file's time is in the future, which means you probably have clock skew problems which may break programs like `make' that rely on file times.

One more trick: some commands will let us apply multiple flags at once. Let's see how `ls` will handle both `a` and `l` flags together:

####TODO 5 :
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

##Navigating the Filesystem

###cd Change Directories

Probably the thing you'll do most often on the commannd line is navigate.  To change directories, you use the `cd` command, which stands for _change directory_

From our `workspace`, let's change directories into our `files` directory:

####TODO 6 :

````
myuser@the-command-line:~/workspace (master) $ cd files
myuser@the-command-line:~/workspace/files (master) $
````

Excellent!  We've moved into the `files` directory, and the prompt now tells us our new location with the path in blue, `~/workspace/files`.

We can now use `ls` to look around this new loation:

####TODO 7 :
````
myuser@the-command-line:~/workspace/files (master) $ ls
letters/  names/
````

Looky there, we have two directories in here!  Let's step inside the `letters` directory:

####TODO 8 :

````
myuser@the-command-line:~/workspace/files (master) $ cd letters
myuser@the-command-line:~/workspace/files/letters (master) $
````

Fine, we're now inside the `letters`.  What's your next move?  Look around, of course:

####TODO 9 :
````
myuser@the-command-line:~/workspace/files/letters (master) $ ls
dad/  mom/
````

Ok, two other directories, and now, instead of moving inside either of those two directories, let's peer into them from the outside.  The `ls` command can take a path to a directory on which you want to list services:

####TODO 10 :
````
myuser@the-command-line:~/workspace/files/letters (master) $ ls mom/
mom-one.txt  mom-two.txt
````

Nice, we just looked inside the `mom` directory from our present working directory, and not from inside of the `mom` directory itself.  And in there we see we've written 2 letters to mom!  Aren't we great?

Ok, now how do we move back up the filesystem?  Easy, we use `cd ..` to go back up on directory:

####TODO 11 :
````
myuser@the-command-line:~/workspace/files/letters (master) $ cd ..
myuser@the-command-line:~/workspace/files
````

Sweet, we went back upstairs one level:

####TODO 12 :

````
myuser@the-command-line:~/workspace/files (master) $ cd ../../
myuser@the-command-line:~
````

Whoa, see what we did there?  We navigated backwards 2 directories by typing `../`, twice.  Alright though, we've gone too far, so let's go back to our workspace directory, BUT, before we do, let's learn about _auto-completion_:

###Auto Completion

Typing long file names can be a drag and slow us down, so bash offers us auto completion.  When addressing files or directories, we can begin to type the name of the file, and press the `tab` key, and if we've typed enough of the name that there's no other conflict in selecting the rest of the name uniquely, bash will auto select the name of the file for us.  This will save you hours of productivity!

Try typing `cd wo`, then press `tab`, and bash should fill-in the directory name, `workspace`.  Press enter to change into the `workspace` directory:

####TODO 13 :
````
myuser@the-command-line:~ (master) $ cd workspace
myuser@the-command-line:~/workspace (master) $
````

If there's a conflict, and you hit tab, the first time you press tab, nothing will happen, the second time, you may here a beep, then bash will display the choices, but narrowed to your search criteria.

##mkdir Making Directories

While working on the command-line, you will often find yourself needing to make directories and files.  We haven't written any letters to our sister yet, so let's take this opportunity to do so.

From your current directory of `~/workspace`, use the `mkdir` command to make a directory called `sister`, where we'll store letter to our dear sister.

####TODO 14 :
````
myuser@the-command-line:~/workspace (master) $ mkdir files/letters/sister
````

Great, in the Cloud9 filesystem pane to the right, you'll now see added a new directory, called `sister`.  Note, we created the new sister directory from outside of its parent directory!  To do that, we had to _first_ spell the path to _where_ we wanted to create our new `sister` directory, which, from our present working directory of `~/workspace`, meant we had to specify `files/letters/sister`.

##Creating, Copying, Moving and Removing Files

###touch

Sometimes you'll find yourself needing to create files on the command-line.  The `touch` command in Linux is intended to change time stamps on files and directories, but it can also create an empty file if one does not already exist.

####TODO 15 :
````
myuser@the-command-line:~/workspace (master) $ touch files/letters/letterhead.txt
````

You'll notice this created an empty text file in the `files/letters/` directory, called `letterhead.txt`

###echo 

`echo` expands variables and prints the evaluation, but it can also be used to redirect text into a new file.  Try this:

####TODO 16 :
````
myuser@the-command-line:~/workspace (master) $ echo "Hey Sis, been a long time... Hope you are well! Love me!" > files/letters/sister/sister-one.txt
````

Now we have a new text file called `sister-one.txt` including our letter content!

###cp Copy File or Directory

You will sometimes need to copy files, and for that, we have the `cp` command.  You should already be in the `~/workspace` directory, so let's change directories into our `files/names` directory and copy a file:

####TODO 17 :

````
myuser@the-command-line:~/workspace (master) $ cd ~/workspace/files/names/
myuser@the-command-line:~/workspace/files/names (master) $ cp 2015-girls.txt 2015-females.txt
````

Nice one, you should see a new file in the `names` directory called `2015-females.txt`!

####mv Move File

Moving files and directories will become part of your work, so let's try that too.  Using the `mv`, we can not only move the file to another directory, we can also _rename_ a file:

####TODO 18 :
````
myuser@the-command-line:~/workspace/files/names (master) $ mv 2015-females.txt ../2015-girls.txt
````

Great stuff, in this last step, you moved the file from our present working directory of `names` to the parent directory of `files`, while _also_ renaming the file!

####rm Remove File

Alrighty, well, we might as well clean up our work a bit.  Stay here in the `names` directory, but let's delete that file we jjst moved:

####TODO 19 :
````
myuser@the-command-line:~/workspace/files/names (master) $ rm ../2015-girls.txt
````

Fantastic, we deleted the `2015-girls.txt` in the `files` directory!  Be careful with the `rm`, it's permanent!

##Manipulating Data

###cat Catenate

We can use <a href="http://en.wikipedia.org/wiki/Cat_%28Unix%29" target="_blank">the `cat` command</a> (short for catenate, a synonym of concatenate) to output contents of a file to the terminal, and can be used to concatenate and list files.

####TODO 20 :
````
myuser@the-command-line:~/workspace (master) $ cd ~/workspace/files/names/
myuser@the-command-line:~/workspace/files/names (master) $ cat 2015-boys.txt 2015-girls.txt > 2015.txt
````

Cool!!! A new file was created, concatenating all the girls and boys from 2015 into one file called `2015.txt`!

Alrighty, let's zoom over to have a look at the letters we wrote dear old dad (don't forget to use autocompletion):

####TODO 21 :
````
myuser@the-command-line:~/workspace/files/names (master) $ cd ../letters/dad/
myuser@the-command-line:~/workspace/files/letters/dad (master) $
````

Let's see what we wrote to dad in our first letter to him.  Though first, let's try our auto complete: start typing `cat dad-`, then press `tab`, twice:

####TODO 22 :
````
myuser@the-command-line:~/workspace/files/letters/dad (master) $ cat dad-
dad-one.txt  dad-two.txt
jfraboni@the-command-line:~/workspace/files/letters/dad (master) $ cat dad-
````

...bash will present you with the remaining possible choices, and return you to where you were in the typing sequence!  Neat!  Continue:

####TODO 23 :
````
myuser@the-command-line:~/workspace/files/letters/dad (master) $ cat dad-one.txt
Dad,

One Lorem ipsum dolor sit amet, vivendo intellegam ne duo. Ubique aliquam vulputate et pro. No sea mentitum signiferumque, ei has eleifend tincidunt. Ei enim nostrum inimicus sed, quod sensibus no ius, dico viderer scriptorem duo ne. Ut sale sadipscing mei, quaeque principes ad vix. Causae maiestatis vim id, cu nec omittantur vituperatoribus.

Etc...
````

Cool, we just printed the contents of our letter to the screen!  `cat` can do some neat things, though not always as intended...

###sed Stream Editor

Check this out use of `cat`, along with the `pipe` and `redirect` features, and in combination with another command `sed` (stream editor).  Using all of these together, we're going to create a form letter:

####TODO 24 :
````
myuser@the-command-line:~/workspace/files/letters/dad (master) $ cat dad-two.txt | sed s/Dad/Mom/g | sed s/Two/Three/g > ../mom/mom-three.txt
````

Running this rather long set of commands will create a file called `mom-three.txt` in the `mom` directory, and you'll notice that the word `Dad` has been replaced with `Mom`, and the letter `Two` replaced with the letter `Three`!

Are you seeing some possiblities here?

Some things to note about the last example.  Unix/Linux commands allow passing the output or result of one command as input to the next command.

The symbol `|`, which means _pipe_, takes the output from the left side command and passes it into the right side command.  And the `>` symbol, which means _redirect_, redirects the output of the left side operation to to some file named on the right - and if that files doesn't exists, as is the case in our last example, it will be created.

Finally, we use the <a href="http://en.wikipedia.org/wiki/Sed" target="_blank">`sed` utility</a>, used for manipulating character streams.  Our usage looks like this: `sed s/Dad/Mom/g`.  Here, we use the _substitute_ command of the `sed` utility (which is what the `s` before the first `/` character signifies), which looks for the character sequence (or regular expression) after the first delimiter (`/`), which in this case is `Dad`, and replaces a match with the character sequece _after_ the next delimiter, which is `Mom`.  Important to note in our usage, we're also applying the subsitution globally to the stream of characters (denoted by the trailing `g` modifier).  If we didn't apply the global modifier, `sed` would only replace the _first_ match, then exit.

`sed` is a powerful command, and we encourage you to read up on all that it can do!

---

Excellent work, superuser, we've come to the end of our brief lesson on using the command line!

We've covered a lot of commands and we only scratched the surface!

Play around with all of them, make them part of your workflow, and Google for more information!