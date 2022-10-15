
# Convolutional Neural Networks Part 2


```python
from ipypublish import nb_setup
```

## Introduction



The previous chapter went over the basics of ConvNet design and implementation. In the current chapter we cover some advanced topics, including:

- Improvements made to the base ConvNet design in the last few years
- Brief descriptions of some important ConvNets, with particular emphasis on those whose pre-trained models are made available in Keras
- Visualization of filters and Activation Maps in ConvNets and techniques to run a ConvNet backwards to generate images. These are used probe the responses of individual neurons and thus gain some understanding of how these systems work and arrive at their decisions.
- Using ConvNets in other Image Processing tasks such as Object Localization and Detection, Semantic Categorization etc.

## Trends in ConvNet Design

The performance of ConvNets has improved in recent years due to several architectural changes, which include the following:

- Residual Connections
- Use of Small Filters
- Bottlenecking Layers
- Grouped Convolutions (also called Split-Transform-Merge)
- Depthwise Separable Convolutions
- Dispensing with the Pooling Layer
- Dispensing with Fully Connected Layers

Residual Connections are arguably the most important architectural enhancement made to ConvNets since their inception, and are covered in some detail in the following section. Even though proposed in the context of ConvNets, they are critical part of other Neural Network architectures, in particular Transformers.

### Residual Connections


```python
#convnet34
nb_setup.images_hconcat(["DL_images/convnet34.png"], width=700)
```




![png](output_7_0.png)



Residual connections are illustrated in Part (b) of Figure **convnet34**. They were introduced as part of the ResNet model in 2015 and were shown to lead to large improvement in model performance by making possible trainable models with hundreds of layers. Prior to the discovery of Residual Connections, models with more 20-30 layers ran into the Vanishing Gradient problem during training, due to the gradient dying out as it was subject to multiple matrix multiplication during Backprop. 

Part (a) of the figure shows a set of regular conolutional layers, Residual Connections feature a bypass connection from the input to the output such that the input signal is added to the output signal as shown in Part(b). This design clearly helps with gradient propagation, since the addition operation has the effect of taking the gradient at the output of the sub-network and propagating it without change to the input. The idea of Residual Connections is now widely used in DLN architectures, state of the art networks such DenseNet and Transformers include it as part of their design. We provide a deeper discussion of the benefits of Residual Connections in the section on ResNets later in this chapter.

### Small Filters in ConvNets


```python
#convnet11
nb_setup.images_hconcat(["DL_images/convnet11.png"], width=600)
```




![png](output_10_0.png)



s
As ConvNet architectures have matured, one of the features that has changed over time is the filter design. Early ConvNets such as AlexNet used large $7 \times 7$ Filters in the first convolutional layer. However, a stack of $3 \times 3$ Filters is a superior design to the single $7 \times 7$ Filter for the following reasons (see Figure **convnet11**)):

* The stacked $3 \times 3$ design uses a smaller number of parameters: Using the formula for number of parameters in a ConvNet developed in Section **SizingConvnets**, it follows that the $7 \times 7$ Filter uses $C \times (7 \times 7 \times C + 1)=49 C^2 + C$ parameters (since each Filter uses $7 \times 7 \times C + 1$ parameters, and there are C such Filters). In comparison the stacked $3 \times 3$ design uses a total of $3 \times C \times (3 \times 3 \times C + 1)=27 C^2 + 3C$ parameters, i.e., a 45% decrease.

* The stacked $3 \times 3$ design incorporates more non-linearity, it has 4 ReLU Layers vs the 2 ReLU Layers in the $7 \times 7$ case, which increases the system's modeling capacity.

* The stacked $3 \times 3$ design results in less computation.

The better performance with smaller filters can be explained as follows: The job of a filter is to capture patterns within the Local Receptive Field and patterns at a finer level of granularity can be captured with smaller filters. Also as we stack up the layers, filters at the deeper levels progressively capture patterns within larger areas of the image. For example consider the case of the stacked $3 \times 3$ Filters in Figure **convnet11**: While the first $3 \times 3$ Filter scans patches of size $3 \times 3$ in the input image, it can be easily seen that the second $3 \times 3$ filter effectively scans patches of size $5 \times 5$, and the third $3 \times 3$ Filter scans patches of size $7 \times 7$ in the input image. Hence even though the filter size is unchanged as we move deeper into the network, they are able to capture patterns in progressively larger sections of the input image. This is illustrated in Figure **convnet33** for the case of two layers of $3\times 3$ filters.


```python
#convnet33
nb_setup.images_hconcat(["DL_images/convnet33.png"], width=600)
```




![png](output_12_0.png)



### Bottlenecking using 1x1 Filters


```python
#cnn21
nb_setup.images_hconcat(["DL_images/cnn21.png"], width=600)
```




![png](output_14_0.png)



Several modern ConvNets use Filters of size $1\times 1$. At first glance these may not make sense, but note that because of the depth dimension, a $1\times 1$ Filter still involves a dot product with weights associated with the depth dimension and the corresponding activations across them. As shown in Figure **cnn21**, this can be used to compress the number of layers in a ConvNet. This operation called 'bottlenecking', is very useful and is frequently used in modern ConvNets to reduce the number of parameters or the number of operations required.


```python
#convnet12
nb_setup.images_hconcat(["DL_images/convnet12.png"], width=600)
```




![png](output_16_0.png)



Bottlenecking with $1 \times 1$ and $1 \times n$ filters, as illustrated in Figure **convnet12**: As shown, the first $1 \times 1$ filter is used in conjuction with a reduction in depth to $C/2$. The $3 \times 3$ filter then acts on this reduced depth layer, which gives us the reduction in parameters, and this is followed by another $1 \times 1$ filter that expands the depth back to $C$. It can the shown that this filter architecture reduces the number of parameters from $9 C^2$ to $3.25 C^2$ (ignoring the bias parameters). It can be easily shown that the number of computations also decreases from $9C^2 HW$ to $3.25C^2 HW$, where $H,W$ are the spatial dimensions of the ConvNet.

### Grouped Convolutions


```python
#convnet27
nb_setup.images_hconcat(["DL_images/convnet27.png"], width=800)
```




![png](output_19_0.png)



Grouped Convolutions are illustrated in Figure **convnet27**. As shown, the regular $3\times 3$ convolution is replaced by the following:

- Step 1: Compress the input layers using a $1\times 1$ convolution from 256 layers to 128.
- Step 2: Split the output of Step 1 into 32 separate convolution layers, such that each layer 4 Activation Maps.
- Step 3: Use regular $3\times 3$ convolution on each of the 32 layers
- Step 4: Marge or Concatenate all 32 convolution layers to form a structure with 128 Activation Maps
- Step 5: Expand the output of step 4 to 256 Activation Maps with a $1\times 1$ convolution

Grouped Convolutions have been shown to improve the performance of ConvNets. It is not completely clear how they are able to do so, but it has been observed that the 4 Activation Maps in the smaller Convolutional Layers learn features that have a high degree of correlation. For example AlexNet, which was one of the earliest ConvNets, featured 2 groups due to memory constraints, and it was shown that Group 1 learnt black and white shapes while Group 2 learnt colored shapes. This functions as akind of regularizer and helps the network learn better features.

