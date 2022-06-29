# Memoji-coversion

## Introduction

<p class="text-justify"> Facial expression for emotion detection has always been an easy task for humans, but achieving
the same task with a computer algorithm is quite challenging. With the recent advancement
in computer vision and machine learning, it is possible to detect emotions from images. Computer
algorithms are very sophisticated. Intelligent human-computer interaction is a new field
aimed at enabling people to use computers naturally as tools. It is claimed that human communication
skills are required for computers to interact with humans. One of these skills is the
ability to understand a person’s emotional state. Therefore a utility that detects emotion from
facial expressions would be widely applicable. Such an advancement could bring applications
in medicine, marketing and entertainment. </p>

## Objectives

i. To develop a CNN model for detecting facial expressions to classify them into seven emotions
like Angry, Disgust, Fear, Happy, Sad, Surprise and Neutral.

ii. To develop a website that can convert facial expressions to personalised memoji’s
at real time using Facecam.

## Problem statement

To develop a website to convert facial expression to memoji in real time.

## Application in Societal Context

i. Website can be used to create personalized memoji.

ii. Can be used to generate animated face for videos.

iii. Memoji is used to create NFT images as the profile pictures.


## Block diagram

<p align="center">
  <img src="https://user-images.githubusercontent.com/63513035/176335965-d2e9bfa8-f8a0-4a3d-9e0f-c439ca5a2f62.png">
</p>
<p align="center">
    Fig 1.0
</p>

After the input is fed in the form of image, the background is removed so that it cannot
compromise or reduce the prediction accuracy. So, the proposed system works on two level 
of CNN framework. The first level removes the background and the second level extracts the
primary expression vector (EV). The EV is generated by tracking down the relevant facial
points of importance. Each layer consists of 4 filters. These filters detect the shapes, edges,
texture and objects. The first layer uses edge, circle , corner detector filter to detect the face
while the second layer catches the eyes, lips, ears, nose etc. Above mentioned technique is
based on FACS(Facial Action Coding System) which leverages the relevant facial points to
detect the human emotion instead of wearing sophisticated sensors.

## Implementation

### Dataset

The dataset used in this project is the FER-2013 dataset. The dataset contains approximately
30000 facial RGB images. The images are restricted for 48*48 pixels. The main
labels of the images are divided into Angry, Disgust, Fear, Happy, Sad, Surprise and Neutral.
All these categories have about 4500 images. This dataset is the standard dataset across
the academia for facial recognition related projects. 0=Angry, 1=Disgust, 2=Fear, 3=Happy,
4=Sad, 5=Surprise, 6=Neutral are the labels of the dataset.


### Facial Action Coding System (FACS)

FACS is an anatomically based coding system that allows for the differentiation of expressions
that are closely similar. FACS splits the face into two sections: upper and lower and further
subdivides motion into action units (AUs). AUs are the unit of measurement between the
muscle movements that combine to produce expressions.The face tracking point is used to
constrain the image region to process and the color probability distribution, both computed
in the initialization step, is used to calculate the probability of a face pixel being skin so that
“skin mask” of the user’s face can be created. Using this mask the system can detect, as a
result of their nonskin-color property, the user’s eyebrows, eyes and mouth bounding boxes
and due to their position related to the face tracking point, the system can label the zones.
One problem can appear if the user has got his eyes a little bit sunk, then due to the shadow
in the eyelid, most probably the eyebrow and eye will be found as a single blob. In that case,
we divide this bounding box assuming that the eyebrow has been detected together with the
eye. Finally, from the bounding boxes positions, 10 face features are extracted. These 10
feature points of the face will later allow us to analyze the evolution of the face parameters
(distances and angles) used for expression recognition. Figure shows how FACS divides
the input human images into different EV or expression vectors.

