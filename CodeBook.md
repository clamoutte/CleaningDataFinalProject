---
title: "Getting and Cleaning Data: Code Book"
output: html_notebook
---

## Project Summary

This project is part of the Getting and Cleaning Data online course in Coursera. The goal of the project is to demonstrate ability in
collecting, processing and cleaning data by creating a tidy data set from data collected from the accelerometers from the Samsung Galaxy S smartphone. 

## Data Sources

Data is directly downloaded from the following URL for the project https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

The original data source for the project can be found here:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

## Data Set Information

(Extracted from the original source)

The experiments were carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, the following data was captured: 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. 

The obtained dataset was randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain.

## Attribute Summary

(Extracted from the original source)

For each record in the dataset it is provided: 
* Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration. 
* Triaxial Angular velocity from the gyroscope. 
* A 561-feature vector with time and frequency domain variables. 
* Its activity label. 
* An identifier of the subject who carried out the experiment.

## Variables

For the purpose of this project, we will only extract the mean and standard deviation measurements for the following variables:

* tBodyAcc-XYZ
* tGravityAcc-XYZ
* tBodyAccJerk-XYZ
* tBodyGyro-XYZ
* tBodyGyroJerk-XYZ
* tBodyAccMag
* tGravityAccMag
* tBodyAccJerkMag
* tBodyGyroMag
* tBodyGyroJerkMag
* fBodyAcc-XYZ
* fBodyAccJerk-XYZ
* fBodyGyro-XYZ
* fBodyAccMag
* fBodyAccJerkMag
* fBodyGyroMag
* fBodyGyroJerkMag

Additionally the following vectors with signal averages will be used:

* gravityMean
* tBodyAccMean
* tBodyAccJerkMean
* tBodyGyroMean
* tBodyGyroJerkMean

## Transformation Steps

The script will perform the following transformations:

1. Merges the training and the test sets to create one data set.
   * For both training and test data set, first need to bind observations with subject ids and activity ids into a single data frame (using c bind)
   * Bind Train and Test Set using rbind
2. Extracts only the measurements on the mean and standard deviation for each measurement.
   * Extract variables that have Mean and Std in names as well as ActivityId and SubjectId using grep
3. Uses descriptive activity names to name the activities in the data set
   * Merge data set with activities file by matching on activity Id
4. Appropriately labels the data set with descriptive variable names.
   * Use Mixed Caps so that labels are more readable
   * Remove unneeded special characters
   * Use underscore instead of commas for valiables that have numbers
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
   * Use dplyr group_by to group by activity and subject id, and summarize all variables using the mean

## Tidy Data Set

The tidy data set consists of 180 observations and 89 variables (variables mapping to mean and sd measurements of the original data set).

Tidy Data Set will be extracted to TidyDataSummary.txt.