It can also be shown that the number of computations for the Grouped case decreases in inverse proportion to the number of groups and the size of the filter. This calculation is carried out detail in the next section.

### Depthwise Separable Convolutions


```python
#convnet28
nb_setup.images_hconcat(["DL_images/convnet28.png"], width=900)
```




![png](output_22_0.png)



A standard convolution both filters and combines inputs into a new set of outputs in one step. The depthwise separable convolution splits this into two layers, a separate layer for filtering and a separate layer for combining. This factorization has the effect of drastically reducing computation and model size. Hence they take the idea behind Grouped Convolutions to the limit by splitting up the M Activation Maps in the input layer into M separate single layer Activation Maps as shown in Figure **convnet28**. Each of these Activation Maps is then processed using a separate convolutional filter, and then combined together at the output. A simple $1\times 1$ convolution, is then used to create a linear combination of the output of the depthwise layer . Hence this design serializes the spatial and depthwise filtering operations of a regular convolution. An immediate benefit of doing this is a reduction in the number of computations (and the number of parameters), as shown next:

- The number of computations in a regular convolution shown in Part (a) is given by $D_K D_K\times MN\times D_F D_F$ where $D_K$ is the size of the filter, M is the depth of the input layer, N is the depth of the output layer and $D_F$ is the size of the Activation Map.
- The number of computations in the Depthwise Separable Convolution is given by $D_K D_K\times M\times D_F D_F + MN\times D_F D_F$

It follows that the ratio $R$ between the number of computations in the Depthwise Separable network and the Regular COnvNet is given by

$$
R = {1\over N} + {1\over D_K^2}
$$

For a typical filter size of $D_K= 3$, it follows that the number of computations in the Depthwise Separable network reduces by a factor of 9, which can be a significant reduction for training times that sometimes run into days. The idea of separating out the filtering into two parts, spatial and depthwise, has subsequently proven to be very influential, and underlies the type of filtering in a new model called Transformers, which we will study in a later chapter.

Depthwise Separable Convolutions are supported in Keras usong the *SeparableConv2D* command that implements all the operations shown in Part (b) of the figure.

## ConvNet Architectures


```python
#convnet15
nb_setup.images_hconcat(["DL_images/convnet15.png"], width=600)
```




![png](output_25_0.png)



We briefly survey ConvNet architectures starting with the first ConvNet, LeNet5, whose details were published in 1998. Starting with AlexNet in 2012, ConvNets have won the ImageNet Large Scale Visual Recognition Challenge (ILSVRC) image classification competition run by the Artificial Vision group at Stanford University. ILSVRC is based on a subset of the ImageNet database that has more than 1+ million hand labeled images, classified into 1,000 object categories with roughly 1,000 images in each category. In all there are 1.2 million training images, 50K validation images and 150K testing images. If an image has multiple objects, then the system is allowed to output upto 5 of the most probably object categories, and as long as the the "ground-truth" is one of the 5 regardless of rank, the classification is deemed successful (this is referred to as the top-5 error rate).

Figure **convnet15** plots the top-5 error rate and (post-2010) the number of hidden layers in DLN architectures for the past seven years. Prior to 2012, the winning designs were based on traditional ML techniques using SVMs and Feature Extractors. In 2012 AlexNet won the competition, while bringing down the error rate signficantly, and inaugurated the modern era of Deep Learning. Since then, error rates have come down rapidly with each passing year, and currently stand at 3.57%, which is better than human-level classification performance. At the same time, the number of Hidden Layers has increased from the 8 layers used in AlexNet, to 152 layers in ResNet which was the winner in 2015. This is when the machines outpaced humans in accuracy and the competetion was stopped.

In this section our objective is to briefly describe the architecture of the winners from the last few years, namely: AlexNet (2012), ZFNet (2013), VGGNet (2014), Google InceptionNet (2014) and ResNet (2015). Note that VGGNet, InceptionNet and VGGNet are available as pre-trained models (on ImageNet) in Keras, for use in Transfer Learning. In addition we will go over a few other architectures whose pre-trained models are also included in Keras, namely XceptionNet, MobileNet, DenseNet and NASNet. The first three are "classical" ConvNet designs with multiple Convolutional, Pooling, and Dense layers arranged in a linear stack. The Google Inception Network and ResNet have diverged from some of the basic tenets of the first ConvNets, by adopting the Split/Transform/Merge and the Residual Connection designs respectively. In more recent years the focus has shifted towards coming up with ConvNets that have a much lower number of parameters, without sacrificing performance. The InceptionNet actually began this trend, and MobileNet also belongs to this category of models.

These following architectures are described in greater detail next:

- LeNet (1998)
- AlexNet (2012)
- ZFNet (2013)
- VGGNet (2014)
- InceptionNet (2014)
- ResNet (2015)
- Xception (2016)
- DenseNet (2017)
- MobileNet (2017)
- NasNet (2018)

The table below which is taken from Keras Documentation summarizes the size, performance, number of parameters and depth of these models. The performance is with respect to the ImageNet dataset, with the Top-1 Accuracy being the performance for the best predition and the Top-5 Accuracy being the performance for the case when the Ground Truth is among the top 5 predictions.


```python
#ConvNetPerformance
nb_setup.images_hconcat(["DL_images/convnet35.png"], width=600)
```




![png](output_27_0.png)



### LeNet5 (1998)

