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
Optimizer   [Adam   vs   Nadam]   and   Learning   Rates
At first, I used the Adam Optimizer for a few trials with a small learning rate as suggested in the lessons. A high learning rate might overshoot the desired output but a small learning rate might take too long to reach the destination. Also a small learning rate could get it stuck at a local minimum. I shifted to Nadam which is an Adam Optimizer with Nesterov Momentum which was suggested in a discussion on Slack. Momentum makes it converge more quickly and actually increased the score from about 31 to 41 with no other changes. I used the recommended learning rate of 0.002 for Nadam.
source:
https://www.quora.com/What-is-an-intuitive-explanation-of-momentum-in-training-neural-networks https://keras.io/optimizers/#nadam
Batch   Size
Computing   the   gradient   over   the   entire   dataset   is   expensive   and   slow.   This   is   why   we   use   batches.   I   chose   a   size   of   40.
It   is   said   that:
1. This   is   usually   32-   512   data   points.
2. In terms of computational power, while the single-sample stochastic GD process takes many many more
iterations,   you   end   up   getting   there   for   less   cost   than   the   full   batch   mode,   "typically."
3. Optimizing   the   exact   size   of   the   mini-batch   you   should   use   is   generally   left   to   trial   and   error.
4. It has been observed in practice that when using a larger batch there is a significant degradation in the quality
of the model, as measured by its ability to generalize. The lack of generalization ability is due to the fact that
large-batch   methods   tend   to   converge   to   sharp   minimizers   of   the   training   function.
5. Batch size and learning rate are said to be linked.  If the batch size is too small then the gradients will become
more   unstable   and   would   need   to   reduce   the   learning   rate.
source:    https://stats.stackexchange.com/questions/164876/tradeoff-batch-size-vs-number-of-iterations-to-train-a-neural-network/236393
Number   of   epochs,   Steps   per   epoch,   and   Validation   Steps   per   epoch
Number   of   Epoch
This is the total number of iterations on the same data. A large number of epoch might overfit your data while a small number   of   epoch   might   underfit   your   data.
Steps   per   epoch:
The number of steps (batches of samples) before declaring your epoch finished. This should be the number of training images   over   batch   size   because   you   should   theoretically   train   your   entire   data   on   very   epoch.
Validation   Steps   per   epoch:
This   should   be   number   of   validation   images   over   batch   size   because   you   should   test   all   your   data   on   every   epoch



**Ideas for Improving your Score

Collect more data from the sim. Look at the predictions think about what the network is getting wrong, then collect data to counteract this. Or improve your network architecture and hyperparameters. 


