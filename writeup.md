## Deeplearning Project Writeup ##

**Follow Me Project**

>In this project, you will train a deep neural network to identify and track a target in simulation. So-called “follow me” applications like this are key to many fields of robotics and the very same techniques you apply here could be extended to scenarios like advanced cruise control in autonomous vehicles or human-robot collaboration in industry.

The goals of this project are the following:
* Understand the network architecture.
* Choose appropriate parameters of FCN
* Try 1 by 1 convolutions and fully connected layer
* Manipulate Images in accordance with Network Limitation
* Understand the limitation of the current network architecutre

[image1]: ./examples/model.png "model plot"

----
### Network Architecture ###

My Network consists of 3 x encoders and 3x decoders as a Fully-Convolutional Neural Network. In the encoder, I used Separable Convolutions and Batch Normalization to train the network faster. In the decoder, I used Bilinear Upsampling to realize transposed convolutions, and used Layer Concatenation to carry out Skip connections.

(model plot)
![alt text][image1]


### Choose Parameters ###

|  | Optimizer | Learning Rate | Batch Size | Number of Epochs | Steps per Epoch | Validation Steps per Epoch | Number of training Data |
|----|----|----|----|----|----|----|----|
| No.1 | Adam | 0.003 | 32 | | | | |
| No.2 | Adam | 0.002 | 32 | | | | | 
| No.3 | Adam | 0.0015| 32 | | | | |

* Optimizer (Adam & Nadam)
* Learning Rates




**Ideas for Improving your Score

Collect more data from the sim. Look at the predictions think about what the network is getting wrong, then collect data to counteract this. Or improve your network architecture and hyperparameters. 