LeNet5 was the first ConvNet, it was designed by Yann LeCun and his team at Bell Labs, see [Lecun, Bottou, Bengio, Haffner (1998)](https://ieeexplore.ieee.org/document/726791). It had all the elements that one finds in a modern ConvNet, including Convolutional and Pooling Layers, along with the Backprop algorithm for training (Figure **LeNet5**)).  It only had two Convolutional layers, which was a reflection of the smaller training datsets and processing capabilities available at that time. LeCun et.al. used the system for handwritten signature detection in checks, and it was successfully deployed commercially for this purpose.


```python
#LeNet5
nb_setup.images_hconcat(["DL_images/LeNet5.png"], width=900)
```




![png](output_29_0.png)



As shown in Figure **LeNet5**, the system uses two Convolution layers with $5 \times 5$ Filters and Stride $S=1$, and two Pooling layers with $2 \times 2$ Filters and $S=2$. The system reduces the input $32 \times 32$ images into 16 Activation Maps of size $5 \times 5$ at the end of the second pooling operation, before flattening this tensor and outputting the result into the Fully Connected part of the design.


```python
#AlexNet
nb_setup.images_hconcat(["DL_images/AlexNet.png"], width=900)
```




![png](output_31_0.png)



### AlexNet (2012)

After the pioneering work done in LeNet5, progress in ConvNets lay dormant for more than a decade. It was held back by the following issue: In order to train larger ConvNets with millions of parameters, it was necessary to have a large training dataset with correspondingly millions of images (this is required in order to prevent overfitting, see Chapter **ImprovingModelGeneralization** for an explanation). Image datasets of this size did not exist until about 2010, when the ImageNet dataset was released.

AlexNet is responsible for the explosion in interest in DLNs in the last few years.This network won the ILSVRC competition in 2012 by a wide margin compared to its nearest rival which was based on SVMs (it had a 15.4% top-5 error rate vs 26.2% for the next lowest network), and this opened up the eyes of the ML community to the potential of DLNs. The architecture of AlexNet [Krizhevsky, Sutskever, Hinton (2012)](https://dl.acm.org/citation.cfm?id=2999134.2999257) was very similar to that of LeNet5, with the following exceptions (see Figure **AlexNet**)):

- AlexNet replaced the *tanh()* activation function used in LeNet5, with the ReLU function and also the MSE loss function with the Cross Entropy loss.

- AlexNet used a much bigger training set. Whereas LeNet5 was trained on the MNIST dataset with 50,000 images and 10 categories, AlexNet used a subset of the ImageNet dataset with a training set containing 1+ million images, from 1000 categories.

- AlexNet used Dropout regularization (= 0.5) to combat overfitting (but only in the Fully Connected Layers). It also used a Normalization Layer, that is no longer used in ConvNets since it does not improve the performance significantly.

AlexNet was able to use a training set which was larger by two orders of magnitude, without a corresponding increase in training time, by exploiting the power of GPUs. It used two GTX 580 GPUs for 5-6 days to complete the training phase. This was enabled by using a Grouped Convolution design (not shown in the above figure) with two groups, each running on its own GPU.

AlexNet used 5 Convolutional layers (vs 2 used in LeNet5), and it used a similar combination of Convolutional and Pooling Layers followed by 3 Dense Layers. The input into the system consisted of $224 \times 224 \times 3$ images, which are then processed by the first convolutional layer with 96 Activation Maps using $11 \times 11$ filters with $S=4, P=0$. The system has $4$ more Convolutional layers, consisting of a $5 \times 5$ Filter followed by three $3 \times 3$ Filters. The number of Activation Maps in the last Convolutional layer is increased to 256 before the activations are flattened and fed into the Fully Connected Layers.

AlexNet had a total of 60 million parameters, which was still much more than the number of training images available. In order to prevent overfitting, the system used Data Augmentation techniques to produce additional test images, thus boosting the Test dataset to 15 million images.

### ZFNet (2013)


```python
#zfnet
nb_setup.images_hconcat(["DL_images/zfnet.png"], width=600)
```




![png](output_34_0.png)



ZFNet, which was designed by [Zeiler and Fergus (2013)](https://arxiv.org/abs/1311.2901), won the ILSVRC competition in 2013 by achieving a 11.2% top-5 error rate. The architecture was essentially a tuning modification to AlexNet, with the following changes (Figure **zfnet**)):

- Use of $7\times 7$ instead of $11 \times 11$ Filters in the first Convolutional layer, 

- Use of a stride of $S=2$ instead of $S=4$.

The reduction in filter size and stride helped to pick image features at a finer level of resolution.

### VGGNet (2014)


```python
#VGGNet
nb_setup.images_hconcat(["DL_images/VGGNet.png"], width=600)
```




![png](output_37_0.png)



[Simonyan and Zisserman (2014)](http://arxiv.org/abs/1409.1556) created a network which reduced the top-5 ILSVRC error rate to 7.3% (Figure **VGGNet**)). The main innovations in the network, called VGGNet, are the following:

- VGGNet increased the number of layers to 19 layers (16 Convolutional + 3 Fully Connected), as opposed to the previous designs that were limited to 8 such layers.

- VGGNet considerably simplified the ConvNet design, by repeating the same smaller convolution filter configuration 16 times: All the filters in VGGNet were limited to $3 \times 3$, with stride and padding of 1, along with $2 \times 2$ maxpooling filters with stride of 2. Since these smaller filters are used in a series of 2 or 3 consecutive convolutional layers, the net effect is that of using a single $5 \times 5$ or $7 \times 7$ filter, but with the advantage of a smaller number of parameters and increased model non-linearity, as explained in Section **SmallFilters**.

An interesting fact about about VGGNet is that it has a total of 144 million parameters, *of which about 124 million parameters are used in the final 3 Dense layers*. This was a result of the Flatten operation on the last 3D tensor of which when connected to the dense layer with 4096 nodes resulted in $7 \times 7 \times 512 \times 4096=102,760,448$ parameters. Global Max Pooling was used in subsequent designs to reduce this parameter count.

Even though VGGNet did not win the ILSVRC competition in 2014, it came close to doing so, and its simple and elegant design has been influential in subsequent ConvNet architectures. The main lesson from VGGNet was the classical ConvNet design of the LeNet5/AlexNet type can be substantially improved by increasing the number of Convolutional Layers and by using smaller filters.

### Google Inception Network (2014)


```python
#Inception1
nb_setup.images_hconcat(["DL_images/Inception1.jpg"], width=1000)
```




![png](output_40_0.png)




Along with VGGNet, the Google Inception Network (Figure **Inception1**)) competed in the 2014 ILSVRC competition, see [Szegedy, Ioffe, Vanhoucke (2016)](http://arxiv.org/abs/1602.07261). It did slightly better than VGGNet (6.7% top 5 error rate as compared to 7.3% for VGGNet), but at the cost of a more complex architecture. The Inception Network was the first design that moved away from the linear stacking of convolutional and pooling layers and introduced the Split/Transform/Merge architecture to ConvNets. It was able to reduce the number of parameters to about 5 million by using this and also by eliminating all fully connected layers with the use of Global Max Pooling.


```python
#cnn7
nb_setup.images_hconcat(["DL_images/cnn6.png"], width=800)
```




![png](output_42_0.png)



The InceptionNet design was based on the stacking of a base module callled the Inception Module (see Figure **cnn6**).
As the LHS of the figure shows, the basic idea of the Inception module is to process the input data using multiple filters in parallel, before concatenating all their Activation Maps together and forming the input to the next stage (which we called Split/Transform/Merge earlier in this chapter). The Inception module uses four different types of convolutional engines: $1 \times 1$, $3 \times 3$, $5 \times 5$, and $3 \times 3$ with max-pooling. The smaller convolutions extract features at a finer level of detail, while the larger convolutions deal with features at a coarser level. However there is a problem associated with the architecture on the LHS: After the Activation Maps on all the four branches are concatenated, it results in 672 Activation Maps at the output of the module! As we add more modules, this will clearly result in an explosion in the number of Activation Maps, thus making the architecture infeasible. Another problem with the architecture is the extremely large number of numerical operations required to compute the activations.

The solution to these problems is shown on the RHS of Figure **cnn7** and uses the concept of Bottlenecking with $1\times 1$ convolutions: We add three Activation Maps to the design that are generated using $1\times 1$ convolutions. The $1\times 1$ convolution in series with the Pooling layer reduces the number of Activation Maps in that branch from 256 to 64, which reduces the total number of Activation Maps at the output to 480. In addition two more $1\times 1$ convolutions are added to the $3\times 3$ and $5\times 5$ filter branches to compress the number of input Activation Maps to 64, before they are processed by the larger filters. This helps to reduce the number of numerical computations required from 854 million to 358 million.

The InceptionNet design aligns with the intuition that visual information should be processed at different scales and then aggregated so that the next stage can abstract features from different scales at the same time. The designers of the system also included a couple of extra output modules in the middle of the network (see Figure **Inception1**)), in order to amplify the error signal propagating towards the initial portion of the network, since they were concerned that the large number of layers in the network will cause the error signal to fade by the time it gets to the initial portion.

### ResNet (2015)


```python
#cnn7
nb_setup.images_hconcat(["DL_images/cnn7.png"], width=800)
```




![png](output_45_0.png)



ResNets (short for Residual Neural Networks) were introduced by [He, Zhang, Ren, Sun (2015)](https://arxiv.org/abs/1512.03385), and this design won the ILSVRC 2015 competition by a wide margin, achieving a top 5 error error rate of 3.57%. ResNets have innaugurated the era of *ultra-deep* ConvNets, indeed the winning ResNet network came with 152 layers, an order of magnitude jump from the 22 layers in the previous year's winner. The main architectural innovation in ResNets made such deep networks possible, and is based on the following insight: The number of layers in a ConvNet is constrained due to the fact that the error information propagating back during the backward phase of the Backprop algorithm, tends to get more and more diffused by the time it gets to the initial layers, due to multiplications with the weights and activations in the intervening layers. As a result the weights  in the initial few layers are not modified in an optimal fashion during Gradient Descent. This effect is shown in Figure **cnn7**, which shows that both the Training and Test Error for a 56-layer network is higher when compared to that of a 20-layer network (which implies that the increase cannot be attributed to overfiting).




```python
#cnn8
nb_setup.images_hconcat(["DL_images/cnn8.png"], width=600)
```




![png](output_47_0.png)



In order to overcome this problem,  [He, Zhang, Ren, Sun (2015)](https://arxiv.org/abs/1512.03385) introduced a bypass link, as shown in LHS of Figure **cnn8**.

- In the forward pass of Backprop, the bypass link enables the input signal to skip a few stacked Convolutional Layers, and then it is added to the output of these layers as shown. Note that the very first Convolutional Layer in the system is not bypassed. Hence one way to interpret this design is the following: The bypass enables the activation after the first convolutional layer to propagate all the way to the front of the network, while being modified by some delta (or residue) from each of the intervening bypassed layers. This design is based on the hypothesis that it is easier to optimize the residual mapping than to optimize the original, unreferenced mapping.

- In the backward pass of Backprop, the bypass enables the error gradient information from the Output Layer of the network to propagate all the way to the first Convolutional Layer (with some modification from the gradients from the intervening layers). Hence all the layers in the network are able to access a strong signal from the error gradient information from the Output Layer, irrespective of the total number of layers in the network. This property enables ResNets to go Ultra-Deep without sacrificing performance.

Other interesting aspects of ResNets include the following:

- The system makes extensive use of Batch Normalization, see Section **BatchNormalization**, which is implemented at the end of every layer.

- It uses a relatively large Learning Rate of 0.1 (Section **LearningRateSelection**), which is divided by 10 whenever the validation error plateaus during training. Such a large rate is made possible due to the use of Batch Normalization.

- The system does not make use of Dropout normalization (Section **DropoutRegularization**). It is theorized that Dropout is not needed in the presence of Batch Normalization.

- The system does not make use of Dense layers at the end of the network.

ResNets are still among the best performing ConvNets and are used by default in practical cases.


```python
#convnet44
nb_setup.images_hconcat(["DL_images/convnet44.png"], width=700)
```




![png](output_49_0.png)



There has been some recent work by [Li, Xu et.al.] (https://arxiv.org/pdf/1712.09913.pdf) which beautifully shows the beneficial effect of adding Residual Connections. They achieved this by coming up with a new way to visualize Loss Surfaces for a Neural Network, examples of which are shown in Figures **convnet 44** and **convnet 45**. Part (a) of Figure **convnet44** shows the Loss Surface for a 56 layer ResNet without any Residual Connections, while Part (b) shows the Loss Surface for the same network after the addition of Residual Connections. As cen be seen, the Loss Surface has become much more smooth and convex in shape, which makes it easier to run the SGD algorithm on it. In contrast, the chaotic shape of the Loss Surface without residual connections makes it very easy for the SGD algorithm to get caught in local minimums. There is a single large minima in the Loss Surface without Residual Connections, however for the SGD to get to it, it needs to initialized properly. This also implies, that without Residual Connections, the effectiveness of SGD is highly dependent on the initialization values.


```python
#convnet45
nb_setup.images_hconcat(["DL_images/convnet45.png"], width=700)
```




![png](output_51_0.png)



The contour plots in Figure **convnet45** shows the effect of the network depth on the Loss Surface, both with and without Residual Connections. We observe the following:

- Networks with a smaller number of layers, such as the 20 layer ResNet on the LHS, exhibit fairly well behaved Loss Surfaces, even in the absence of Residual Connections. Hence Residual Connections are not essential for smaller networks.
- Networks with a larger number of layers on the other hand, start to exhibit chaotic non-convex behavior in their Loss Surface in the absence of Residual Connections.


```python
#convnet48
nb_setup.images_hconcat(["DL_images/convnet48.png"], width=700)
```




![png](output_53_0.png)



Another very interesting perspective on why Residual Connections are so effective was provided by [Veit, Wilbur, Belongie] (https://arxiv.org/pdf/1605.06431.pdf). Instead of looking at the backward flow of gradients, the focused on the forward path of ResNet, and noted the following:

- In a network with no Residual Connections, there exists only a single forward path and all data flows along it. However in a network with n Residual Connections, there exist $2^n$ forward paths. This is illustrated in Figure **convnet48** for the case $n=3$. The 8 separate forward paths that exist in this network are shown in Part (b) of this figure. As a result, the network decisions are effectively made by all of these 8 forward paths, that are operating parallel. This is very much like what is done in the Ensemble method, in which multiple models operate in parallel to improve model accuracy.

-  They furthermore showed that gradient flow in the backwards direction is dominated by a few shorter paths. This is illustrated in Figure **convnet49** which has results for a network with 54 Residual Connections. Part (a) of this figure shows the distribution of the path lengths in this network, while Part (b) plots the gradient magnitudes. They further multiplied the gradient magnitudes with the number of pathlengths for a particular path, and and obtained the graph in Part (c). As can be seen the majority of the gradients are contributed by path lengths of 5 to 17, while the higher path lengths contribute no gradient at all. Fom this they concluded that in very deep networks with hundredsof layers, Residual Connections avoid the vanishing gradient problem by introducing short paths which can carry the gradient throughout the extent of these networks.


```python
#convnet49
nb_setup.images_hconcat(["DL_images/convnet49.png"], width=700)
```




![png](output_55_0.png)



### Beyond ResNets: ResNext and DenseNet


```python
#ResNext
nb_setup.images_hconcat(["DL_images/ResNext.png"], width=600)
```




![png](output_57_0.png)



The base ResNet design can be improved by applying the techniques discussed earlier in this chapter, two of which are shown in Figure **ResNext**:

- The Left Hand Side of the figure shows the application of Bottlenecing using $1\times 1$ filter, which reduces the number of parameters and computation by almost a factor of 3
- The Right Hand Side of the figure shows the application of Split/Transform/Merge to ResNet, which results in a network called ResNext.

A 101-layer ResNeXt was able to achieve better accuracy than a 200-later ResNet even though it has only 50% of the parameters. ResNeXt was submitted to the ILSVRC 2016 classification task, in which it secured second place.


```python
#DenseNet
nb_setup.images_hconcat(["DL_images/DenseNet.png"], width=800)
```




![png](output_59_0.png)



DenseNets are built from modules called Dense Blocks as shown in the lower part of figure **DenseNet**. Within each Dense Block, the Activation Maps of all preceding layers are used as inputs into the next convolutional layer, and its own Activation Maps are used as inputs into all subsequent layers. In contrast to ResNets, DenseNets don't combine features through summation before they are passed into a layer; instead, they combine features by concatenating them. DenseNets use smaller number of Activations Maps per layer (only 12) compared to ResNets, which results in a decrease in the number of parameters. It is likely that the concatenation of layers makes up for this reduction. The Table **ConvNetPerformance** shows that DenseNets are able to outperform ResNets with a smaller model size.


```python
#convnet47
nb_setup.images_hconcat(["DL_images/convnet47.png"], width=700)
```




![png](output_61_0.png)



The DenseNet architecture is quite effective in making the shape of the Loss Function surface more convex and hence easier to optimize, as shown in Part(b) of the above figure (taken from [Li, Xu et. al]  https://arxiv.org/pdf/1712.09913.pdf). 

### Xception


```python
#Xception
nb_setup.images_hconcat(["DL_images/Xception.png"], width=700)
```




![png](output_64_0.png)



The Xception architecture replaces the regular Convolution operation by Depthwise Separable convolutiion in all its layers except for the first two. It has 36 convolutional layers forming the feature extraction base of the network. These convolutional layers are structured into 14 modules, all of which have linear residual connections around them, except for the first and last modules. 

The Xception network has performance that is comparable with the Google InceptionNet, but with a smaller parameter count.

### MobileNet


```python
#MobileNet
nb_setup.images_hconcat(["DL_images/MobileNet.png"], width=700)
```




![png](output_67_0.png)



MobileNet belongs to the same category of architectures as Xception, since it uses Depthwise Separable Convolutions to bring down the parameter count. The motivation behind MobileNet was to come up with a design that could be deployed in real world applications such as robotics, self-driving car and augmented reality. These involve tasks need to be carried out in a timely fashion on a computationally limited platform with small low latency models.

The MobileNet architecture is defined in Table 1 (note that a filter shape of $1\times\times 1\times 128\times 256$ denotes a $1\times 1$ filter with 128 Activation Maps in the input layer and 256 Activation Maps in the output layer). All layers are followed by a batchnorm and ReLU nonlinearity with the exception of the final fully connected layer which has no nonlinearity and feeds into a softmax layer for classification. A final average pooling reduces the spatial resolution to 1 before the fully connected layer. Counting depthwise and pointwise convolutions as separate layers, MobileNet has 28 layers. As Table **ConvNetPerformance** shows, this results in a model with the smallest number of parameters, with some decrease in accuracy.

## Visualizing ConvNets

ConvNets seem to work very well and constitute a significant advance in neural network architecture. However their decision making process proceeds through complex non-linear computations that are opaque to humans. In order to gain more confidence in the output of these networks, it would be nice if we can get some insights into how they go about doing their job. The field of ConvNet Visualization attemtps to do this in various ways that are described in this section. In particular we will describe the following techniques:

- Visualizing the last layer in the Feature Space: The Last Layer before the classification step represents the results of all the transformations on the original image, and hence visualizing its co-ordinates gives insights into the ConvNets's operation.
- Visualizing Local Filters: Using the template matching interpretation of image recognition, the shape of local filters can tell us the kind of objects the network is looking for.
- Identifying Maximally Activating Patches in Images: This technique solves the following problem: Given a neuron that gets activated by an image, identify the portion of the image that it is reacting to.
- Generating Images that Maximize Neuron Activations: This is the process of running the ConvNet backwards to generate images that maximize the activation at a chosen neuron.
- Generating Images from Feature Vectors: This also involves running the ConvNet backwards, to generate images whose Feature Vectors match those from a sample image.

### Visualizing the Proximity Property of Feature Space Representations


```python
#cnn10
nb_setup.images_hconcat(["DL_images/cnn10.png"], width=900)
```




![png](output_71_0.png)



We have emphasized the fact that DLNs transform the representation of images from RGB pixels to a feature space representation that also carries semantic information, such that images that are in the same category tend to have representations that cluster together in feature space. This property can be verified by examining the L2 nearest neighbors for an image, as shown in the RHS of Figure **cnn10**. This figure shows the sample image in the first column on the left side of the figure, while the images in each row correspond to images whose feature space L2 distance is closest to the sample image in that row. The feature space representation is obtained as the activations of the FC2 Fully Connected layer in AlexNet (see Figure **convnet7**). We note the following:

- Images whose pixel values are very different are nevertheless close to each other in feature space, thus verifying the semantic clustering property of DLNs.
- On the other hand, relying on L2 nearest neighbors in pixel space is not a reliable way of clustering images, since it can result in images that are in different categories, as shown on the LHS of Figure **cnn10**.

### Visualizing Local Filters


```python
#cnn9
nb_setup.images_hconcat(["DL_images/cnn9.png"], width=900)
```




![png](output_74_0.png)



Consider a ConvNet, such as AlexNet, with 64 Activation Maps in the first Convolutional Layer which are generated using 64 local filters of size $11\times 11$. Each of these filters can be visualized by using the filter values to generate a $3\times 11\times 11$ color image, and this is shown in Figure **cnn9** for AlexNet as well as for a few other types of ConvNets. Using the template matching interpretation of local filtering, it follows that first Hidden Layer filters in all these networks are mostly looking for simple patterns such as straight edges in various orientations. Hubel and Wiesel had discovered that the visual system in animals has a similar property, in that the first layer of neurons in the visual cortex is sensitive to the presence of edges in the image falling on the retina.

Unfortunately it is not possible to as readily visualize filters in the deeper layers of the network, due to the fact that they possess a depth of more than 3 and hence cannot be converted into a color image. Hence in order to understand what is happening in the deeper layers of the network, we rely on techniques described in the following sub-sections.

### Visualizing Activation Maps

Unlike Convolutional Filters, Activation Maps can be visualized for all layers of a network, since each of them can be considered to be a grayscale image. This exercise was carried out in Chollet Section 5.4.1 and the results are summarized for the cat image shown below.


```python
#convnet36
nb_setup.images_hconcat(["DL_images/convnet36.png"], width=900)
```




![png](output_78_0.png)



Figure **convnet37** graphs some of the Activation Maps in Convolutional Layer 1 and Layer 8 of an 8 layer ConvNet. We note tha following:

- Recall that the Activations Maps in Layer1 act as detectors of simple shapes such as edges of various types. The Activation Maps figures in Layer 1 bear this out, since most of them outline the shape of the cat which is where the edges occur.
- An examination of the Layer 8 Activation Maps on the other hand shows that they have very little resemblance to the original image. In most Activation Maps a few of the neurons show higher activation than the others (these are coded in yellow). These are responding to some higher level aspect of the input image, but we can't tell what that is from the Activation Maps figures alone. Thus higher level activations carry more and more information about the presence or absence of certain complex patterns in the input image, rather than the shape of the image itself. If a neuron has zero activation then it menas that the pattern it is looking for is not present in the input image.


```python
#convnet37
nb_setup.images_hconcat(["DL_images/convnet37.png"], width=1200)
```




![png](output_80_0.png)



### Identifying Maximally Activating Patches in Images

In the previous section we surmised that the neurons in the higher convolutional layers are activated by more complex patterns in the input iamge while the lower layers are activated by simpler paterns. This intuition can be verified  by using the concept of Maximally Activating Patches, which are defined as follows: Pick any neuron in a ConvNet, it can be one of the logit nodes whose activation is equal to the class-score of the corresponding category, or it can  be a neuron in one of the Activation Maps within a convolutional layer. Assuming that the input image is such that it results in a high activation value at the chosen node, i.e., the neuron reponds positively to some pattern that it detects in the image. Then the Maximally Activating Patch is defined to be the localized portion of the image that the neuron is responding to.

Maximally Activating Patches are identified by running the ConvNet backwards, which is actually a very important notion. Though originally proposed as a way to identify Maximally Activating Patches, the backwards operation has since been extended to tasks that involve **generating** new images from a trained ConvNet.

There are two main techniques that are used to run a ConvNet backwards:

- DeConvNet
- Guided Backpropagation


```python
#cnn_13_Backwards_Propagation_through_MaxPooling
nb_setup.images_hconcat(["DL_images/cnn13.png"], width=600)
```




![png](output_82_0.png)




```python
#cnn15_Backwards_Propagation_through_ReLU
nb_setup.images_hconcat(["DL_images/cnn15.png"], width=600)
```




![png](output_83_0.png)



Both these techniques use the same computations for going backwards through Convolutional and Pooling layers, but differ in the way they pass through ReLU non-linearities. These operations are described next:

- Backwards through Convolutional Layers: This operation is the same as that carried out by backpropagating gradients in the Backprop algorithm, and involves multiplication by the transpose of the Convolutional Filter. 

- Backwards through Pooling Layers: This operation is referred to as "switching" and proceeds as follows: Carry out a forward pass through the network, and keep record of the positions at which the maximum activation in max-pooling occurs (see Figure **cnn13**). In the backward pass, the incoming activation is placed in the "maximum activation" spot, while all the activations are set to zero. The reader may recall that this rule was derived in Chapter **TrainingNNsBackprop** in the section on Gradient Flow Calculus.

- Backwards through ReLU Non-Linearities: As shown in Figure **cnn15**, there are multiple ways in which a ConvNet can be run backwards through ReLU non-linearities:

    - The top row of the figure shows a Forward Pass through a ReLU non-linearity. It shows the negative pre-activations on the LHS being reset to zero in order to generate activation numbers on the RHS of the figure.
    - The second row in the figure shows a backward pass through a ReLU for gradients using traditional Backprop: Recall that the ReLU non-linearity acts as a switch for the gradients during Backprop, so that the negative pre-activations (in the LHS of the top row) cause the gradients in the corresponding positions to go to zero.
    - The third row in the figure shows the ReLU backward pass used in DeConvNets. When going backwards through a ReLU non-linearity, all negative values are set to zero, as shown. In contrast to Backprop and Guided Backprop (see below), the numbers flowing back during the DeConvNet operation should not be thought of as gradients, they should be regarded as "activations"" that are propagating backwards.
    - The fourth row in the figure shows a backward pass for gradients used in Guided Backpropagation. When passing backwards through ReLU non-linearity, the negative gradients are set to zero, in addition to the gradients for whom the corresponding input activation is negative. Hence the Guided Backpropagation ReLU backpropagation rule combines the rules for Regular Backpropagation + DeConvNet Backpropagation.





```python
#cnn11
nb_setup.images_hconcat(["DL_images/cnn11.png"], width=1200)
```




![png](output_85_0.png)



We now describe the application of DeConvNets to the problem of finding out the portion of an image that an individual neuron is responding to (also called the Maximally Activating Patch):

- Start with a fully trained ConvNet model (such as on ImageNet) and present it with an input image. Do a forward pass through the model and compute all the activations.
- To examine a given activation, say $a$, (which has been activated by the image), set all the other activations in its Activation Map to zero (as well as the activations of the other Activation Maps in its layer) and pass this as input to the DeConvNet network.
- Propagate the signal backwards using the DeConvNet propagation rules described above, until the pixel space is reached. This results in the computation of ${\partial a}\over{\partial x_{ijk}}$ for all the pixels $x_{ijk}$ in the image.

The reconstructed image obtained by plotting ${\partial a}\over{\partial x_{ijk}}$ for AlexNet (trained on ImageNet) is shown for activations in Layers 1 to 5 in Figure **cnn11**. For each layer, the images on the LHS show the actual reconstruction, while the corresponding images on the RHS are portions of the input image that were identified by the reconstruction. Note that the nine largest activations were chosen in each of the Activation Maps. We can draw the following conclusions from these images:

- The reconstructed image resembles a small piece of the original input image, with the shapes in the input weighted according to their contribution to the neuron whose activation was propagated back.
- All the neurons in a single Activation Map seem to get activated by similar shapes, and this shape varies with the Activation Map. This property is stronger in the higher layers.
- As we go up the layers, the activations get triggered by more and more complex shapes and objects.


```python
#cnn12
nb_setup.images_hconcat(["DL_images/cnn12.png"], width=1200)
```




![png](output_87_0.png)



A similar procedure can be carried out using the Guided Backpropagation procedure, and the results for Convolutional Layers 6 and 9 for AlexNet are shown in Figure **cnn12** (with the recosnstructed image on the LHS and the corresponding patch from the actual image on the RHS). This figure shows that the reconstructed image quality is better with Guided Backpropagation.

### Generating Images

Generating images using ConvNets is one of the most exciting areas in Deep Learning, and as a field is still undergoing rapid development. There are several ways in which ConvNets are being used to generate images, and in this section we explore a few of them:

- Generating images that maximally activate a neuron
- Images generated using Google's Deep Dream algorithm
- Generating images by Feature Inversion

One of the realizations that we have to come based the image generation work, is that a trained Neural Network contains a lot of detailed information about the objects as well as other parts of the image in its training dataset, which is enough to actually generate images of these objects. Previously it was thought that Supervised Learning models incorporated only very basic high level information about objects, which was just sufficient to be able to recognize them. It is also possible to generate images using ConvNets with the help of Unsupervised Learning techniques such as Generative Adversarial Networks (GANs) and PixelCNN, but these are not covered in this chapter.

### Generating Images that Maximally Activate a Neuron


```python
#cnn16
nb_setup.images_hconcat(["DL_images/cnn16.png"], width=800)
```




![png](output_91_0.png)




Start with a fully trained ConvNet, and keep its weights fixed during this procedure. Solve the following maximization problem: 

Find an image $I$ that maximizes the following Loss Function
$$
\mathcal L = S_c(I) - \lambda ||I||^2_2
$$
In this equation, the $S_c(I)$ is the Score Function for the $c^{th}$ class, and is computed by doing a forward pass through the ConvNet. The second term is added for doing Regularization, with $\lambda$ as the Regularization Parameter. It had been experimentally observed that without the Regularization Term, the optimization procedure results in an image that looks like white noise.

The following algorithm is used to do the optimization:

1. Start with a trained ConvNet (trained on zero centered image data) and fix the value of its weights. Initialize the image pixel values $x_{ijk}$ to zero.
2. Repeat Steps 3 to 5 until a Stopping Condition is satisfied
3. Do a forward pass through the network and compute the Score Function $S_c(I)$ and Loss Function $\mathcal L$.
4. Starting with the gradient $\frac{\partial\mathcal L}{\partial S_c}$, use the Backprop algorithm to compute the gradients $\frac{\partial\mathcal L}{\partial x_{ijk}}$ of the Loss Function with respect to each of the image pixel values
5. Change the pixel values using the following iteration:
$$
x_{ijk} \leftarrow x_{ijk} - \eta\frac{\partial\mathcal L}{\partial x_{ijk}}
$$
6. Add the training set mean image to the final pixel values to obtain the final image.



Figure **cnn16** shows the results of applying this algorithm to a ConvNet trained on the ImageNet dataset. The reader will notice the objects belonging to the category whose Score Function is being maximized, emerging at multiple places in each image, but with colors that are different than the natural coloration of the object. The reason for this is that the neurons in the later layers of the network, and especially the classification neurons, incorporate more invariance in their object recognition. Hence they recognize an object irrespective of its color or location in the image and this invariance property gets reflected in the generate images. It is possible to generate images that are more pleasing to the eye, and some of these are shown in Figure **cnn19**. These images were generated by making the following changes to the algorithm described above:

- Incorporation of the Total Variation (TV), Gaussian Blur and Jitter regularizers into the Loss Function
- Initialize the image by using the average of the images in that category from the test dataset (if an image has multiple facets, then averaging is done over one of the facets)
- Use of Gaussian Blur regularization results in a blurry, but single and centered object. The optimization then proceeds by updating the center pixels more than the edge pixels to produce a final image that is sharp and is centrally located.

Chollet Section 5.4.2 has a Keras implementation of a very similar algorithm for generating images that maximally active the average activation of a chosen Activation Map.


```python
#cnn19
nb_setup.images_hconcat(["DL_images/cnn19.png"], width=600)
```




![png](output_94_0.png)



### Adversarial Images


```python
#cnn20
nb_setup.images_hconcat(["DL_images/cnn20.png"], width=600)
```




![png](output_96_0.png)



It has been shown that ConvNets can be fooled into mis-classifying images. A couple of examples of this are shown in Figure **cnn20**: In the top row the first image is classified correctly as an elephant. Then this image is modified by changing some the pixels (which are shown in the last two columns), which results in the second image. These changes are not perceptible to the human eye since the second image also looks like an elephant, however when sent through a ConvNet, the system classifies it as a koala. A similar process applied to the boat in the bottom row, results in its mis-classification as an iPod. These images, which fool the ConvNet into mis-classifying them, are known as Adversarial Images.

Adversarial images can be easily created by making a slight modification to the algorithm that was presented in the prior section for generate images that maximally activate neurons. The only changes needed are the following:

1. Instead of initializing the input image with zeroes, we initialize it with the image whose adversarial example we wish to generate.
2. Choose the neuron whose activation is to be maximized, as the classification node for the adversarial image class.

We then run the maximization algorithm, and after a few iterations, the system will mis-classify the input image even though it does not appear to have changed.

Adversarial Images are an active research topic, since they constitute a significant security loophole that can perhaps be exploited.

### Generating Images Using Google Deap Dream


```python
#cnn17
nb_setup.images_hconcat(["DL_images/cnn17.png"], width=600)
```




![png](output_99_0.png)



Google Deep Dream uses the following algorithm to generate images:

1. Start with a trained ConvNet (trained on zero centered image data) and fix the value of its weights. Initialize the image pixel values $x_{ijk}$ to some random image from the test dataset. In the example in Figure **cnn17**, the initial image was chosen to be that of clouds, shown on top part of the figure.
2. Repeat Steps 3 to 6 until a Stopping Condition is satisfied
3. Do a forward pass through the network and compute the activations at all the nodes, up until a chosen layer.
4. Set the gradients at each node of the chosen layer equal to the activation at that node, i.e.,
$$
\frac{\partial\mathcal L}{\partial z_i} = z_i
$$
5. Using the Backprop algorithm compute the gradients $\frac{\partial\mathcal L}{\partial x_{ijk}}$ of the Loss Function with respect to each of the image pixel values
6. Change the pixel values using the following iteration:
$$
x_{ijk} \leftarrow x_{ijk} - \eta\frac{\partial\mathcal L}{\partial x_{ijk}}
$$
7. Add the training set mean image to the final pixel values to obtain the final image.

In the example in Figure **cnn17**, the ConvNet was trained using ImageNet. The top part of the figure show the input image, and after a number of iterations, the original image changes to the one shown in the bottom of figure. The Deep Dream algorithm tends to amplify random features in the original image, until they start to resemble objects that were part of the network's original training set. Note that setting the gradient equal to the activation is equivalent to using the following Loss Function:
$$
\mathcal L = {1\over 2}\sum_i z_i^2
$$
where the sum is over all the activations in a given layer.

Chollet Section 8.2 has a Keras implementation of Google Deep Dream.

### Generating Images Using Feature Inversion


```python
#cnn18
nb_setup.images_hconcat(["DL_images/cnn18.png"], width=600)
```




![png](output_102_0.png)



The image generation techniques that we have described so far, do their work by iteratively creating images that maximally activate a neuron. There is another technique, which instead of trying to maximize neuron activations, instead works by generating images whose Feature Vector is specified in advance. In order to do so, the following Loss Function is used:
$$
\mathcal L = ||\Phi(X) - \Phi_0||^2 + \lambda_\alpha \mathcal R_\alpha(X) + \lambda_{V^\beta}\mathcal R_{V^\beta}(X)
$$
where the Regularisers $\mathcal R_{\alpha}$ and $\mathcal R_{V^\beta}$ are set to
$$
\mathcal R_\alpha(X) = ||X||^\alpha_\alpha,\ \ {\mbox and}\ \ \mathcal R_{V^\beta}(X) = \sum_{i,j} ((x_{i,j+1} - x_{ij})^2 + (x_{i+1,j} - x_{ij})^2)^{\beta\over 2}
$$
In these equations $\Phi_0$ is the Feature Vector from the test image that the algorithm is trying to match, while $\Phi(X)$ is the Feature Vector from the current iteration of the generated image. Note that the addition of the Regularisers $\mathcal R_{\alpha}$ and $\mathcal R_{V^\beta}$ is critical to generating "good" images. In their absence, the algorithm will generate images whose Feature Vector minimizes the Loss Function, but which look like noise to the human eye.

The algorithm is as follows:

1. Start with a trained ConvNet (trained on zero centered image data) and fix the value of its weights. Initialize the image pixel  $x_{ijk}$ to some random values. The example in Figure **cnn18** shows two different test images in the leftmost image in each row.
2. Repeat Steps 3 to 5 until a Stopping Condition is satisfied
3. Do a forward pass through the network and compute the activations at all the nodes, up until a chosen layer.
4. Compute the gradients $\frac{\partial\mathcal L}{\partial\Phi}$ at each node of the chosen layer and use the Backprop algorithm compute the gradients $\frac{\partial\mathcal L}{\partial x_{ijk}}$ of the Loss Function with respect to each of the image pixel values
5. Change the pixel values using the following iteration:
$$
x_{ijk} \leftarrow x_{ijk} - \eta\frac{\partial\mathcal L}{\partial x_{ijk}}
$$
6. Add the training set mean image to the final pixel values to obtain the final image.

The images generated by running this algorithm are shown in Figure **cnn18**. The notation relu2_2 is used to denote the images generated by matching feature vectors in the second layer and so on. As the figure shows, the generated images in the first few layers closely match the original test image, which implies that the ConvNet is able to store fine level details regarding the test image with a high level of fidelity. As we go to the higher layers, the image content and the overall spatial structure are preserved, but the color, texture and exact shape are not.

This procedure shows that the activations at a particular layer can be used to 'encode' an image. Hence instead of transmitting the original image, we instead send the activations from one of the layers. At the receiving end, we use these activations plus our knowledge of the pre-trained model which generated the activations to 'de-code' the image back.

## Other Image Processing Tasks


```python
#convnet38
nb_setup.images_hconcat(["DL_images/convnet38.png"], width=1200)
```




![png](output_105_0.png)



In addition to Classification, ConvNets are also used to solve several important Image Processing tasks. We discuss the following in this section:

- Object Localization: This involves having the model put a box around the object, in addition to classifying it.
- Semantic Segmentation: This is defined as the process of classifying each and every pixel in an image, into a fixed number of categories.
- Object Detection: Object Localization is restricted to boxing a single object (or a fixed number of them). If the number of objects to be boxed and identified is variable and not known in advance, then the problem becomes that of Detection.

Examples of thesee three types of image processing are shown in Figure **convnet38**.

### Object Localization


```python
#Localization
nb_setup.images_hconcat(["DL_images/convnet39.png"], width=1200)
```




![png](output_108_0.png)



The Classification + Localization problem can be solved by training a model to predict the co-ordinates of the 4 corners of the bounding box, in addition to classifying the object. In order to do so, the modeler has to create a training dataset in which the label identifies the co-ordinates of the box. Once this done, the training can proceed using the type of model shown in Figure **Localization**. It shows a so-called 'two-headed' Convnet, with the body consisting of the convolutional base. The output from the base is routed to Dense Networks, with Network One connected to the logits for classifying the object (using the Softmax Loss) and Network Two connected to a Regression Layer that predicts the box co-ordinates (using the Mean Square Error or L2 Loss). The Backprop algorithm is then run on the combined loss. As the figure shows, Transfer Learning can be used for this problem with a pre-trained Convolutional Base, as long as the objects to be classified are not too different than the ImageNet dataset.

### Semantic Segmentation


```python
#Labeling
nb_setup.images_hconcat(["DL_images/convnet40.png"], width=1200)
```




![png](output_111_0.png)



Semantic Segmentation is the problem of classifying each and every pixel in an image into a fixed number of categories. It has a number of important application, for example it can be used by the vision system in a self-driving car to differentiate the road, pedestrians, trees etc. In order to train a model to do Semantic Segmentation we need an appropriate training dataset in which every pixel is labeled, an example of which is shown in Figure **Labeling**. In this example all the pixels are given one of 5 labels, and this information is captured using multiple Label Maps as shown.


```python
#SemanticSegmentation
nb_setup.images_hconcat(["DL_images/convnet41.png"], width=1200)
```




![png](output_113_0.png)



The objective of the Semantic Segmentation model is to predict a Label Map for the input image, and this can be done using ConvNets as shown in Figure **SementicSegmentation**. The input image is sent through multiple convolutional layers, and the final prediction is in the form of a 3D tensor with C layers (corresponding to C pixel categories). For the $c^{th}$ layer, the model predicts a total of $H\times W$ binary valued probabilities of the pixels belonging to the $c^{th}$ category. The final prediction for a pixel location is the category that has the maximum probability value.

### Object Detection

Object Detection is a challenging problem since the number of objects in the image is not known in advance. An initial attack on this problem led to an algorithm called R-CNN (stands for Region based CNN) in which a ConvNet model was used to detect images over several region candidates in the image (these region candidates were generated seprately by a non-ML algorithm). This did work but was very expensive, since each image required several forward passes through the model. An algorithm called YOLO (for 'You only Look Once') was proposed subsequently, which is much more efficient since it can do its job with just a single forward pass. This makes it suitable for real time detection tasks, such as detecting objects in a video clip.

The YOLO algorithm takes the following steps to do detection (see Figure **YOLO**):

- The image is divided into a grid of size $S\times S$ as shown in the LHS of the figure
- For each grid cell, the model predicts $B$ Bounding Boxes as potential candidates for object detection, for a total of $BS^2$ Bounding Boxes. This is shown in the top half of the figure.
- The model predicts a confidence score for each bounding box, which is defined as $P(Object)*IOU^{truth}_{predict}$. These confidence scores reflect how confident the model is that the box contains an object and also how accurate it thinks the box is that it predicts.
- Lastly, for each grid cell, the model predicts the softmax probability vector of it containing one of the $C$ objects $P(Class_i|Object), 1\le i\le C$, i.e. the conditional probability of class $i$ given that the grid cell contains an object. This is illustrated in the bottom part of the figure.

The model's final prediction is obtained by doing the following computation:

$$
Pr(Class_i|Object) ∗ Pr(Object) ∗ IOU^{truth}_{pred} = Pr(Class_i) ∗ IOU^{truth}_{pred}
$$

This computation gives us class-specific confidence scores for each box. These scores encode both the probability of that class appearing in the box and how well the predicted box fits the object.


```python
#YOLO
nb_setup.images_hconcat(["DL_images/convnet42.png"], width=1200)
```




![png](output_117_0.png)



The YOLO Model is shown in Figure **YOLO_Model**, for the case $S = 7, B = 2$ and $C = 20$. This system models detection as a Regression problem. Note that the final predictions are encoded as a $S\times S\times (5B+C)$ tensor since the model predicts $5B+C$ numbers for each grid cell: $x,y,w,h$ and $confidence$, where the $(x, y)$ coordinates represent the center of the box relative to the bounds of the grid cell. The width and height are predicted relative to the whole image and the confidence prediction represents the IOU between the predicted box and any ground truth box.


```python
#YOLO_Model
nb_setup.images_hconcat(["DL_images/convnet43.png"], width=1200)
```




![png](output_119_0.png)



## References and Slides

- [Slides CNN3](https://drive.google.com/file/d/1JSYMO2BwblfMIFTCfQhgmRevm9FtazJq/view?usp=sharing)
- [Slides CNN4](https://drive.google.com/file/d/1Zy0ZmTNu4u086cUjcO0dbGS6Y8K1GXU5/view?usp=sharing)
