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

Gallery

After the initial analysis of the photos, it was decided to designate a total of 5 separate categories:<br/>
• '(0, 6)' - people up to the age of six, <br/>
• '(7, 20)' - people between the age of seven and twenty, <br/>
• '(21, 37)' - people between the age of twenty-first and thirty-seven, <br/>
• '(38, 59)' - people between thirty-eight and fifty-nine years of age, <br/>
• '(60+)' - people over sixty years of age.

The figure below shows five photos from each category.

![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure7.jpg)


Before further processing of the photographs, it was checked whether there were any damaged images in the initial set, the so-called "corrupted files". After importing the photos to Python, it was checked for duplicate photos, too. MD5 cryptographic algorithm was used to automatically detect duplicates in the dataset.
In the next step, it was decided to examine the resolution of photos and then select one optimal size. The following figure shows the combinations of the width and height of each image.

<p align="center">
  <img src="https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure5.jpg" />
</p>


<p align="center">![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure5.jpg)</p>





![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure3.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure4.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure5.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure6.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure7.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure8.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure9.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure10.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure11.jpg)
![alt text](https://github.com/MaciejPyra/Human_Age_Recognition/blob/main/Figures/figure12.jpg)
