# Getting and Cleaning Data Project Assignment

## This code book provides explanation on the data used in the Project.

A zipped file is downloaded and stored as 'GCD_Project_Dataset.zip' from the above web address in the working directory set with setwd() .

Once the download is confirmed, the fiel is uzipped into the same directory. IT contains subdirectories '/test' and '/train' in the 'UCI HAR Dataset' folder. In this folder there is a file named features.txt, containing the headers that will be used for reading data files 'x_test.txt and x_train.txt'. The number of rows in features.txt corresponds with the number of columns in the 'x' files named above.

FEATURES.txt
	Column Names: V1, V1 – 561 observations in each
		- V1 is integer
		- V2 is character

x_test.txt and x_train.txt files each contain 561 columns with numeric data
	- x_test.txt contains 2,947 observations
	- x_train.txt – 7,352 observations
	
y_test.txt, subject_test.txt, y_train.txt, subject_train.txt 
		- each consist of 1 column of integers
		- 'test' files are 2,947 and 'train' files – 7,352 rows long

After combining and merging 'x', 'y', and 'subject' data sets (removing unnecessary columns that are not pertinent to this analysis) a large data set 'joined_df' is formed by using cbind() function with the combined tables above.

'joined_df' has preserved legacy data formatting from the merged tables, consisting of 86 numeric columns from the 'x' tables and two integer columns from 'y' and 'subject' data sets. Column examples are as follows, where 't' in the column name denotes time and 'f' indicates the frequency domain signals:

- tBodyAcc-XYZ
- tGravityAcc-XYZ
- tBodyAccJerk-XYZ
- tBodyGyro-XYZ
- tBodyGyroJerk-XYZ

- fBodyGyro-XYZ
- fBodyAccMag
- fBodyAccJerkMag
- fBodyGyroMag
- fBodyGyroJerkMag

A lookup table 'activities' is formed from the 'activity_labels.txt' file. It contains two columns (names assigned at reading): 'act.label' – integer and 'activity.name' – character and 6 rows.
This table is used to assign variable names to the values of 'act.label” column in the 'joined_df' data table.

Merging the two tables mentioned above: 'joined_df' and 'activities' produce the data table 'tidy_dt'. The table preserved its previous structure and formatting, adding one more character column. It has 89 columns and 10,299 observations.

Following the merge, the 'act.label' column is removed from the 'tidy_dt' table in accordance with 'tidy'data principles as being redundant and not meaningful. 

Per the final Project instructions, a new data set is formed by computing averages for every column in the data table grouped by columns 'activity.name' and 'subject'. The new data table 'avg_dt', consisting of 180 by 88 matrix  is stored as 'tidy_dataset_w_means.txt' file as per the Project's requirements. It has:
- one character column named 'activity.name' used for grouping 
- one integer column 'subject' also used for grouping
- 86 numeric columns of calculated averages from the 'mean' or 'std' columns gathered from the 'x' tables earlier
