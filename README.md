# Dog Breed Identification
## Farhad Navid 

### Purpose

The goal of this analysis is to explore various techniques to improve the prediction performance of one of the Kaggle challenges **“Dog Breed Identification.”**  Why this challenge? The author is fascinated by a large number of classes on this challenge, the limited amount of training data per class, and the inherent computational challenges it brings.

### Proposal

Two main approaches considered for this problem.  
 * Image Augmentation to increase the number of inputs.  
 * Use of  ImageNet pre-trained model. 
 
The prediction performance of the model required the use of Support Vector Machine (SVM) for this classification problem.  Due to the size of the data set and model feature size, it required to employ the use of GPU and for that, the author selected to use the AWS ecosystem. 

**Note** 
Due to the size of the train data set and the model features it was necessary to separate the notebooks. 
**Files**
 1. **DB_EDA.jpynb** ===================>This file performs the normal EDA type analysis on the data set.
 2. **Data_Prep.jpynb** =================>This file does the data preparation for the analysis including the augmentation. 
 3. **ModelVGG.jpynb** =================>This file contains the CNN Models models used.
 4. **Transfer_Learning_org.jpynb** ========>This file contains the pretrain VGG19 with original train data.
 5. **Transfer_Learning_aug.jpynb** ========>This file contains the pretrain VGG19 with Augmented train datae.
 6. **ReadMe.md** =====================>The read me file for the repository. 
 7. **Licenses** ========================>The MIT license file
 8. **Document.doc** ===================>This document has instruction on creating AWS instance and loading up the files and datasets to AWS EBS system. Please note these are some points I came across and I hope you find it helpful.
   
## Data set
* Number of classes (Dog Breeds): **120**
* Number of images: **10222** Training data 
* Image Size Varies 
* Augmented training data **51110**. 

### Distribution of the classes

**Top 10 Histogram**|**Last 10 Histogram**
:---:|:---:
![file3](https://github.com/Farhad-n/Clasification/blob/master/image/Top10_Bar.png)| ![file4](https://github.com/Farhad-n/Clasification/blob/master/image/Tail10_bar.png)

### Overall Distribution. 

The average per class is about **85 sample**.  This plot does show the unbalance nature of the data set.  

![file7](https://github.com/Farhad-n/Clasification/blob/master/image/histigram.png)

### Distribution of image Height and Width
**Average Height and Width ( 387, 443)**
Image Height Histogram| Image Width Histogram
:---:|:---:
![file5](https://github.com/Farhad-n/Clasification/blob/master/image/hist_height.png)| ![file6](https://github.com/Farhad-n/Clasification/blob/master/image/hist_width.png)

### Analysis

The pre-train model from ImageNet required image sizes of  **(224 X 224)**; therefore the training dataset was resized. Initially, the VGG19 “block4_pool” features were considered for processing the training dataset. The number of features of “block4_pool” with the shape of (, 14,14,512) puts the total number of the features to 100352 and with the original train dataset size (10222, 224,224,3) created a dataset too large for the selected tools.  Later on, it was decided to use the “fc2” layer (last layer) from VGG19 which had a much smaller number of features (, 4096) a more reasonable task for execution.

Accuracy, Cohen’s Kapp, F1 score, and classification report were selected to compare the result of experiments between the original train dataset and Augmented data set. 

### Result
Performance Summary
:---:
![file15](https://github.com/Farhad-n/Clasification/blob/master/image/SVM_res.png)

The result in the table is from minimally turned SVM predictor with the kernel=’rbf’ and c=1000.  Tuning included comparing the result of the various setting, The kernel =[’linear’ , ‘rbf’]  and "C"=[0.001, 0.1, 1, 10, 1000]. Additional parameter tuning can further improve the performance of the original data set.  However, since the result with the above tuning showed significant improvement over the CNN model prediction result, no further tuning was performed (Accuracy of 76%).

Please note the extreme overfitting observed in the CNN models is due to minimal hyperparameter tuning after re-sizing the training images (224 X 224). The initial CNN models were tuned for the image size of (100X 100). Also, we reduced the number of parameters in the models for computational efficiency. Following are the result of the models.  

**Functional API W Inception** | **CNN W 2 VGG Layer**
:---:|:---:
![file16](https://github.com/Farhad-n/Clasification/blob/master/image/Incp.png)| ![file17](https://github.com/Farhad-n/Clasification/blob/master/image/VGG.png)

Since the gap in the performance between the prediction of the CNN models and the SVM was large, the CNN tuning deemed unnecessary  (76% vs. 14% best case).  

Additionally, the result of the augmented dataset with the default parameter for the SVM showed further improvement in performance scores (over 20%). The training dataset size between the augmented data set to the original data set (25000 vs. 10222) difference is the only contributing factor for increase in the performance.
 
**SVM Classification report Summary**
:---:
![file14](https://github.com/Farhad-n/Clasification/blob/master/image/SVM_class_rpt.png)

### Project Retrospective

This project turned out to be a great learning experience in every step of the way and loosely followed the planned project timeline. This project leads to what felt like several smaller projects. In the end, we used AWS EC2 instances for utilizing GPU for processing the data and running the models instead of SageMaker3. Also, we end up using the “fc2” block for the pre-trained model instead of “block4_pool”. Also, utilized Keras augmentation technics for the image augmentation.  Furthermore, only some hyperparameter tuning was performed on the models due to time constraint. 

Learning about the memory and resource management for the massive datasets is a worthy goal and skill set for the aspiring data scientist. 

Next, would be interested to gain additional knowledge on memory and resource management and try using the various pre-trained models from ImageNet and run additional experiments to identify the minimum number of required for augmented data. 

### 
Confusion Matrix
:---:
![file7](https://github.com/Farhad-n/Clasification/blob/master/image/Con_mtx.png)

