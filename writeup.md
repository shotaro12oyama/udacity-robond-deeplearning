## Deeplearning Project Writeup ##

**Follow Me Project**

>In this project, you will train a deep neural network to identify and track a target in simulation. So-called “follow me” applications like this are key to many fields of robotics and the very same techniques you apply here could be extended to scenarios like advanced cruise control in autonomous vehicles or human-robot collaboration in industry.

The goals of this project are the following:
* Understand the network architecture.
* Choose appropriate parameters of FCN
* Try 1 by 1 convolutions and fully connected layer
* Manipulate Images in accordance with Network Limitation
* Understand the limitation of the current network architecutre

[image1]: ./example/model.png "model plot"
[image2]: ./example/segmentation_image.png "segmentation image"
[image3]: ./example/learning_history.png "learning history"


----
### Network Architecture ###

My Network consists of 3 x encoders and 3x decoders as a Fully-Convolutional Neural Network. In the encoder, I used Separable Convolutions and Batch Normalization to train the network faster. In the decoder, I used Bilinear Upsampling to realize transposed convolutions, and used Layer Concatenation to carry out Skip connections.

(model plot)
![alt text][image1]


#### 1 by 1 convolution layer and fully connected layer ####

1x1 convolution helped in reducing the dimensionality of the layer. A fully-connected layer of the same size would result in the same number of features. Also, replacement of fully-connected layers with convolutional layers presents an added advantage that during inference, images of any size can be fed into the trained network.

source: 
http://iamaaditya.github.io/2016/03/one-by-one-convolution/
https://classroom.udacity.com/nanodegrees/nd209/parts/c199593e-1e9a-4830-8e29-2c86f70f489e/modules/cac27683-d5f4-40b4-82ce-d708de8f5373/lessons/032b020f-7c02-46dc-9266-eaee3eb76eb7/concepts/7754d15f-28ca-47f9-9b20-19ae90581829


#### Encoding, Decoding and Skip connection ####

Encoder plays a role of classification by abstracting features from several window size. However, it does not preserve spatial information. By using 1 by 1 convlution, which is mentioned above, we can connect the output of encoder into decoder, which upscale the output of encoder to the original image size. Simultaneously, Skip connection can use information from multiple resolution scales, and can make the segmentation more precise.

source:
https://www.quora.com/What-is-an-Encoder-Decoder-in-Deep-Learning/answer/Christian-Baumgartner-3?srid=ison
https://classroom.udacity.com/nanodegrees/nd209/parts/c199593e-1e9a-4830-8e29-2c86f70f489e/modules/cac27683-d5f4-40b4-82ce-d708de8f5373/lessons/032b020f-7c02-46dc-9266-eaee3eb76eb7/concepts/f3e2bc90-1d30-4367-84d2-35d069ab5152


#### How the model can work well for another object ####

As the picture below, the model trained with the existing data detected human object only. If I need to recognize another object such as dog and cat, it seems that I should prepare the object data and train the networks with the data specifically.

![alt text][image2]


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

![alt text][image3]


### Future Enhancement ###
I should try to collect more data from the simulator. Also, I may be able to add more layer for encoder and decoder, in order to deal with more complicate model. Or, using max-pooling indices for upsampling like Segnet, i may get better performance.

source:
https://arxiv.org/pdf/1511.00561.pdf
