#(B)randeis (A)nti-(P)lagiarism (S)uite 
##Introduction
This tool is using MOSS from Standford University as plagiarsim detection engine and developed by Wenbin Xiao to automatically 
unpack archive files(recursively if necessary), process test files and basefiles then submit to MOSS.

##Prerequisite

* `tar` that can unpack `tar.gz` and `zip`.
* `moss` please go to MOSS [website](http://theory.stanford.edu/~aiken/moss/) to apply for the submission script and follow the installation. 
When you have your `moss`, put it under the same directory of `baps`.
##Usage
`baps -d source_dir -l lang [-b basefiles]`

* `-d` to specify the directory containing source files or source archive
* `-l` to specify the postfix of the language
* `-b` optional, to specify the basefiles directory 

##Example
You have the file structure as following:
    baps -d source_dir -l java -b basefiles
