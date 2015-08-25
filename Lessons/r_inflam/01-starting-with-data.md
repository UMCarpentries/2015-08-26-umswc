---
layout: page
title: Programming with R
subtitle: Getting Started
output: 
  html_document:
    keep_md: yes
---




> ## Learning Objectives {.objectives}
> * A first look at RStudio
> * Getting the data

### Interacting with R & RStudio

Let's start by learning about our tool:

* It has four different panels: Console, Scripts, Environments, Plots
* Code and workflow are more reproducible if we can document everything that we do.
* Our end goal is not just to "do stuff" but to do it in a way that anyone can
  easily and exactly replicate our workflow and results.
* The best way to achieve this is to write scripts. RStudio provides an
  environment that allows you to do that

There are two main ways of interacting with R: using the console or by using
script files (plain text files that contain your code).

The console window (in RStudio, the bottom left panel) is the place where R is
waiting for you to tell it what to do, and where it will show the results of a
command.  You can type commands directly into the console, but they will be
forgotten when you close the session. It is better to enter the commands in the
script editor, and save the script. This way, you have a complete record of what
you did, you can easily show others how you did it and you can do it again later
on if needed. You can copy-paste into the R console, but the Rstudio script
editor allows you to 'send' the current line or the currently selected text to
the R console using the `Ctrl-Enter` shortcut.

At some point in your analysis you may want to check the content of variable or
the structure of an object, without necessarily keeping a record of it in your
script. You can type these commands directly in the console. RStudio provides
the `Ctrl-1` and `Ctrl-2` shortcuts allow you to jump between the script and the
console windows.

If R is ready to accept commands, the R console shows a `>` prompt. If it
receives a command (by typing, copy-pasting or sent from the script editor using
`Ctrl-Enter`), R will try to execute it, and when ready, show the results and
come back with a new `>`-prompt to wait for new commands.

If R is still waiting for you to enter more data because it isn't complete yet,
the console will show a `+` prompt. It means that you haven't finished entering
a complete command. This is because you have not 'closed' a parenthesis or
quotation. If you're in RStudio and this happens, click inside the console
window and press `Esc`; this should help you out of trouble.

#### Commenting

Use `#` signs to comment. Comment liberally in your R scripts. Anything to the
right of a `#` is ignored by R.

#### Assignment Operator

`<-` is the assignment operator. It assigns values on the right to objects on
the left. So, after executing `x <- 3`, the value of `x` is `3`. The arrow can
be read as 3 **goes into** `x`.  You can also use `=` for assignments but not in
all contexts so it is good practice to use `<-` for assignments. `=` should only
be used to specify the values of arguments in functions, see below.

In RStudio, typing `Alt + -` (push `Alt`, the key next to your space bar at the
same time as the `-` key) will write ` <- ` in a single keystroke.

#### Appearance and Settings

You can change the font size, colors and many other settings for RStudio in `Tools -> Global Options`

###Getting the data

We are studying inflammation in patients who have been given a new treatment for arthritis,
and need to analyze the first dozen data sets.

To start, we need to make a place to store our datafiles. Normally, RStudio defaults to saving and looking for files in `My Documents`, but you probably don't want to keep all of your R data, scripts and output in a single folder. You could just add full or relative paths to all of your R commands get or save data, but then whatever R program you write will not be portable or reproducible. Consider if this was a line in your script (here, read.csv tells R to go into your computer and get the data from the .csv file you specified):


~~~{.r}
read.csv("Z:/RadishData/21MarkersData/SpainIsrael2013Pops/MarkerData2014_forR.csv")
~~~

This command will work perfectly on your computer, but what if you send your script and your datafile to a collaborator? Unless they store the datafile you gave them at `Z:/RadishData/21MarkersData/SpainIsrael2013Pops/MarkerData2014_forR.csv`, the script won't work. One easy way around this is to do your work in `Projects`. This is essentially just an R specific folder that holds all of the data, scripts and output for a specific project. You can give an R project folder to anyone who runs R, and they will be able to reproduce your results without having to resort to editing paths and filenames.

#### Making a project

Start RStudio, click on `File -> New Project`. Choose `New Directory`, then `Empty Project`. RStudio will ask you for a Directory Name and where it should create the new project. Lets name our new directory "SWC_R_exercise" and save it to our Desktop by clicking `Browse` and then selecting the `Desktop`, finally, click `Create Project`. Then close RStudio.

On you Desktop, you should now have a new folder called `SWC_R_exercise`, that contains two files: `.Rhistory` and `SWC_R_exercise.R`. Before we get our data, lets make a folder for it called `Data` inside the `SWC_R_exercise` folder.

Now, lets get the data files and store them in our project folder. Our datasets are at <a href="https://github.com/UMSWC/2015-08-26-umswc/tree/gh-pages/Lessons/r_inflam/data"> datasets</a>.

