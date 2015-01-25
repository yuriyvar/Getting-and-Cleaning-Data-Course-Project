# Getting-and-Cleaning-Data-Course-Project - README file
The data for this Project is located on the webserver at the following address: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

For R to use the data it needs to be first downloaded and unzipped using download.file() and unzip() R functions. To do that those functions needs to be placed in R and the new R script file should be stored as run_analysis.R. Remember to set up a working directory using setwd() where the file will be downloaded and unzipped.

Once the zipped file is downloaded and unzipped, two additional folders '/test' and '/train' are created in the newly created directory 'UCI HAR Dataset'. Those folders each contain test and train data that will be used for this assignment.  Files for 'x', 'y' and 'subject' are the data sources that will be used in this exercise. The headers that will be used for the data tables are stored in features.txt file.

The next steps is to start reading those files into R using read.table() R function.
First, download features.txt file for the purpose of analyzing the data and making sure that data headers appear clean and telling; that they are tidy. Then convert all labels into lower characters and remove some extra characters like the parenthesis, the commas, dashes, etc. (tolower() and grep() functions can be used). This is done upfront so when the raw data sets are read, the meaningful column names are assigned to those data sets ('x' files) at the beginning stage. This is for avoiding the further extra steps with inserting column names into the data tables created from 'x' files.

After creating multiple data sets by reading .txt source files, 'x' files are combined using rbind() function, attaching the data sets after each other and forming a unified data set. Same methods are used for combining the 'y' and 'subject' files. The newly created file will have 10,299 observations and 561 in it, with column names coming from features.txt file.

Before proceeding to 'rbinding' the 'y' and 'subject' tables, only those columns that contain 'mean' or 'std' strings in them are selected by using grep() function. This leaves the data set 'comb_X'with 86 columns and 10,299 rows that are left intact.

Once these test and train data tables are combined, each of them will have 10,299 observations. At this point the three tables with 'x', 'y', and 'subject' data is merged  together using cbind() function. This step will form a large data set needed for further analysis with two additional columns with named 'act.label' and 'subject' coming from 'y' and 'subject' files respectively. The data frame is named 'joined_df'.

This is a logical point for importing another lookup table with the numeric labels and variable names for the activities called 'activity_labels.txt', which is located in 'UCI HAR Dataset' folder. Following this step is 'tidying' those activity names by converting them into lower characters and replacing  each '_' in  with a space “ “. The new lookup table 'activities' has two columns: 'act.label' and 'activity.name'.

The next step is to merge the lookup table'activities' with the 'joined_df' data frame on common columns 'act.label', which adds a new column 'activity.name', aligning each activity name with the 'act.label'. As a result, a new data.table 'tidy_dt' is formed that now has 89 columns in it: 86 columns from the 'x' tables + 2 columns from the 'y' and 'subject' tables + the new 'activity.name' column. Since the 'act.label' is no longer needed as redundant, it is removed from the new data table.

The finale step in the assignment instructs to calculate the averages for every column in the latest data table for each activity and each subject, which would create a final data table ('avg_dt'). R function lapply() together with the grouping features of R 'data.table' packages is used to create this new data table with 88 columns and 180 observations (6 activities and 30 subjects grouped together produces  a matrix with 180 various combinations). The 'avg_dt' table is then saved as 'tidy_dataset_w_means.txt' file using write.table() with row.names=FALSE as instructed.
