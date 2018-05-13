# Vehicle Detection and Tracking Project

## Get HOG and color histogram features
First, I load the training pictures with the **function load_car_not_car_images()**, this function was inspired by this [excellent post](https://towardsdatascience.com/vehicle-detection-and-tracking-6665d6e1089b). Then I use these three functions **get_hog_features()**, **color_hist()** and **extract_features()** provided in the course to extract the HOG features and color histogram features. Before extracting features, I first convert the pictures to YCrCb color space. For color histgram features, I set number of bins to be 32 and get histograms for all the three channels. For the HOG features, I use 32 number of bins, 16 pix per cell and 2 cell per block. I also extract HOG features for all color channels.

## Split and normalize data
Next, I split the data features into 80% training data and 20% test data. I used the StandardScaler() function to normalize the features.

## Train the classifier.
Next, I tried several different classifiers and finally chose the Support vector machine with rbf kernel and parameter C=10 as the classifier for this project. The test accuracy for this classifier was 0.9916.

## Sliding Window Search and heat map
Next, I modified the **find_cars()** function provided by the course to do sliding window search. Instead of setting only one scale, I set a list of scales from 1 to 3. By doing this, I can detect the cars both close to the our vehicle and far away from our vehicle. One example was shown below:

![find_cars_image](https://note.youdao.com/favicon.ico)

Then, I applied the functions **add_heat()**, **apply_threshold()** and **draw_labeled_bboxes()**. The threshold I chose here is 2. I got the following result:

![apply_threshold_image](https://note.youdao.com/favicon.ico)

## Final Processor
Finally, I put everything together to get the final processor. I also added the lane detection functions from last project into the final processor. The final video was in the 'test_videos_output' folder. My final result looks well except several false positives.

## Discussions

One problem with my detection processor is that it works extremely slow. It tooks more than 5 hours to make the 50 seconds final video. One reason is that here I used too many different scales in the **find_cars()** function. I also re-run the processor with less scales. By doing this, the processor worked faster, but the result had more false positives. 