The data sets are stored in [comma-separated values](reference.html#comma-separated-values-(csv)) (CSV) format. 
The first few rows of each file should look something like this:


~~~{.output}
0,0,1,3,1,2,4,7,8,3,3,3,10,5,7,4,7,7,12,18,6,13,11,11,7,7,4,6,8,8,4,4,5,7,3,4,2,3,0,0
0,1,2,1,2,1,3,2,2,6,10,11,5,9,4,4,7,16,8,6,18,4,12,5,12,7,11,5,11,3,3,5,4,4,5,5,1,1,0,1
0,1,1,3,3,2,6,2,5,9,5,7,4,5,4,15,5,11,9,10,19,14,12,17,7,12,11,7,4,2,10,5,4,2,2,3,2,2,1,1
0,0,2,0,4,2,2,1,6,7,10,7,9,13,8,8,15,10,10,7,17,4,4,7,6,15,6,4,9,11,3,5,6,3,3,4,2,3,2,1
0,1,1,3,3,1,3,5,2,4,4,7,6,5,3,10,8,10,6,17,9,14,9,7,13,9,12,6,7,7,9,6,3,2,2,4,2,0,1,1

~~~


We could go to this page and download each one individually, then move each one from the `Downloads` folder to `SWC_R_exercise`, but now we know enough shell scripting to automate the process (in the SHELL):


~~~{.r}
cd ~/Desktop/
curl -O https://raw.githubusercontent.com/UMSWC/2015-08-26-umswc/gh-pages/Lessons/r_inflam/data/SWC_R.zip
unzip SWC_R.zip -d SWC_R
mv SWC_R/* SWC_R_exercise/Data/
~~~
We `cd` to the `Desktop` directory, so that the zipfile will be downloaded there
`-O` tells curl to save the zipfile as the same filename it has on the web
Because we downloaded a zip file, we need to unzip it
we `SWC_R/*` to get all the files and move them to the SWC_R_exercise folder.

How did we know we needed to download from `https://raw.githubusercontent.com/UMSWC/2015-08-26-umswc/gh-pages/Lessons/r_inflam/data/` 

instead of 

`https://github.com/UMSWC/2015-08-26-umswc/tree/gh-pages/Lessons/r_inflam/data`? 

Click on any of the inflammation files, and what you get is still a formatted webpage, if we download this page, we'll get the data, but it will also have all of the .html code that makes the page pretty. Instead, we want *just* the data. If we click on the various viewing options, we find that `Raw` gives us the format we want. So we use the URL for the `Raw` version.

We can check that everything downloaded correctly by looking in the `SWC_R_exercise` folder:



~~~{.r}
cd ~/Desktop/SWC_R_exercise/Data/
ls -lh
~~~




~~~{.output}
bash: line 0: cd: /Users/Amanda/Desktop/SWC_R_exercise/Data/: No such file or directory
total 2768
-rw-r--r--   1 Amanda  staff   7.3K Aug 25 17:35 01-starting-with-data.Rmd
-rw-r--r--@  1 Amanda  staff   8.5K Aug 25 15:18 01-starting-with-data.md
-rw-r--r--   1 Amanda  staff    12K Aug 25 18:17 01-supp-cond.Rmd
-rw-r--r--   1 Amanda  staff    12K Jul 29 14:00 01-supp-cond.md
-rw-r--r--   1 Amanda  staff    11K Aug 25 18:15 02-loading-and-addressing.Rmd
-rw-r--r--   1 Amanda  staff    19K Aug 25 18:15 02-loading-and-addressing.md
-rw-r--r--   1 Amanda  staff   6.6K Aug 25 18:18 02-supp-loops-in-depth.Rmd
-rw-r--r--   1 Amanda  staff   7.0K Jul 29 14:00 02-supp-loops-in-depth.md
-rw-r--r--   1 Amanda  staff    15K Aug 25 10:48 03-data-structures.Rmd
-rw-r--r--   1 Amanda  staff    42K Aug 25 17:01 03-data-structures.html
-rw-r--r--   1 Amanda  staff    20K Aug 25 10:48 03-data-structures.md
-rw-r--r--   1 Amanda  staff    14K Jul 29 14:00 03-supp-cmdline.Rmd
-rw-r--r--   1 Amanda  staff    17K Jul 29 14:00 03-supp-cmdline.md
-rw-r--r--   1 Amanda  staff    21K Aug 25 18:21 04-func-R.Rmd
-rw-r--r--@  1 Amanda  staff    21K Aug 21 13:06 04-func-R.md
-rw-r--r--   1 Amanda  staff   4.3K Jul 29 14:00 04-supp-making-packages-R.Rmd
-rw-r--r--   1 Amanda  staff   4.3K Jul 29 14:00 04-supp-making-packages-R.md
-rw-r--r--   1 Amanda  staff    11K Aug 25 18:24 05-loops-R.Rmd
-rw-r--r--   1 Amanda  staff    15K Jul 29 14:00 05-loops-R.md
-rw-r--r--   1 Amanda  staff   5.2K Aug 25 18:25 06-best-practices-R.Rmd
-rw-r--r--   1 Amanda  staff   5.1K Jul 29 14:00 06-best-practices-R.md
-rw-r--r--   1 Amanda  staff   1.3K Aug 25 18:26 07-knitr-R.Rmd
-rw-r--r--   1 Amanda  staff   1.5K Jul 29 14:00 07-knitr-R.md
-rw-r--r--   1 Amanda  staff   673B Jul 29 14:00 AUTHORS
-rw-r--r--   1 Amanda  staff   1.4K Jul 29 14:00 CONDUCT.md
-rw-r--r--   1 Amanda  staff   1.8K Jul 29 14:00 CONTRIBUTING.md
-rw-r--r--   1 Amanda  staff   5.3K Jul 29 14:00 LICENSE.html
-rw-r--r--   1 Amanda  staff   3.2K Jul 29 14:00 LICENSE.md
-rw-r--r--   1 Amanda  staff   2.2K Jul 29 14:00 Makefile
-rw-r--r--   1 Amanda  staff   3.6K Jul 29 14:00 README.md
drwxr-xr-x   6 Amanda  staff   204B Jul 29 14:00 _includes
drwxr-xr-x   3 Amanda  staff   102B Jul 29 14:00 _layouts
-rw-r--r--   1 Amanda  staff   655B Jul 29 14:00 arith.R
-rw-r--r--   1 Amanda  staff   706B Jul 29 14:00 check.R
-rw-r--r--   1 Amanda  staff   119B Jul 29 14:00 count-stdin.R
drwxr-xr-x   6 Amanda  staff   204B Jul 29 14:00 css
drwxr-xr-x  21 Amanda  staff   714B Aug 23 22:16 data
-rw-r--r--   1 Amanda  staff   3.3K Jul 29 14:00 discussion.html
-rw-r--r--   1 Amanda  staff   1.1K Jul 29 14:00 discussion.md
drwxr-xr-x  52 Amanda  staff   1.7K Aug 24 12:59 fig
drwxr-xr-x   7 Amanda  staff   238B Aug 25 10:48 figure
-rw-r--r--   1 Amanda  staff   347B Jul 29 14:00 find-pattern.R
-rw-r--r--   1 Amanda  staff   841K Jul 29 14:00 ggplot.pdf
-rw-r--r--   1 Amanda  staff   4.1K Jul 29 14:00 guide.html
-rw-r--r--   1 Amanda  staff   2.0K Jul 29 14:00 guide.md
drwxr-xr-x   3 Amanda  staff   102B Jul 29 14:00 img
-rw-r--r--   1 Amanda  staff   4.3K Aug 25 17:06 index.html
-rw-r--r--@  1 Amanda  staff   1.7K Aug 25 17:06 index.md
-rw-r--r--   1 Amanda  staff    10K Jul 29 14:00 instructors.Rmd
-rw-r--r--   1 Amanda  staff    25K Jul 29 14:00 instructors.html
-rw-r--r--   1 Amanda  staff    14K Jul 29 14:00 instructors.md
drwxr-xr-x   4 Amanda  staff   136B Jul 29 14:00 js
-rw-r--r--   1 Amanda  staff   386B Jul 29 14:00 line-count.R
-rw-r--r--   1 Amanda  staff   3.6K Jul 29 14:00 notes.txt
-rw-r--r--   1 Amanda  staff    63B Jul 29 14:00 print-args-trailing.R
-rw-r--r--   1 Amanda  staff    44B Jul 29 14:00 print-args.R
-rw-r--r--   1 Amanda  staff   217B Jul 29 14:00 readings-01.R
-rw-r--r--   1 Amanda  staff   224B Jul 29 14:00 readings-02.R
-rw-r--r--   1 Amanda  staff   239B Jul 29 14:00 readings-03.R
-rw-r--r--   1 Amanda  staff   442B Jul 29 14:00 readings-04.R
-rw-r--r--   1 Amanda  staff   550B Jul 29 14:00 readings-05.R
-rw-r--r--   1 Amanda  staff   640B Jul 29 14:00 readings-06.R
-rw-r--r--   1 Amanda  staff   766B Jul 29 14:00 readings-usage.R
-rw-r--r--   1 Amanda  staff    10K Jul 29 14:00 reference.html
-rw-r--r--   1 Amanda  staff   5.8K Jul 29 14:00 reference.md
-rw-r--r--   1 Amanda  staff    49B Jul 29 14:00 requirements.txt
-rw-r--r--   1 Amanda  staff    14B Jul 29 14:00 session-info.R
drwxr-xr-x   8 Amanda  staff   272B Jul 29 14:00 tools

~~~
