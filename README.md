# Dog Breed Identification
## Farhad Navid 

The goal of this analysis is to identify the various breed of dogs using Dog images provided in kaggle data set. 

This document is intended to go through the entire process and for each step breifly talk about lesson's learned and challenges faced. 

**One note due to size of the input files and parametes in it was dificult to fit everything in one notebook.  The files were seprated to reduce the memory usage. Following are he discrption for weach file.**  

**Files**
 1. **DB_EDA.jpynb** ====================>This file performs the normal EDA type analysis on the data set.
 2. **Data_Prep.jpynb** =================>This file does the data preparation for the analysis including the augmentation. 
 3. **ModelVGG.jpynb** ==================>This file contains the models we will use.
 4. **ModelIncp.jpynb** =================>This file contains the models we will use.
 5. **Transfer_Learning_org.jpynb** =====>This file contains the models we will use.
 6. **Transfer_Learning_aug.jpynb** =====>This file contains the models we will use.
 7. **ReadMe.md** =======================>The read me file for the repository. 
 8. **Licenses** ========================>The MIT license file
 9. **Document.doc** ====================>This document have instruction on creating AWS instance and loading up the files and datasets to AWS EBS system. please note these are some points I came across and I hope you find it helpful.

Following section is the step by step instruction    

**Steps:**
1. Initiate AWS E2 instance to run this project.
 * Upload the data files.
 * Unzip the data files.
 * Upload the jupyter notebook files. 
2. EDA, Examine some basic characteristic of the dataset, Histogram, file structure, dim, ...
3. Preprocess the images. resize and reshape i.e. All the picture having the same dimension. 
4. Create training data set X_train, y_train, Xtrain will have the images and Y_train will have the lable. 
5. Augment the data.  Need to add more images to the data set.   
 * Create 4X per image.  Rotate, Flip, zoom, shear, 
 * add the newly created images to the training set directory.
 * recreate the X_train and y_train NumPy array.
6. Create the X_test dataset this is test data set. 
7. Build Model (Few Models are considered)
 * Sequential CNN VGG style with 2 VGG block inception module architecture
 * Functional API CNN with inception architecture using BatchNormalization and Dropout
 * Use the Keras pretrained model. (VGG19) fc2 weights
 
The Model will be used to run the test data and record the validation.
A commentary for each step will be provided along with some visualization and summary through the process.  
in conclusion a summary commentary will be provided to discuss the challenges, weaknesses and opportunities for improvement in the models or the process.
## EDA
![file9](https://github.com/Farhad-n/Clasification/blob/master/image/top_10.png "Top 10 Row") ![file8](https://github.com/Farhad-n/Clasification/blob/master/image/tail_10.png "last 10 Row")

![file3](https://github.com/Farhad-n/Clasification/blob/master/image/top10_bar.png "Top 10 Hist") ![file4](https://github.com/Farhad-n/Clasification/blob/master/image/tail10_bar.png "last 10 RHist")

![file5](https://github.com/Farhad-n/Clasification/blob/master/image/hist_height.png "THistogram Heights") ![file6](https://github.com/Farhad-n/Clasification/blob/master/image/hist_width.png "Hitogram Weidths")

![file7](https://github.com/Farhad-n/Clasification/blob/master/image/Histogram.png)
