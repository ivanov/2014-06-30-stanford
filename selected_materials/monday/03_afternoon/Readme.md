## Afternoon project:

**Download set of data files [from here](http://npk.io/evvF+).**

Then, from the command line

1. create a new directory to put the data directory in
2. initialize a git repository in the parent directory
3. Write a shell script to process those files and add todays date to them
4. Commit that script
5. Write a script to count the number of lines in each file and store that to a text file
6. Commit those changes
7. Make a new repository for the project on github
8. Add the new github repositiory as origin for your local working directory
9. Push the changes to github

Solution

1. create a new directory to put the data directory in

    `mkdir afternoon_project`   
    `mv data/ afternoon_project/`    
    `cd afternoon_project/data`

2. initialize a git repository in the data directory

    `git init`

3. Write a shell script (in the data folder, for now) to process those files and add today's date to them

        ##########################################
        # Here's a script to add the date to the end of filenames
        # filename is "rename.sh"

        # Sets today's date, using the format YYYY-MM-DD
        TODAY=$(date +"%Y-%m-%d")

        # rename files passed from the command line to the script, append today's date to each
        for filename in $*
        do
          mv $filename ${filename/.csv/_$TODAY.csv}
        done
        ##########################################

    Call that script: `bash rename.sh *.csv`

4. Commit that script

    `git add rename.sh`    
    `git commit -m "created script to rename files with the date added"`

5. Write a script to count the number of lines in each file and store that to a text file

        ##########################################
        # Script to output the number of lines in each file
        # filename is "linecount.sh"

        for filename in $*
        do
          wc -l $filename
        done
        ##########################################

    This may fail (e.g. say that all the files have 0 lines in them) because the line returns are not unix formatted.   
    This can be fixed by adding the following line to the script like so.

        ##########################################
        # Script to output the number of lines in each file
        # Fixes carriage return problem
        # filename is "linecount.sh"

        for filename in $*
        do
          # replaces incorrect line breaks, outputs a renamed file with correct line break types
          tr '\r' '\n' < $filename > ${filename/-/-tr-}
  
          # output the line count on each of these new fixed files
          wc -l ${filename/-/-tr-}
        done
        ######################################

6. Commit those changes

    `git add linecount.sh`    
    `git commit -m 'created linecount script that also fixes line eding problem'`

7. Make a new repository for the project on github

    Done via github website.

8. Add the new github repositiory as origin for your local working directory

    `git add remote origin <<insert your repository info here>>`

9. Push the changes to github.

    `git push -u origin master`
