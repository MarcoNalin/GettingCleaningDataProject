DATA DICTIONARY - Wearable Computing
====================================

# HOW DATA WAS GENERATED

First of all the file with data was downloaded from:
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

And it was unzipped in the working directory

Then two separate data sets with the 561 features were imported (test dataset and train dataset), opening the files X_train.txt and X_test.txt

Features names were taken from the file "features.txt" and assigned to the column names of both datasets.
Before doing this step, some special characters were removed from the names, in particular: "(" ")" "-" "_" ","

The assignment required to consider only means and standard deviations, so I dropped from the two data frames
the columns which didn't match the regular expression "mean|std"

The next step was to add the users from the files subject_XXXX.txt (where XXXX was "train" and "test") of the two subfolders train and test.

Activities' labels were imported from the file "activity_labels.txt"

One additional column was added to each of the two datasets, tanking values from the files y_test.txt and y_train.txt, matching the labels in "activity_labels.txt"

In the end, the complete data set was created using rbind with the two data frames.

At this point the second dataset was created by aggregating data per users and activities.

Finally, the second dataset was saved in the file "tidydata.txt"


# DATA
##GENERAL DATA

user
	The users' IDs
	
activities
	Labels with the activities' names:
		1 WALKING
		2 WALKING_UPSTAIRS
		3 WALKING_DOWNSTAIRS
		4 SITTING
		5 STANDING
		6 LAYING

##TIME RELATED DATA		
		
tBodyAccmeanX
tBodyAccmeanY
tBodyAccmeanZ
tBodyAccstdX
tBodyAccstdY
tBodyAccstdZ
	Means and standard deviations for the three axis of the body acceleration (data related to time)
	
tGravityAccmeanX
tGravityAccmeanY
tGravityAccmeanZ
tGravityAccstdX
tGravityAccstdY
tGravityAccstdZ
	Means and standard deviations for the three axis of the gravity acceleration (data related to time)

tBodyGyromeanX
tBodyGyromeanY
tBodyGyromeanZ
tBodyGyrostdX
tBodyGyrostdY
tBodyGyrostdZ
	Mean and standard deviations for the three axis of the gyroscope data (data related to time)

The body linear acceleration and angular velocity were derived in time
to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). 	
	
tBodyAccJerkmeanX
tBodyAccJerkmeanY
tBodyAccJerkmeanZ
tBodyAccJerkstdX
tBodyAccJerkstdY
tBodyAccJerkstdZ
	Mean and standard deviations for the three axis of the Jerk data of the body acceleration (data related to time)

tBodyGyroJerkmeanX
tBodyGyroJerkmeanY
tBodyGyroJerkmeanZ
tBodyGyroJerkstdX
tBodyGyroJerkstdY
tBodyGyroJerkstdZ
	Mean and standard deviations for the three axis of the Jerk data of the gyroscope (data related to time)

Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm
(tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

tBodyAccJerkMagmean
tBodyAccJerkMagstd
	Magnitude of body acceleration Jerk data mean and standard deviation (data related to time) 

tBodyGyroJerkMagmean
tBodyGyroJerkMagstd
	Magnitude of gyroscope Jerk data mean and standard deviation (data related to time) 

tBodyAccMagmean
tBodyAccMagstd
	Magnitude of body acceleration mean and standard deviation (data related to time) 

tGravityAccMagmean
tGravityAccMagstd
	Magnitude of gravity acceleration mean and standard deviation (data related to time) 
	
tBodyGyroMagmean
tBodyGyroMagstd	
	Magnitude of gyroscope data mean and standard deviation (data related to time) 


##FREQUENCY RELATED DATA		
Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ,
fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag.

fBodyAccmeanX
fBodyAccmeanY
fBodyAccmeanZ
fBodyAccstdX
fBodyAccstdY
fBodyAccstdZ
fBodyAccmeanFreqX
fBodyAccmeanFreqY
fBodyAccmeanFreqZ
	Means and standard deviations for the three axis of the body acceleration (data related to frequency)
	
fBodyAccJerkmeanX
fBodyAccJerkmeanY
fBodyAccJerkmeanZ
fBodyAccJerkstdX
fBodyAccJerkstdY
fBodyAccJerkstdZ
fBodyAccJerkmeanFreqX
fBodyAccJerkmeanFreqY
fBodyAccJerkmeanFreqZ
	Mean and standard deviations for the three axis of the Jerk data of the body acceleration (data related to frequency)

fBodyGyromeanX
fBodyGyromeanY
fBodyGyromeanZ
fBodyGyrostdX
fBodyGyrostdY
fBodyGyrostdZ
fBodyGyromeanFreqX
fBodyGyromeanFreqY
fBodyGyromeanFreqZ
	Mean and standard deviations for the three axis of the gyroscope data (data related to frequency)

fBodyAccMagmean
fBodyAccMagstd
fBodyAccMagmeanFreq
	Mean and standard deviations for the body acceleration magnitude (data related to frequency)
	
fBodyBodyAccJerkMagmean
fBodyBodyAccJerkMagstd
fBodyBodyAccJerkMagmeanFreq
	Mean and standard deviations for the magnitude of body acceleration jerk data (data related to frequency)

fBodyBodyGyroMagmean
fBodyBodyGyroMagstd
fBodyBodyGyroMagmeanFreq
	Mean and standard deviations for the gyroscope data magnitude (data related to frequency)

fBodyBodyGyroJerkMagmean
fBodyBodyGyroJerkMagstd
fBodyBodyGyroJerkMagmeanFreq
	Mean and standard deviations for the jerk gyroscope data magnitude (data related to frequency)
