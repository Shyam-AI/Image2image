# image2image
# Task : Building a full scale image to image translation. Engaged in the developmenet of generating colour image from black and white (gray scale image) .
# Dataset : 
           coco dataset
# Idea : 
       # 1.Convert the coco dataset(colour) to LAB - to use as input for our model:
            In our setting, the generator model takes a grayscale image (1-channel image) and produces a 2-channel image, a channel for *a and another for *b. 
            The discriminator, takes these two produced channels and concatenates them with the input grayscale image and decides whether this new 3-channel image is fake or real.
            
            # Reason : Using the above mentioned technique, we were able to reduce the number of trainable parameters as  the model has to only learn A and B channel, 
                       thus reducing the model size. 
 # Project flow diagram (Architecture)
 
<img src="https://github.com/Shyam-AI/image2image/blob/main/images/color_gans.png" width="800px" height="auto">

# Loading the data using fastai api
          For any training and validating GAns we have to input a large amount of  dataset . For this specific application we have to input image dataset .

           Dataset can be :

           i) Custom dataset(over own images)

           ii) Benchmark dataset ( these are the dataset which are available open source )

           Note : for our application we have used coco dataset (also tested on ImageNet dataset).
                      
# Building the generator
            Here we are using unet over pretrained resnet-34 .
           Input : The generator takes L channel as the input which is the grayscale image .
           Output : The output from the generator is ab channel.
           
# Discriminator - Patch Discriminator
           The main task of the discriminator :
           Classifies between real or fake image.
           Here in PatchDiscriminator gives the classification for every patch.
           
# Generator training :
           Instead of training generator and discriminator together .

           We try to train our generator first and then have the adversial learning between generator and discriminator.
          

           The trained generator model is saved in .pt format so that it can be used while training the whole model.
# Main model training :
           Defined a training function .

           Note : In training visualization function is also called so that output images during the training can be viewed. During training of the entire model the trained                         generator model is loaded .
           
           After training the entire model the trained model is saved .pt    format so that it can be downloaded and loaded into our own application and can predict on the input              image by the user.
           
# Saving model
           Trained generator model and main model is saved in .pt format.

# Prediction
           Prediction Using the our trained model to predict on any image.
           Built a web app using streamLit.
# Findings:
           Instead of just adversial learning what we found was if we could pre-train the generator and then train it along with discriminator made massive difference in the quality of output we got from the generator. Used a pretrained ResNet18 as the backbone of  U-Net and to accomplish the second stage of pretraining, we are going to train the U-Net on our training set with only L1 Loss. Then we will move to the combined adversarial and L1 loss.
