# Human_Age_Recognition

The aim of the project was the practical implementation of convolutional neural networks and maximizing the accuracy of their classification in terms of recognizing the age range to which the analyzed people belong. My task was to build the model which would provide reliable indication for assigning individual images of faces to appropriate age groups.


Please note that repo code includes not only final models but also procedding steps like try to understand the whole dataset, image preprocessing and data normalization. Aditionally, there was a comprehensive analysis of the best model in terms of classification accuracy and its potential problems with specific category discrimination.

Data collected by Eran Eidinger, Roee Enbar and Tal Hassner presented in the work "Age and Gender Estimation of Unfiltered Faces" (Institute of Electrical and Electronics Engineers, Princeton University, New York, 2013), was used. The authors collected photos taken with the iPhone 5 or its newer model. The photos were uploaded by users on social networks.

WHY?

WHY NOT? Why not just waste a couple of weeks of your life creating a deep learning project, just to cover up your insecurities of how incompetent you are. Seriously, this was a great opportunity to immerse into very interesting world of convolutional neural networks, problems related to choice of optimal network topology, regularization and image classification. Thanks to ConvNets it was possible to increase model accuracy in ImageNet project from 72% in 2010 to 96% in 2015. 
It turned out that models based on convolutional neural networks can effectively compete with traditional algorithms such as logistic regressions, decision trees or random forests, especially in the context of very fast development of computers and multiple multiplication of their potential computing power. Therefore, I decided to implement the my own project relating to image classification and face recognition.


Stack
* Python
* DS/ML frameworks -> NumPy, pandas, Matplotlib, seaborn, scikit-learn, TensorFlow 

Image Preprocessing

After the initial analysis of the photos, it was decided to designate a total of 5 separate categories:<br/>
• '(0, 6)' - people up to the age of six, <br/>
• '(7, 20)' - people between the age of seven and twenty, <br/>
• '(21, 37)' - people between the age of twenty-first and thirty-seven, <br/>
• '(38, 59)' - people between thirty-eight and fifty-nine years of age, <br/>
• '(60+)' - people over sixty years of age.

The figure below shows five photos from each category.

<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure7.jpg" />
</p>


Before further processing of the photographs, it was checked whether there were any damaged images in the initial set, the so-called "corrupted files". After importing the photos to Python, it was checked for duplicate photos, too. MD5 cryptographic algorithm was used to automatically detect duplicates in the dataset.
In the next step, it was decided to examine the resolution of photos and then select one optimal size. The following figure shows the combinations of the width and height of each image.

<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure5.jpg" />
</p>


The "zero padding" method was used to align the aspect ratio of the images to a value of 1. For each photo, its width was compared with its height, and then made equal by adding zero pixels to the smaller value on both sides of the photo (left and right for width or top and bottom for height). A pixel with a value of zero on the RGB scale is assigned a black color.

There are two examples of how zero padding can be used in practice. In the first line, zero value pixels were added to the left and right of the image to increase the width of the photo, which aspect ratio was 0.79. In turn, the second line shows the modification of the image height by zero padding above and below the image. The aspect ratio in this case was equal to 1.19. Finally, the format of both modified photos was equal to 1.


<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure6.jpg" />
</p>

Following the chart above, the final size value turned out to be 256x256 pixels. Then, by means of interpolation, all images were reduced to the above benchmark.

Subsequently, the pixel values of photos were normalized. The pixel values in each image turned to be integers in the range <0, 255>.

Model Building

Due to the non-linearity of convolutional neural networks, it was difficult to construct a topology that would immediately give good results, especially in terms of image recognition. The only effective way was through trial and error method, a heuristic approach that did not guarantee obtaining the best model but brought us at least closer to a suboptimal solution.

A total of over 60 models were built. The following steps were made to choose the best network architecture and regularization technique, if nedeed: 
* basic models with a different number of convolutional networks, the number of kernels and the number of layers and resplectively neurons in deep layers. Selected topologies were tested on various combinations of hyperparameters, changing learning rate and batch size.
* regularized models including Dropout, Weight Constraint, Batch Normalization and Weight Decay. The mentioned regularization techniques were used both separately and in conjunction with each other. Similar to the basic models various combinations of hyperparameters were implemented.

Classification and evaluation of the best model

In accordance with the modeling results presented in the previous chapter, model with five convolution layers, each respectively with 16, 16, 32, 32 and 64 filters, was selected as the best and guaranteeing the highest classification accuracy on the validation set. Additionally, the value of the padding parameter was defined as "same" for the first 3 layers and "valid" for the next two. Pooling occurred after each layer. Later in the topology, three deep layers appeared, with 256, 128 and 5 neurons each.    

The figure below shows a graphic illustration of that architecture. The dimensions of the tensor that is passed through the network are also specified on each layer.


<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/Architektura_sieć_v2.jpg" />
</p>


In order to present the network training process, a graph showing the accuracy of ConvNet classification in relation to the epoch was generated. The chart below shows two lines, the blue one indicating the learning progress on the set training set and the red one symbolizing the validation set. In addition, the yellow color accentuates the space known as the model overfitting.



<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure8.jpg" />
</p>


At a later stage of the work, using the above model, the classification of photos from the test set was performed in order to assess and verify the predictive power of the analyzed network. A value of 70.37% was achieved. Taking into account the fact that the photographs reproduced the reality in which we live - a very limited and additionally unbalanced set and the rawness of images - final result is relatively satisfying. Face recognition is a very complex problem especially regarding unstable face position, various-lengthened poses, non-schematic facial expressions and uneven lighting of images.

A heatmap showing a specific number of predicted classifications to individual categories depending on their true class was generated and presented below.

<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure9.jpg" />
</p>




![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure9.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure5.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure6.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure7.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure8.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure9.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure10.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure11.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure12.jpg)
