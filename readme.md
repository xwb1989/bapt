#(B)randeis (A)nti-(P)lagiarism (T)ool
##Introduction
This tool is using MOSS from Standford University as plagiarsim detection engine and developed by Wenbin Xiao to automatically 
unpack archive files(recursively if necessary), process test files and basefiles then submit to MOSS.

##Prerequisite

* Python 2.x
* `moss` please go to MOSS [website](http://theory.stanford.edu/~aiken/moss/) to apply for the submission script 
and follow the installation. When you have your `moss`, put it under the same directory of `bapt`.

##Usage

    bapt -l lang [-b basefiles] -d dir1 [dir2, dir3, ...]

* `-l` to specify the postfix of the language
* `-b` optional, to specify the basefiles directory 
* `-d` to specify the directories containing files or archives

##How it works
BAPT will go through directories specified by `-d` with two procedures:

* If there is an archive file, it will create a directory based on the archive name, then extract files in the 
archive to that directory; if will only extract files with extension specified by `-l` option. Extraction
is recursive, it means files in sub-archives inside that archive will also been extracted.
* If there is a directory, it will recursively "flatten" the directory such that all files in sub-directories will
be moved out to the directory and then sub-directories will be removed.

After preprocessing all files, it will upload them along with basefiles(if the basefile directory is specified by 
        `-b`) to MOSS.

##Example

###Basic
Assuming you have a directory `source_dir` as following:

    source_dir/
    ├── Alice.tar
    │   ├── nested-archive.tar
    │   │   ├── file11.java
    │   │   └── file12.java
    │   ├── file1.java
    │   └── file2.java
    └── Bob.tar
    │   ├── file1.java
    │   └── file2.java
    └── James/
        ├── sub-dir/
        │   └── file11.java
        ├── file1.java
        └── file2.java
 
If you run command like:

    bapt -l java -b basefiles -d source_dir

After pre-processing, it becomes:

    source_dir/
    ├── Alice/
    │   ├── file1.java
    │   ├── file11.java
    │   ├── file12.java
    │   └── file2.java
    └── Bob/
    │   ├── file1.java
    │   └── file2.java
    └── James/
        ├── file1.java
        ├── file11.java
        └── file2.java

And then all java files will be submitted to MOSS.

###Multiple Directories
You can also submit multiple directories. It can be easily achieved by specifying multiple directories for `-d`.
Example: 

    bapt -l java -b basefiles -d source_dir/2013 source_dir/2014

This is useful when you want to check assignment solutions from different classes. 

