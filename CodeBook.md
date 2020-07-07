---
title: "CodeBook"
author: "Gene"
date: "7/7/2020"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
'''{r}
## R Markdown

# Load dplyr
library(dplyr)

#Check if folder exists
if(!file.exists("./data")){dir.create("./data")}

#download file and unzip
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileUrl,"./data/human_rec.zip", method="curl")

if(!file.exists("UCI HAR Dataset")){
	unzip("./data/human_rec.zip")
	print("hi")
}

#Load Training and test sets into R
x_train <- read.table("./UCI HAR Dataset/train/X_train.txt")
y_train <- read.table("./UCI HAR Dataset/train/y_train.txt")
subj_train <- read.table("./UCI HAR Dataset/train/subject_train.txt")
x_test <- read.table("./UCI HAR Dataset/test/X_test.txt")
y_test <- read.table("./UCI HAR Dataset/test/y_test.txt")
subj_test <- read.table("./UCI HAR Dataset/test/subject_test.txt")
act_labels <- read.table("./UCI HAR Dataset/activity_labels.txt")

## Merges the training and the test sets to create one data set.
# first concatenate by rows 
x_data <- rbind(x_train, x_test)
y_data <- rbind(y_train, y_test)
subj_data <- rbind(subj_train, subj_test)

#Rename y_data and subj_data column names to avoid confusion
names(y_data)<- "Activity"
names(subj_data) <- "Subject"

merged_data <- cbind(subj_data,x_data,y_data)
names(merged_data)

## Extracts only the measurements on the mean and standard deviation for each measurement.
#Load features.txt to understand rows aligned with mean and standard deviation
features <- read.table("./UCI HAR Dataset/features.txt")

#change V2 column from factor variable to character
features[,2]<- as.character(features[,2])

#subset rows from features to select only those with "mean" or "std"
features_mean_std <- grepl("mean|std", features[,2])
features_V1 <- paste0("V",features$V1[features_mean_std])
chosen_columns <- c("Subject",features_V1,"Activity")

merged_data_subset <- subset(merged_data, select = chosen_columns)

#Update names of columns to be descriptive
descriptive_names <- features$V2[features_mean_std]
names(merged_data_subset) <- c("Subject",descriptive_names,"Activity")

#Use descriptive activity names to name the activities in the data set
merged_data_subset$Activity <- act_labels[merged_data_subset$Activity, 2]

#update t and f to appropriate description
names(merged_data_subset)<-gsub("^t", "time", names(merged_data_subset))
names(merged_data_subset)<-gsub("^f", "frequency", names(merged_data_subset))

#New Data set
library(reshape2)
data_melted <- melt(merged_data_subset, id = c("Subject", "Activity"))
Tidy_Data <- dcast(data_melted, Subject + Activity ~ variable, mean)

write.table(Tidy_Data, file = "Tidy_Data.txt",row.name=FALSE)

library(knitr)
knit2html("./data/codebook.md")

'''