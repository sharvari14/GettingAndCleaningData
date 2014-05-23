GettingAndCleaningData
======================

This repository cotains the following files:

run_analysis.R
CodeBook.md
README.md


R script called run_analysis.R that does the following: 
* Merges the training and the test sets to create one data set.
* Extracts only the measurements on the mean and standard deviation for each measurement. 
* Uses descriptive activity names to name the activities in the data set
* Appropriately labels the data set with descriptive activity names. 
* Creates a second, independent tidy data set with the average of each variable for each activity and each subject. 

CodeBook.md:
* code book that describes the variables, the data, and any transformations or work that you performed to clean up the data.

The data used to generate the files in this repository was downloaded from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

Usage:

source("run_analysis.R")

The latter will run the R script, it will read the dataset and write these files:

merged_clean_data.txt -- 8.35 Mb, a 10299x68 data frame

data_set_with_the_averages.txt -- 0.225 Mb, a 180x68 data frame

The script normally runs for ~30 seconds, but the exact number depends on your system.

Use data <- read.table("data_set_with_the_averages.txt") to read the latter. It is 180x68 because there are 30 subjects and 6 activities, thus "for each activity and each subject" means 30*6=180 rows. Note that the provided R script has no assumptions on numbers of records, only on locations of files.
