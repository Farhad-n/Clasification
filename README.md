# Dog Breed Identification
## Farhad Navid 

The goal of this analysis is to identify the various breed of dogs using Dog images provided in kaggle data set. 

This document is intended to go through the entire process step by step and at each step talk about the challenges faced during this project. 

**Files:**
> 1. **DB_EDA.jpynb** ====>This file performs the normal EDA type analysis on the data set.
> 2. **Data_Prep.jpynb** ===>This file does the data preparation for the analysis including the augmentation. 
> 3. **Models.jpynb** =====>This file contains the models we will use.
> 4. **ReadMe.txt** =======>The read me file for the repository. 
> 5. **Licenses** =========>The license file
> 6. **Document.jpynb** ===>This document have instruction on creating AWS instance and loading up the files and datasets to AWS EBS system. please note these are some points I came across and I hope you find it helpful.

Following section is the step by step instruction    

**Steps:**
1. Initiate AWS E2 instance to run this project.
 * Upload the data files.
 * Unzip the data files.
 * Upload the jupyter notebook files. 
2. EDA, Examine some basic characteristic of the dataset, Histogram, file structure, dim, ...
3. Preprocess the images. resize and reshape i.e. All the picture having the same dimension. 
4. Create training data set X_train, y_train, Xtrain will have the images and Y_train will have the lable. 
6. Augment the data.  Need to add more images to the data set. 
 * Pick random number of images  
 * Create 5X per image.  Rotate, Flip, color, shift, 
 * reshuffle the training data set
 * add the newly created images to the training set directory.
 * recreate the X_train and y_train NumPy array.
7. Create the X_test dataset this is test data set.
8. Prepare data to fit into a deep learning model Create a 20, 80 splits for train and validate data set. 
9. Build Model (Few Models are considered)
 * Simple CNN (Convolutional Neural Network)
 * Sequential CNN VGG style with 2 VGG block inception module architecture
 * Functional API CNN with inception architecture using BatchNormalization and Dropout
 * Use the Keras pretrained model. (VGG19)
 
The Model will be used to run the test data and record the validation.
A commentary for each step will be provided along with some visualization and summary through the process.  
in conclusion a summary commentary will be provided to discuss the challenges, weaknesses and opportunities for improvement in the models or the process.

![test](image/histogram.png)
