# Getting-and-Cleaning-Data-Course-Project

## Project
This is the readme file for the Getting and Cleaning Data Course Project through Coursera. The purpose is to demonstrate clear ability to obtain data and modify to create a tidy data set. The data used comes from the Human Activity Recognition and Smart Phone Data section of the UCI Machine Learning Repository website.

## Files

Run_analysis.R is a program that downloads the data from the UCI website, and then prepares the data to be outputted into its final form as Tidy_Data.txt.
It merges multiple data sets, modifies the names of each column, ses descriptive activity names to name the activities, extracts a subset of only the mean and standard deviation measurements and outputs the data to the final, Tidy_Data.txt file. 

CodeBook.md is a file that describes the steps taken, variables used, and transformations performed in the run_analysis.R file.

Tidy_Data.txt is the final data file with the appropriate table and values in one text file.

## Run_Analysis Process

**Step 1: Download and load files**

Download zip file from the appropriate url location and pull each txt file from the folder "UCI HAR Dataset" using read.table.

**Step 2: Merges the training and the test sets.**

Create one data set including subject (subj_train & subj_test), activity (y_train and y_test) and features (x_train and t_test) data with cbind and rbind. This results in a full data set, merged_data.

**Step 3: Extracts the features for only the measurements on the mean and standard deviation for each measurement.**

Use the grepl function to search the features.txt file (loaded as a data frame, features) for mean and standard deviation (std) resulting in features_mean_std.

**Step 4: Apply new names to the columns of the merged_data data frame**

The subset of the features table and the name "Subject" and "Activity" are then used to create a vector, chosen columns, with the column names. Those column names are assigned to the merged_data names.

**Step 5: Extract from the data frame, data that only includes the mean and standard deviation**

Features_mean_std is used to subset the merged_data to only include the mean and standard deviation values in merged_data_subset.

**Step 6: Appropriately labels the data set with descriptive variable names.**

The descriptions from features are then used to rename the columns in the merged_data_subset to be more descriptive. The gsub function is used to clarify the shorthand that was used for time (t) and frequency (f).

**Step 7: Use descriptive activity names to name the activities in the data set**

The activity_labels.txt file (loaded as act_labels data frame) is then used to assign descriptive names to the Activity variable.

**Step 8: Create a second, independent tidy data set with the average of each variable for each activity and each subject**

The Tidy_data data frame is then created by grouping by subject and activity and calculating the mean for each. It is then exported to Tidy_Data.txt. '''
