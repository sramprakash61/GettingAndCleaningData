Purpose
This script processes data from the Human Activity Recognition Using Smartphones Dataset to extract the average means and standard deviations of each variable for a given subject and activity, returning a tidy data frame containing these values.

The script was prepared to meet the requirements of an assignment in the Getting and Cleaning Data Course offered on Coursera

Source Data

File Downloaded from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip
Full details can be found here: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Assumptions
The script assumes the data will be found in the directory "./UCI HAR Dataset/" structured as it is in the linked archive. The script requires that the packages "plyr" and "reshape2" are available. I have configured the path to my windows local system path (C:\\Users\\rxs755\\Desktop\\DS\\data1) and you will see the same thorough out the script. 

Use
To use the script at the prompt, call source("~/run_analysis.R") correcting for file location, then run_analysis(). Assigning the ouput of the script to a data frame is recomended, since the resulting table is too large to simply read on screen.

Functionality
The script imports the test and training datasets (x_test.txt and x_train.txt) from the UCI HAR data and combines them into a single dataframe, with the columns named from the features.txt file provided in the archive.Partial string matching using grep is used to identify the columns that include mean() and std() in their name. These columns of interest are then assigned to a new data frame.

The activity labels for each observation (provided in y_test.txt and y_train.txt) are converted from numeric vectors to factors with the corresponding text activity label (found in activity_labels.txt) using the mapvalues function from plyr, and this factor is added to the data frame containing all the mean and standard deviation observations. An additional column containing the subject id for each observation (read in from subjects_test.txt and subjects_train.txt) is also included.

The data frame is then averaged for each subject and activity for each variable, resulting in a data frame with 180 rows and 81 columns (subject, activity, then the 79 variables from the data set meeting the criteria). This is accomplished using the melt and dcast functions in the reshape2 library*.

This data frame is returned from the function, meeting the requirements of the assignment.