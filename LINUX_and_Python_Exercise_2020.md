17 Nov 2020
#LINUX And Python Exercise
----------------

## Objective for linux part
After this course, the student should be able to
* create and use virtual machine (VM) on a cloud
* remotely access and work on VM on a cloud
* handle directory-related commands and wildcard
* compress and uncompress different file types
* install new software from ubuntu repository
* use text utility commands
* use pipe

## You can use any linux commands or python scripts to do the task 1-23.
## Tasks
1. Create a new virtual machine (VM) at DigitalOcean
2. Copy file exercise_20201117.tar.gz from medbif server (directory /home/medbif/20201117) to your home directory of your new VM. This is your original source file and we won't working directly on this file. We'll copy and work in a working directory.
3. Create a new directory named working in your home directory
4. Copy file exercise_20201117.tar.gz from your home directory to *working* directory
5. Change directory to your *working* directory
6. Uncompress the exercise_20201117.tar.gz inside your *working* directory.
7. Extract selected columns according to the following list from the assignment file. Save each selection in a separate file. The filenames are in parenthesis.
  * First column (first_col.txt)
  * All columns except the first (no_first_col.txt) 
  * Every odd column (odd_col.txt)
  * The first 2 columns and the last 2 columns (first_2_list_2.txt)
8. Create new directory named *extract* in your current *working* directory.
9. Move all extracted file from task 7 to newly created *extract* directory.
10. Compress all files including the extract directory into one compressed file named *extract.7z*. If this file is not in *working* directory, move this file into *working* directory. We would like to compresss using 7z format.
11. Make sure that extract.7z contains all contents as expected. (Check or test the compressed file)
12. Delete all files inside *extract* directory and remove *extract* directory. 

## Now, let's go back and work with the indian_food.csv file. **Please copy your command and result into a text file or Google doc. You'll need to submit this text file in the exam.**
13. Display the first 5 lines of the file and then the last 5 lines.
14. Count the number of lines in the assignment file.
15. Count the number of unique entries in the third column of the indian_food.csv file. (exclude the header)
16. Find the most common entry for column 6.
17. Find the smallest value for column 4, and save the line(s) with this value to a new file (smallest_column_4.txt).
18. Find the largest value for column 5, and save the line(s) with this value to a new file (largest_column_5.txt)
19. Create two new files in /tmp directory, one with the top half of the lines in the assignment file and the other with the bottom half of the lines. We create these 2 new files in /tmp because they are temporary files. And normally, files in /tmp will be automatically deleted when we shut down or restart the system.
20. Create a new file from the two half-files from the previous task, but reverse the order so that the bottom half is now on top. Name the new file as swap_half.txt
21. Sort the indian_food.csv file in reverse order by the last column and save as reverse.txt
22. Create a directory named *text_util* inside your *working* directory and move all newly created files in task 13-21 to the new directory.
23. Create a new copy of the assignment file as *indian_food_na.csv, and change all occurrences of '-1' to 'NA' in the newly created file. (hint. - you may use linux command or python script. It's up to your preference. You'll have to submit your commands or script.)

## Python script part (The following tasks are required to write in Python.)
24. Create a director named *python* inside your *working* directory and put all python scripts here.
### Name python script based on the assigned task i.e. task_24.py
25. Write a python script to count the number of lines of a text file. i.e. running this command should display the number of lines of indian_food.csv - python3 task_25.py indian_food.csv
26. Write a python script to count the number of lines from pipe. i.e. running this command should display the number of lines of indian_food.csv - cat indian_food.csv | python3 task_26.py
27.Write a python script to display the first 5 lines of a text file. i.e. running this command should display the first 5 lines. python3 task_27.py indian_food.csv
28. Write a python script to display the first 5 lines from pipe. i.e. running this command should display the first 5 lines. cat indian_food.csv | python3 task_28.py
29. Write a python script to process data from a indian_food.csv with the following conditions and pipe the result in to a new file names task29_result.csv. (The result file must be csv format.) The running command will be "python3 task29.py indian_food.csv > task29_result.csv".
* If region value is -1, exclude this row.
* If region value is not -1, convert values to contain only the first letter of each word ie. East -> E, North East -> NE.

## General information
Hint: Placing a > at the end of a command, followed by a file name will redirect all output from the command to the file instead of to the screen.

Commands you can use to solve the following tasks (for more info, use man <command>):
* mkdir - create a new directory.
* rmdir - remove directory
* cut - Extract on or more columns.
* head - send the lines at the top of the file to the screen
* tail - send the lines at the bottom of the file to the screen
* wc - count words, characters and lines in the file
* cat - send the full content of the file to the screen
* cp - create a copy of the file
* mv - move the file to a new location, or rename the file
* nano - text editor (search: ctrl-w, replace: ctrl-\, save: ctrl-o, exit: ctrl-x)
* sort - sort the file according to specified columns
* uniq - on a sorted file, will remove duplicate lines and can count the removed lines
* rm - remove files