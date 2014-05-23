## this file describes the purpose of run_analysis.R and the output files produced by running said script.

The UCIHAR Dataset is the described as following from the source[1]:

The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. Check the README.txt* file for further details about this dataset.


Source of the original data: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip . Original description: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

The attached R script (run_analysis.R) performs the following to clean up the data:

1. Merges the training and test sets to create one data set, namely
train/X_train.txt with test/X_test.txt -- the result is a 10299 x 561 data frame, as in the original description ("Number of Instances: 10299" and "Number of Attributes: 561")

train/subject_train.txt with test/subject_test.txt -- the result is a 10299 x 1 data frame with subject IDs,

train/y_train.txt with test/y_test.txt -- the result is also a 10299 x 1 data frame with activity IDs.

2. Reads file features.txt and extracts only the measurements on the mean and standard deviation for each measurement.
The result is a 10299 x 66 data frame, because only 66 out of 561 attributes are measurements on the mean and standard deviation. All measurements appear to be floating point numbers in the range (-1, 1).

3. Reads activity_labels.txt and applies descriptive activity names to name the activities in the data set:
walking

walkingupstairs

walkingdownstairs

sitting

standing

laying

4. The script also appropriately labels the data set with descriptive names: all feature names (attributes) and activity names are converted to lower case, underscores and brackets () are removed.
Then it merges the 10299x66 data frame containing features with 10299x1 data frames containing activity labels and subject IDs.

The result is saved as merged_clean_data.txt, a 10299x68 data frame such that the first column contains subject IDs, the second column activity names, and the last 66 columns are measurements. Subject IDs are integers between 1 and 30 inclusive. Names of the attributes are similar to the following:

tbodyacc-mean-x

tbodyacc-mean-y

tbodyacc-mean-z

tbodyacc-std-x

tbodyacc-std-y

tbodyacc-std-z

tgravityacc-mean-x

tgravityacc-mean-y

5. Finally, the script creates a 2nd, independent tidy data set with the average of each measurement for each activity and each subject.
The result is saved as data_set_with_the_averages.txt, a 180x68 data frame, where as before, the first column contains subject IDs, the second column contains activity names (see below), and then the averages for each of the 66 attributes are in columns 3...68. There are 30 subjects and 6 activities, thus 180 rows in this data set with averages.
