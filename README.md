GettingCleaningDataProject
==========================

Course project for the Getting and Cleaning Data on Coursera

This is the script that generated the clean dataset, which can be found in the file: run_analysis.R


### Download the data file
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileUrl, dest = "Dataset.zip")
### Unzip the downloaded file
unzip("Dataset.zip")

### Import the 561 feature test dataset
test_dataset <- read.table("./UCI HAR Dataset/test/X_test.txt", header = FALSE)
### Import the 561 feature training dataset
train_dataset <- read.table("./UCI HAR Dataset/train/X_train.txt", header = FALSE)

### Import the features' names
features <- read.table("./UCI HAR Dataset/features.txt", header = FALSE)
### Clean the names from special characters, like: "(" ")" "-" "_" ","
clean_features <- gsub("-|_|\\(|\\)|,", "", features[,2])

### Assign the appropriate name to the two datasets columns
names(test_dataset) <- clean_features
names(train_dataset) <- clean_features

### As requested in the assignment, I proceed to remove the columns which are not representing means (mean) or standard deviations (std)
test_dataset <- subset(test_dataset, select = grep("mean|std", names(test_dataset)))
train_dataset <- subset(train_dataset, select = grep("mean|std", names(train_dataset)))

### Import the test dataset users
test_users <- read.table("./UCI HAR Dataset/test/subject_test.txt", header = FALSE)
### Import the training dataset users
train_users <- read.table("./UCI HAR Dataset/train/subject_train.txt", header = FALSE)

### Add a column with the respective users
test_dataset$user <- test_users[[1]]
train_dataset$user <- train_users[[1]]

### Import the activity labels
activity_labels <- read.table("./UCI HAR Dataset/activity_labels.txt", header = FALSE)

### Import the test activities
test_activities <- read.table("./UCI HAR Dataset/test/y_test.txt", header = FALSE)
### Import the training activities
train_activities <- read.table("./UCI HAR Dataset/train/y_train.txt", header = FALSE)

### Create two new vectors with the activities labels
### Note: I don't need complex matching in the activities labels, as the first
###       row corresponds to value 1, the second to value 2, and so on...
test_activities_labels <- as.character(activity_labels[test_activities[[1]],2])
train_activities_labels <- as.character(activity_labels[train_activities[[1]],2])

### Now we are ready to add the last two columns with the activity labels
test_dataset$activities <- test_activities_labels
train_dataset$activities <- train_activities_labels

### Finally we are ready to bind the two datasets
dataset <- rbind(test_dataset, train_dataset)

### Now we can cleanup the memory from useless data
rm(features,test_activities,test_dataset,test_users,train_activities,train_dataset,train_users,clean_features,test_activities_labels,train_activities_labels, activity_labels)

### Create the second dataset grouping by activities and users:
tidy_dataset <- aggregate(dataset, by=list(dataset$user,dataset$activities), FUN=mean)
### Remove the duplicated columns for users and Activities after the aggregation
tidy_dataset <- subset(tidy_dataset, select = -c(user,activities))
### Assign proper names for groups
names(tidy_dataset)[1] <- "user"
names(tidy_dataset)[2] <- "activities"

### Finally we save the tidy_dataset to file
write.table(tidy_dataset, file = "tidydata.txt")
