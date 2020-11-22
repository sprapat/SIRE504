17 Nov 2020

# Solution for LINUX And Python Exercise

Your solution may be different but it gives the correct result. That's fine.

You can compare your method with the solution on the following criteria.
* Correctness
* Concise and easy to understand
* Performance

## Tasks
1. Create a new virtual machine (VM) at DigitalOcean
````console
# Just follow the instruction.
# So you learn how to use resources on cloud.
# After you ssh into your new droplet, you can update and upgrade the system
# If you are already root user, you don't need sudo command.

apt update && apt upgrade
````
2. Copy file exercise_20201117.tar.gz from medbif server (directory /home/medbif/20201117) to your home directory of your new VM. This is your original source file and we won't working directly on this file. We'll copy and work in a working directory.
````console
# use scp command to copy to/from remote server
scp medbif@128.199.244.205:/home/medbif/20201117/exercise_20201117.tar.gz .

# but if you are certain that there is only one file there, you can use wildcard.
scp medbif@128.199.244.205:/home/medbif/20201117/* .
````
3. Create a new directory named working in your home directory
````console
mkdir working
````

4. Copy file exercise_20201117.tar.gz from your home directory to *working* directory
````console
# You can use tab completion to help you with the filename.
# Or you can use wildcard to make it match only the file you want.
cp exercise_20201117.tar.gz working
````

5. Change directory to your *working* directory
````console
cd working
````

6. Uncompress the exercise_20201117.tar.gz inside your *working* directory.
````console
tar zxvf exercise_20201117.tar.gz
````

7. Extract selected columns according to the following list from the assignment file. Save each selection in a separate file. The filenames are in parenthesis.
  * First column (first_col.txt)
  ````console
# To use comma as separator for cut command, you can just type comma after -d option.
# There is no need to wrap comma between quotes.
cut -d, -f 1 indian_food.csv > first_col.txt
  ````

  * All columns except the first (no_first_col.txt)
  ````console
cut -d, -f 2- indian_food.csv > no_first_col.txt
  ````  
  * Every odd column (odd_col.txt)
  ````console
# You can see the column headers with their numbers using the following command.
medbif@medbif:/tmp/working$ head -n 1 indian_food.csv | tr , '\n' | nl
     1  name
     2  ingredients
     3  diet
     4  prep_time
     5  cook_time
     6  flavor_profile
     7  course
     8  state
     9  region

# Then you can use cut to get the columns you want.
cut -d, -f 1,3,5,7,9 indian_food.csv > odd_col.txt
  ````    
  * The first 2 columns and the last 2 columns (first_2_list_2.txt)
  ````console
cut -d, -f 1,2,8,9 indian_food.csv > odd_col.txt
  ````  

8. Create new directory named *extract* in your current *working* directory.
````console
mkdir extract
````

9. Move all extracted file from task 7 to newly created *extract* directory.
````console
# Since all new files have .txt extension, we can use wildcard for that.
# Don't forget to use tab completion for quickly typing the directory name.
mv *.txt extract/
````

10. Compress all files including the extract directory into one compressed file named *extract.7z*. If this file is not in *working* directory, move this file into *working* directory. We would like to compresss using 7z format.
````console
# First you need to install new software.
apt install p7zip-full

# Then you can search internet, option help or man command to learn how to use 7z command.
7z a extract.7z extract
````

11. Make sure that extract.7z contains all contents as expected. (Check or test the compressed file)
````console
# To test the compressed file, you don't need to really extract it.
# There is an option to test the file.
7z t extract.7z

````

12. Delete all files inside *extract* directory and remove *extract* directory. 
````console
# You can do the task in 2 steps. 1) delete all files inside extract dir. 2. use rmdir command to remove empty dir.
# Or you can use -r option of rm to remove all contents in one step.
# But please be careful when you use -r option especially when you are root user.
# Because rm -r / can wipe all harddisk contents.
# One mistake likes having an extra space between / and dir name can be a disaster.
# For example
# instead of typing
# rm -r /trash_this
# you type
# rm -r / trash_this

rm -r extract
````

13. Display the first 5 lines of the file and then the last 5 lines.
````console
head -n 5 indian_food.csv

tail -n 5 indian_food.csv
````

14. Count the number of lines in the assignment file.
````console
wc -l indian_food.csv
````

15. Count the number of unique entries in the third column of the indian_food.csv file. (exclude the header)
````console
# If you know that you'll work a lot on data without header, you can create temporary files
# that contains only head and data.
head -n1 indian_food.csv > /tmp/header.csv
tail -n+2 indian_food.csv > /tmp/data.csv

# Now, you can cound unique entries.
cut -d, -f 3 indian_food.csv | sort | uniq -c

# If you haven't prepared the temporary files, you can use.
tail -n+2 indian_food.csv | cut -d, -f 3 | sort | uniq -c
````

16. Find the most common entry for column 6.
````console
# We count the number of each entry and sort numerically in reversed order
# to put the largest value at the top.
# We don't cut only the first line because there may be more than 1 entry with the same count.
cut -d, -f 6 indian_food.csv | sort | uniq -c | sort -nr
````

17. Find the smallest value (exclude -1) for column 4, and save the line(s) with this value to a new file (smallest_column_4.txt).
````console
# This task is actually 2 tasks.
# The first one is to find the smallest value.
# We have to escape the minus sign using backslash for grep.
cut -d, -f 4 /tmp/data.csv | grep -v "\-1" | sort -n | head -n 1
5

# The secone one is to use the smallest value (which is 5) to save the line(s) that contain(s) the value to a new file
# I use awk.
awk -F , '{if($4==5) print $0;}' /tmp/data.csv > smallest_column_4.txt
````

18. Find the largest value for column 5, and save the line(s) with this value to a new file (largest_column_5.txt)
````console
# This is similar to task 17
cut -d, -f 5 /tmp/data.csv | grep -v "\-1" | sort -nr | head -n 1
720

awk -F , '{if($5==720) print $0;}' /tmp/data.csv > largest_column_5.txt
````

19. Create two new files in /tmp directory, one with the top half of the lines in the assignment file and the other with the bottom half of the lines. We create these 2 new files in /tmp because they are temporary files. And normally, files in /tmp will be automatically deleted when we shut down or restart the system.
````console
# There are 255 lines of data.
wc -l data.csv
255

# Put the top 128 lines in one file and the rest in another file
head -n 128 /tmp/data.csv > /tmp/top.csv
tail -n +129 /tmp/data.csv > /tmp/bottom.csv
````
20. Create a new file from the two half-files from the previous task, but reverse the order so that the bottom half is now on top. Name the new file as swap_half.txt
````console
# put header and everything as requested
cat /tmp/header.csv /tmp/bottom.csv /tmp/top.csv > swap_half.txt
````
21. Sort the indian_food.csv file in reverse order by the last column and save as reverse.txt
````console
# sort the last column in reverse order
sort -t, -k9,9r /tmp/data.csv > /tmp/data_reverse.txt

# put the header back
cat header.csv /tmp/data_reverse.txt > reverse.txt
````
22. Create a directory named *text_util* inside your *working* directory and move all newly created files in task 13-21 to the new directory.
````console
mkdir text_util

# use wildcard to move all text files at once.
mv *.txt text_util/
````
23. Create a new copy of the assignment file as *indian_food_na.csv*, and change all occurrences of '-1' to 'NA' in the newly created file. (hint. - you may use linux command or python script. It's up to your preference. You'll have to submit your commands or script.)
````console
# using sed command seems to be the simplest command.
sed 's/-1/NA/g' indian_food.csv > indian_food_na.csv
````

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