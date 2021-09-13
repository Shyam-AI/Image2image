# image2image
# Task : Building a full scale image to image translation. Engaged in the developmenet of generating colour image from black and white (gray scale image) .
# Dataset : 
           coco dataset (also trained using custom image dataset)
# Idea : 
       # 1.Convert the coco dataset(colour) to LAB - to use as input for our model:
            In our setting, the generator model takes a grayscale image (1-channel image) and produces a 2-channel image, a channel for *a and another for *b. 
            The discriminator, takes these two produced channels and concatenates them with the input grayscale image and decides whether this new 3-channel image is fake or real.
            
            # Reason : Using the above mentioned technique, we were able to reduce the number of trainable parameters as we the model has to only learn A and B channel, 
                       thus reducing the model size. 
 # Project flow diagram (Architecture)
 
<img src="https://github.com/Shyam-AI/image2image/blob/main/images/color_gans.png" width="800px" height="auto">

# Findings:
           Instead of just adversial learning what we found was if we could pre-train the generator and then train it along with discriminator made massive difference in the quality of output we got from the generator. Used a pretrained ResNet18 as the backbone of  U-Net and to accomplish the second stage of pretraining, we are going to train the U-Net on our training set with only L1 Loss. Then we will move to the combined adversarial and L1 loss.
