author: "Gene"
date: "7/7/2020"

'''{r}
# Code Book

This book summarizes the variables included in the *run_analysis.R* file.

## Variables

### Downloaded Data
*x_train* contains data from the X_train.txt file
*y_train* contains data from the y_train.txt file
*subj_train* contains data from the subject_train.txt file
*x_test* contains data from the X_test.txt file
*y_test* contains data from the y_test.txt file
*subj_test* contains data from the subject_test.txt file
*act_labels* contains data from the activity_labels.txt file

### Merging data
*x_data* contains merged data of *x_train* and *x_test*
*y_data* contains merged data of *y_train* and *y_test*
*subj_data* contains merged data of *subj_train* and *subj_test*
*merged_data contains merged data from x_data, y_data and subj_data

### Extracting features
*features* contains data from the features.txt file
*features_mean_std* contains a logical for if the feature includes the text "mean" or "std"
*features_V1* contains the number of each feature with the letter "V" added to match the string in the *merged_data*
*chosen columns* contains the columns that is used to subset the *merged_data* data frame
*merged_data_subset* is the subsetted data frame that includes values for only the features that included the text "mean" or "std"

### New names to columns
*descriptive_names* contains the subset of *features* that is used to rename the column names for the *merged_data_subset*

### Create new text file data set
*data_melted* contains the melted data from the *merged_data_subset* with ids being "Subject" and "Activity"
*Tidy_Data* is the output of the function dcast being used on the melted data frame