![image](https://user-images.githubusercontent.com/63513035/176341854-23cea971-403f-4a13-b478-e89c6a9e2be6.png)

<p align="center">
    Fig 1.1
</p>

### CNN Model Building

The CNN Model implemented consists of 5 convolutional layers followed by a dense fully
connected layer. For each layer the kernel size used is 3 x 3 pixels and max pooling of 2 x
2 after each layer. The activation function used is ReLU. There is one Dense layer with 200
neurons. The last output layer consists of 7 neurons corresponding to 7 emotions.

![image](https://user-images.githubusercontent.com/63513035/176341964-dca9c2e3-8458-46aa-9e3b-50fdaae80b6e.png)

<p align="center">
    Fig 1.2
</p>

While implementing the CNN model we made use of the FACS method.The implemented
architecture consist of 5 convolutional layers.The first layer consists of 32 filters with kernel
size of 3*3 filters. In the second and third layer the number of filters are increased to 64 filters
with the kernel size of 3*3 filters. The fourth and fifth layer the number of filters are increased
to 128 filters with the kernel size of 3*3 filters. The activation function used is ReLu. Since
it increases the non-linearity in our input images and preserves lot of non-linear features like
the colours, transition b/w the features etc. The max-pooling of 2*2 is done to convert 3d
features to 2d features and then a dense layer of 200 nodes is implemented. The last layer
consist of 7 layers which is equal to the number of emotions to be predicted. After training
the model it gave an accuracy of 82.41% over 30 epochs. Later we saved the model in hdf5
format.

### Creating Memoji's

Here we are making use of the python module named ‘python-avatars’. There are many
attributes provided like skin colour, hair colour, clothing colour, hair style, clothing style,
facial hair style, accessories etc. With the help of these attributes combinations we can create different avatars which can
be later used as an memoji for the GUI part.

### GUI using Django as Framework

Django is a high-level python web framework and with the help of this we can develop secure
and maintainable websites in an efficient manner. It has many built-in python libraries which
makes it suitable for both frontend and backend.
Here we created html forms which takes all the inputs which are connected to the attributes
for creating the memoji. Once the inputs are submitted, all those corresponding attributes are
used and an avatar with .png file extension is created. The emotion prediction part from the
module 1 and the avatar generation part from module 2 are integrated.
Now, here the CNN model keep on detecting the emotions and when we click on the
generate memoji button the emotion at that point of time is converted to memoji. Below is the
first page which is common for both genders.

![image](https://user-images.githubusercontent.com/63513035/176342472-d9fbc172-34a5-42ee-8c24-ff05d0a5c0e1.png)

<p align="center">
    Fig 1.3
</p>

Now, based on the gender you select the respective attribute and their values will be
loaded. Figure 1.4, 1.5, 1.6 shows different attributes based on gender selection. If you choose
Male as the gender. Figure 1.4, 1.5, 1.6 shows different attributes like skin colour, clothing
colour, hair colour, clothing type, facial hair type and accessories respectively.

![image](https://user-images.githubusercontent.com/63513035/176342853-4d8f25a6-026e-4244-8bba-9bb827a382ee.png)

<p align="center">
    Fig 1.4
</p>


![image](https://user-images.githubusercontent.com/63513035/176342870-d16fd843-3b47-449f-895e-f46a438161b9.png)

<p align="center">
    Fig 1.5
</p>


![image](https://user-images.githubusercontent.com/63513035/176342889-29a55d12-ad1b-4ca0-96ac-65294ccf0720.png)

<p align="center">
    Fig 1.6
</p>


After selecting the attributes the camera turns on and user can look at the camera.

![image](https://user-images.githubusercontent.com/63513035/176342939-b5b16140-3588-4414-80fd-e2e68469bcde.png)

<p align="center">
    Fig 1.7
</p>

## Results

In the website, firstly the option for selecting the gender is given and then the attributes are
chosen, and after choosing the attributes there is option for capturing the image, and the emotion
of the person is detected and converted into memoji and that memoji gets downloaded

![image](https://user-images.githubusercontent.com/63513035/176343968-34d7903a-1073-46af-895c-e47877c0cd7c.png)

<p align="center">
    Fig 1.8: Emotion detecting happy face and the corresponding memoji
</p>


![image](https://user-images.githubusercontent.com/63513035/176344041-89517cb7-526c-4a3f-a655-e5a5f31f0b58.png)

<p align="center">
    Fig 1.9: Emotion detecting neutral face and the corresponding memoji
</p>

## Conclusion

This project implements a simple and effective system for real-time face emotion recognition.
Wearable detectors are frequently used in other techniques. The designed solution is based
on a low-cost web camera. The feature extraction technology employed enables for dynamic
classification of human facial expression emotions and production of personalised memoji in real
time based on the user’s preferences utilising various variables. With an accuracy rate of 82.41%, 
the model produced good results. Future work could include evaluating the performance
of our architecture on various data sets by taking training and testing samples from diverse data
sets. Furthermore, memojis can be utilised with more customised elements like as accessories,
special attire.NFTs (Non Fungible Tokens) can be utilised as a type of transaction in virtual
worlds such as META. Additionally, by improving camera quality and hardware capability, the
current system can be improved to forecast with greater accuracy while still using the existing
architecture.








