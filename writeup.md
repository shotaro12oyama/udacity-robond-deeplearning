## Deeplearning Project Writeup ##

**Follow Me Project**

>In this project, you will train a deep neural network to identify and track a target in simulation. So-called “follow me” applications like this are key to many fields of robotics and the very same techniques you apply here could be extended to scenarios like advanced cruise control in autonomous vehicles or human-robot collaboration in industry.

The goals of this project are the following:
* Understand the network architecture.
* Choose appropriate parameters of FCN
* Try 1 by 1 convolutions and fully connected layer
* Manipulate Images in accordance with Network Limitation
* Understand the limitation of the current network architecutre

[image1]: ./code/model.png "model plot"
[image2]: ./code/learning_history.png "learning history"

----
### Network Architecture ###

My Network consists of 3 x encoders and 3x decoders as a Fully-Convolutional Neural Network. In the encoder, I used Separable Convolutions and Batch Normalization to train the network faster. In the decoder, I used Bilinear Upsampling to realize transposed convolutions, and used Layer Concatenation to carry out Skip connections.

(model plot)
![alt text][image1]


#### 1 by 1 convolution layer and fully connected layer ####

fully connected (FC) layer to a convolutional layer we gain some form of localization if we look at where we have more activations.The idea is that if we choose our new last conv layer to be big enough we will have this localization effect scaled up to our input image size.







source: https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_segmentation.html


#### Encoding and Decoding ####



### How the model can work well for another object ###


### Choose Parameters ###

|  | Optimizer | Learning Rate | Batch Size | Number of Epochs | Steps per Epoch | Score |
|----|----|----|----|----|----|----|
| No.1 | Adam | 0.0020 | 32 | 100 | 200 | 0.406 |
| No.2 | Adam | 0.0020 | 32 | 50  | 50  | 0.391 |
| No.3 | Adam | 0.0025 | 32 | 50  | 50  | 0.375 |
| No.4 | Adam | 0.0015 | 32 | 50  | 50  | 0.370 |

* Optimizer: I selected Adam Optimizer, which was relatively fast and good performance.
* Learning Rates: I selected 0.002 after testing several times with different values.
* Batch Size: I changed the size in the range of 32-64, but it did not affect a lot.
* Number of Epochs and Steps per Epoch: As I increased the sizes, the score was improved gradually.

![alt text][image2]


### Future Enhancement ###
I should try to collect more data from the simulator. Also, I may be able to add more layer for encoder and decoder, in order to deal with more complicate model.


