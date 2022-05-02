# Face recognition

The aim of the project was the practical implementation of convolutional neural networks and maximizing the accuracy of their classification in terms of recognizing the age range to which the analyzed people belong. My task was to build the model which would provide reliable indication for assigning individual images of faces to appropriate age groups.

Please note that repo code includes not only final models but also procedding steps like a try to understand the whole dataset, image preprocessing and data normalization. Aditionally, there was a comprehensive analysis of the best model in terms of classification accuracy and its potential problems with specific category discrimination.


# Table of Contents

  * [Introduction](#intro)
     * [Why convolutional neural network?](#intro1)
     * [Data Source](#intro2)
     * [Technology Stack](#intro3)
  * [Image Preprocessing](#desc)
     * [Categorization](#desc1)
     * [Image Resizing](#desc2)
     * [Pixel Normalization](#desc3)
  * [Model Building](#usage)
  * [Evaluation of the best model](#optim)
     * [Architecture](#optim1)
     * [Training Process](#optim2)
     * [Classification Heatmap](#optim3)
     * [Classification Mistakes](#optim4)


<a name="intro"></a>
<a name="intro1"></a>
## Intorduction
### Why convolutional neural network?

Why not just waste a couple of weeks of your life creating a deep learning project using ConvNets :sweat_smile:? Seriously, this was a great opportunity to immerse into very interesting world of convolutional neural networks, problems related to choice of optimal network topology, regularization and image classification. <br/>
Relatively recently it has turned out that models based on convolutional neural networks can effectively compete with traditional algorithms such as logistic regressions, decision trees or random forests, especially in the context of very fast development of computers and multiplication of their potential computing power. What is important ConvNets allow to increase accuracy in complex problems which have been so far underperformed, in particular in terms of   image classification and face recognition.

<a name="intro2"></a>
### Data Source
Data was collected by Eran Eidinger, Roee Enbar and Tal Hassner and was presented in the paper "Age and Gender Estimation of Unfiltered Faces" (Institute of Electrical and Electronics Engineers, Princeton University, New York, 2013). The authors collected slighty more than 20 000 photos taken with the iPhone 5 or its newer model. The photos were uploaded by users on various social networks.

<a name="intro3"></a>
### Technology Stack
* Python,
* DS/ML frameworks -> NumPy, pandas, Matplotlib, seaborn, scikit-learn, TensorFlow.


<a name="desc"></a>
## Image Preprocessing

<a name="desc1"></a>
### Categorization
The authors of a dataset decided to designate 10 different age categories. However, after the initial analysis of the photos and based on the respective group sizes, it was decided to designate a total of 5 separate categories:<br/>
• category 0 -> '(0, 6)' - people up to the age of six, <br/>
• category 1 -> '(7, 20)' - people between the age of seven and twenty, <br/>
• category 2 -> '(21, 37)' - people between the age of twenty-first and thirty-seven, <br/>
• category 3 -> '(38, 59)' - people between thirty-eight and fifty-nine years of age, <br/>
• category 4 -> '(60+)' - people over sixty years of age.

The figure below shows five photos from each category.

<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure7.jpg" />
</p>


Before further processing of the photographs, it was checked whether there were any damaged images in the initial set, the so-called "corrupted files". After importing the photos to Python, it was checked for duplicate photos, too. MD5 cryptographic algorithm was used to automatically detect duplicates in the dataset.

<a name="desc2"></a>
### Image Resizing
In the next step, it was decided to examine the resolution of photos and then select one optimal size. The following figure shows the combinations of the width and height of each image.

<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure5.jpg" />
</p>


The "zero padding" method was used to align the aspect ratio of the images to a value of 1. For each photo, its width was compared with its height and then made equal by adding zero pixels to the smaller value on both sides of the photo (left and right for width or top and bottom for height). A pixel with a value of zero on the RGB scale was assigned a black color.

There are two examples of how zero padding can be used in practice. In the first line zero value pixels were added to the left and right side of the image to increase the width of the photo which aspect ratio was 0.79. In turn, the second line shows the modification of the image height by zero padding above and below it. The aspect ratio in this case was equal to 1.19. Finally, the format of both modified photos was equal to 1.


<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure6.jpg" />
</p>

Following the chart above, the final size value turned out to be 256x256 pixels. Then, by means of interpolation, all images were reduced to the above benchmark.

<a name="desc3"></a>
### Pixel Normalization
Subsequently, the pixel values of photos were normalized. The pixel values in each image turned to be integers in the range <0, 255>.

<a name="usage"></a>
## Model Building

Due to the non-linearity of convolutional neural networks it was difficult to construct a topology that would immediately give good results, especially in terms of image recognition. The only effective way was through trial and error method, a heuristic approach that did not guarantee obtaining the best model but brought us at least closer to a suboptimal solution.

A total of over 60 models were built. The following steps were made to choose the best network architecture and regularization technique, if nedeed: 
* basic models with a different number of convolutional layers, the number of kernels and the number of dense layers and respectively neurons in such layers. Selected topologies were tested on various combinations of hyperparameters, for example changing learning rate and batch size.
* regularized models including Dropout, Weight Constraint, Batch Normalization and Weight Decay. The mentioned regularization techniques were used both separately and in conjunction with each other. Similar to the basic models various combinations of hyperparameters were implemented.

<a name="optim"></a>
## Evaluation of the best model

<a name="optim1"></a>
### Achitecture
According to the modeling results presented in the previous chapter model with five convolution layers, each respectively with 16, 16, 32, 32 and 64 filters, was selected as the best and guaranteeing the highest classification accuracy on the validation set. Additionally, the value of the padding parameter was defined as "same" for the first 3 layers and "valid" for the next two ones. Pooling occurred after each layer. Further in the topology, there were three dense layers with 256, 128 and 5 neurons each.    

The figure below shows a graphic illustration of that architecture. The dimensions of the tensor that is passed through the network are also specified on each layer.


<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/Final_Topology_full.jpg" />
</p>

<a name="optim2"></a>
### Training Process
In order to present the network training process a graph showing the accuracy of ConvNet classification in relation to the training epoch was generated. The chart below shows two lines: the blue one indicating the learning progress on the training set and the red one symbolizing the validation set. In addition, the yellow color accentuates the space known as the model overfitting.



<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure8.jpg" />
</p>


At a later stage of the work, using the above model, the classification of photos from the test set was performed in order to assess and verify the predictive power of the analyzed network. A value of 70.37% was achieved. Taking into account the fact that the photographs reproduced the reality in which we live - a very limited, unbalanced set and the rawness of images - final result is relatively satisfying. Face recognition is a very complex problem especially regarding unstable face position, various-lengthened poses, non-schematic facial expressions and uneven lighting of images.

<a name="optim3"></a>
### Classification Heatmap
A heatmap showing a specific number of predicted classifications to individual categories depending on their true class was generated and presented below.

<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure9.jpg" />
</p>


In case of category 0 the final model rarely makes mistakes and if it does, it identifies faces as class 1, confusing children most often with the upper age range. 

ConvNet has difficulties distinguishing between catagories 1 and 2. This is especially true for adolescents who in most cases resemble people in the 21-37 age group. Interestingly, the problem mainly exists for photos tagged as images of women, possibly due to the presence of make-up that highlights the characteristics of older people while hiding the natural shapes seen in the 7-20 year old age group.

As expected, the model has many dilemmas with faces from category 2. Already as part of the dataset exploration, it was noticed that the faces of people in the lower limit of the 21-37 age range may be confused with class 1 and those in the upper limit do not differ much from people in category 3, i.e. 38-59 years old. What is particularly important, in contrast to other categories, the 21-37 age group is very diverse, many faces are characterized by unconventionality which makes it difficult to classify them correctly. 

The same conclusion was made for category 3 with the assumption that faces were expected to be misclassified as 21-37 and 60+, in particular.

When it comes to category 4, you can see a large randomness of the classification. As expected, the model makes a lot of mistakes in identifying seniors as people aged 38-59. On the other hand, such a significant percentage of forecasts of assigning them to categories 1 and 2 was surprising. This is probably related to the problem of an unbalanced dataset in which there were very few photos of seniors which ultimately resulted in the network's inability to learn the unique characteristics of the above group.

<a name="optim4"></a>
### Classification Mistakes
The figures below show examples of incorrect classifications for individual categories, along with a brief commentary and an attempt to identify the cause of errors.

<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure10.jpg" />
</p>


It was noticed that the model has a problem with black people and Asians for whose number of photos in the training set is very limited. In addition, many photos are blurry, fuzzy or underexposed. There are also cases of including items unusual for this category in the photo such as sunglasses that distinguish the elderly.


<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure13.JPG" />
</p>


The real problem of category 1 is the great similarity between teenagers and people aged 21-25, less often the middle-aged ones. As in class 0, the model has a lot of difficulties in classifying non-white people.


<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure15.JPG" />
</p>


Interestingly, it was noted that ConvNet learned to classify people with a bicycle helmet into Category 4. This is an obvious error due to the rare occurrence of such pictures in other classes in the training set.


<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure17.JPG" />
</p>


Verifying the results, it turned out that the network may have problems with cases of images with two faces, classifying the main face as a person with a side face.


<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure19.JPG" />
</p>


In addition to the small number of pictures of pensioners in the training set, it may also be influenced by the illusory nature of many pictures - people who have just turned 60 years of age often do not look like seniors yet and are included in other age groups.

