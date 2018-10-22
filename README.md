# Dog Breed Identification
## Farhad Navid 

### purpose

The goal of this analysis is to explore various techniques to improve the performance of one of the Kaggle challenges **“Dog Breed Identification.”**  Why this challenge? I am fascinated by a large number of classes on this challenge and the limited amount of training data per class.
### Proposal

I selected two main approaches to this problem.  
 * Image Augmentation to increase the number of inputs.  
 * Use a pre-trained model from ImageNet. 
 
The prediction performance of the model required the use of Support Vector Machine (SVM) for this classification problem.  Due to the size of the data set and features for the model needed to employ the use of GPU and for that, I have selected to use the AWS ecosystem. 

**Note** 
Due to size of the train data set and the model features it was necessary to separate out the notebooks. 

**Files**
 1. **DB_EDA.jpynb** ====================>This file performs the normal EDA type analysis on the data set.
 2. **Data_Prep.jpynb** =================>This file does the data preparation for the analysis including the augmentation. 
 3. **ModelVGG.jpynb** ==================>This file contains the CNN Models models used.
 4. **Transfer_Learning_org.jpynb** =====>This file contains the pretrain VGG19 with original train data.
 5. **Transfer_Learning_aug.jpynb** =====>This file contains the pretrain VGG19 with Augmented train datae.
 6. **ReadMe.md** =======================>The read me file for the repository. 
 7. **Licenses** ========================>The MIT license file
 8. **Document.doc** ====================>This document have instruction on creating AWS instance and loading up the files and datasets to AWS EBS system. please note these are some points I came across and I hope you find it helpful.
   
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

The training dataset was resized to **(224X 224)** since the required image size for the selected pre-train model was of that size. Initially, the VGG19 “blook4_pool” features were considered for processing the training dataset. The number of features of “blook4_pool” with the shape of (, 14,14,512) puts the total number of the features to 100352 and with the original train dataset size (10222, 224,224,3) created a dataset too large for the selected tools.  Later on, it was decided to use the “fc2” layer (last layer) from VGG19 which had a much smaller number of features (, 4096) a more reasonable task for execution.

Accuracy, Cohen’s Kapp, F1 score, and classification report were selected to compare the result of experiments between the original train dataset and Augmented data set. 

Image Origenal| Image Resized
:---:|:---:
![file10](https://github.com/Farhad-n/Clasification/blob/master/image/Img_org.png)| ![file11](https://github.com/Farhad-n/Clasification/blob/master/image/img_rescale.png)

### Result
Performance Summary
:---:
![file15](https://github.com/Farhad-n/Clasification/blob/master/image/SVM_res.png)

The result in the table is from minimally turned SVM predictor with the kernel=’rbf’ and c=1000.  Tuning included comparing the result of the various setting, The kernel =[’linear’ , ‘rbf’]  and "C"=[0.001, 0.1, 1, 10, 1000]. Additional parameter tuning can further improve the performance of the original data set.  However, since the result with the above tuning showed significant improvement over the CNN model prediction result, no further tuning was performed (Accuracy of 76%).

Please note minimal hyperparameter tuning performed after re-sizing the images (224X224). The initial CNN models were tuned for the image size of (100X 100). Also, we reduced the number of parameters in the models. Following are the result of the models.  
### incp.png and VGG.png
Functional API W Incption | CNN W 2 VGG Layer
:---:|:---:
![file16](https://github.com/Farhad-n/Clasification/blob/master/image/Incp.png)| ![file17](https://github.com/Farhad-n/Clasification/blob/master/image/VGG.png)

Since the gap in the performance between the prediction of the CNN models and prediction of the SVM was large, the CNN tuning deed unnecessary  (76% vs. 14% best case).  

Additionally, the result of the augmented dataset with the default parameter for the SVM showed further improvement in performance scores (over 20%). The only difference in the performance was the training data set size was 25000 vs. 10222.

### Performance result 

SVM Classification report Summary
:---:
![file14](https://github.com/Farhad-n/Clasification/blob/master/image/SVM_class_rpt.png)
### Confusion Matrix
:---:
![file7](https://github.com/Farhad-n/Clasification/blob/master/image/Con_mtx.png)
