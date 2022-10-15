---
layout: default
title: "Convolutional Neural Networks"
---

# Convolutional Neural Networks

## Introduction

Convolutional Neural Networks or ConvNets were originally invented to do image processing. Their origin lies in the research done by Hubel and Wiesel in the 1960s on the visual perception systems in cats, which later won them a Nobel Prize (see [1959](https://physoc.onlinelibrary.wiley.com/doi/abs/10.1113/jphysiol.1959.sp006308); [1962](https://physoc.onlinelibrary.wiley.com/doi/abs/10.1113/jphysiol.1962.sp006837); [1968](https://www.ncbi.nlm.nih.gov/pubmed/4966457)). Fukushima was inspired by their work and created a neural network model which he called the NeoCognitron, see [Fukushima (1975)](https://link.springer.com/article/10.1007%2FBF00342633); [Fukushima (1980)](https://link.springer.com/article/10.1007%2FBF00344251). This model was very similar model to modern ConvNets in its structure, however it lacked an efficient training algorithm, such as Backprop. [LeCun, Bottou, Bengio, Haffner (1998)](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.138.1115) later put the two pieces of the puzzle together while working at Bell Labs during the 90s, and created the modern ConvNet, whose design was based on the NeoCognitron, and which could also be trained using Backprop. LeCun's system, called LeNet5, was successfully commercially deployed to read handwritten signatures in checks. Research in ConvNets lay dormant until 2012, when they were used for the winning entry in the ImageNet Large Scale Visual Recognition Competition (ILSVRC), see [ILSVRC (2015)](https://link.springer.com/article/10.1007%2Fs11263-015-0816-y). This also coincided with a resurgence of interest in neural networks, and since then ConvNets have led the field as the technology behind some of the most powerful DLNs.

## Why Dense Feed Forward Networks don't work well for Images

We start by first considering the question: Why do Dense Feed Forward Networks, not work well when the input is an image? There are two main reasons:

- Consider a typical image consisting of $200 \times 200 \times 3$ pixels, which corresponds to 3 layers of $200 \times 200$ numbers, one for each of the colors Red, Green and Blue. Since the input consists of $120,000$ numbers, these many weights are needed for each node in the first Hidden Layer of a Dense Feed Forward Network. Given a typical Dense Network with say $100$ nodes in the first layer, this corresponds to 12 million weight parameters needed to describe just this layer. More parameters mean that more training data is required to prevent overfitting, which also leads to more time needed to train the model. On the other hand, when ConvNets are used to process images, it reduces the number of parameters by more than two orders of magnitude, thus improving accuracy and reducing training times. It has also been observed in practice that the accuracy of Dense Feed Forward Networks does not keep improving as more hidden layers are added, usually max-ing out at 4 to 5 layers. ConvNets however improve their accuracy with more hidden layers, indeed the most advanced ConvNet architecture features 150 layers!

- Processing by Dense Feed Forward Networks requires that the image data be transformed into a linear 1D vector. This results in a loss of structural information, such as correlation between pixel values that are in proximity of each other in 3D. ConvNets on the other hand are able to process the original 3D image data, which makes it easier for them to recognize shapes using template matching.

![](https://subirvarma.github.io/GeneralCognitics/images/cnn3.png)

*Figure 1*

In order to motivate the design of ConvNets, consider the case when the input consists of $32\times 32\times 3$ [CIFAR-10](https://en.wikipedia.org/wiki/CIFAR-10) [images](https://www.cs.toronto.edu/~kriz/cifar.html), which have to be classified into one of ten categories. Also assume that these images are processed by a Linear Neural Network Model of the type shown in Figure 1. The logits $a_k, i\le k\le 10$ in this model are given by

$$a_k = \sum_{i=1}^{3072} w_{ki} x_i + b_k,\ \ 1\le k\le 10$$

Note that the sum $$\sum_{i=1}^{3072} w_{ki} x_i$$ is maximized if $w_{ki} = x_i,\ 1\le i\le 3072$ under the contraint that both of these are unit vectors. Hence this lends itself to the interpretation that for each category $k$, the weights $w_{ki}, 1\le i\le 3072$ are a template or filter for the category $k$ object, which looks for images that resemble the filter itself. Hence the classification operation can be interpreted as template matching with the input image, as shown in Figure 2.

![](https://subirvarma.github.io/GeneralCognitics/images/cnn3.png)

*Figure 2*

This template matching interpretation of Linear Filtering naturally leads to the following idea for improving the system: Instead of using a template that tries to match the entire image, why not use smaller templates that try to match objects in smaller local portions of the image. This has the following benefits: (a) Smaller templates need a smaller filter size and thus fewer parameters, and (b) Even if the object being detected moves around the image, the same template or filter can still be used, thus leading to translational invariance. This is the main idea behind ConvNets as illustrated in Figure 3.



## Architecture of ConvNets

![](https://subirvarma.github.io/GeneralCognitics/images/cnn3.png)

*Figure 3*

The main architectural aspects of ConvNets are illustrated in parts (a) - (d) of Figure 3:

-  Part (a) of Figure 3 illustrates the difference between template matching in ConvNets vs Dense Feed Forward Networks as shown in Figure 2: ConvNets use a template (or filter) that is smaller than the size of the image in height and width, while the depths match. In the example shown in (a), a filter of size $5\times 5\times 3$ is used for an image of size $32\times 32\times 3$.

- Part (b) shows the template matching operation in ConvNets. As shown here, the matching is done locally, for possibly overlapping patches of the image. At each position of the filter, the template matching is done using the following equation to compute the pre-activation $a$ and activation $z$:

$$a = \sum_{i=1}^{75} w_{i} x_i + b,$$

$$z = f(a) \quad \quad (**tf**)$$

- In this equation the pixel values $(x_1,...,x_{75})$, known as the Local Receptive Field, correspond to the local image patch of size $5\times 5\times 3$ and   changes as the filter is moved around (while the filter values $w_i$ and $b$ remain unchanged). Note that the filter now only has $5\times 5\times 3 + 1 = 76$ parameters, as opposed to the $32\times 32\times 3 + 1 = 3073$ parameters that were needed for the filter in Figure 2. Both the filter as well as the local image patch are 3-D tensors, though the multiplication in Equation (**tf**) uses a stretched out vectorized versions of the two tensors.

- Part (c) of the figure shows the filter being moved across the image, and at each position Equation (**tf**) is used to compute a new value of $z$, and this generates a matrix of size $28\times 28$. This matrix is known as an Activation Map (also called a Feature Map). This operation of sliding the filter across the image, while computing the dot product (**tf**) at each position, is called a convolution. Using the same Filter for all the nodes in the Activation Map implies that all nodes in the Map are tuned to detect the same feature in the Input Layer, *only at different positions in the image*. This leads to the conclusion that ConvNets possess the property of Translational Invariance, i.e., they are able to detect objects irrespective of their location in the image.

- Note that so far we have used a single filter which is only capable of detecting a single pattern in the input image. If we wish to detect multiple patterns, then we need multiple filters, each of which results in its own Activation Map, as shown in Part (d) of Figure 3. For example, Activation Map 1 may detect horizonal edges while Activation Map 2 detects vertical edges etc. As shown, a Hidden Layer in ConvNets consists of a stack of Activation Maps.

The filter in Dense Feed Forward Networks spans the entire input image, which means that it is looking for patterns that also span the entire image. However, real world images are built from smaller patterns that rarely span the entire image plane. Hence, by reducing the size of the filter, Convnets are better positioned to detect smaller shapes, which are then composed hierarchically into larger shapes and objects as we go deeper into the network. Also the Translational Invariance property ensures that the shape is detected irrespective of its location in the image plane.

## Fully Connected DLNs vs ConvNets

![](https://subirvarma.github.io/GeneralCognitics/images/cnn2.png)

*Figure 4*

Figure 4 illustrates another way to contrast ConvNets with Dense Feed Forward networks. The top part of the figure shows a Dense Feed Forward Network with the input image and the nodes in the first Hidden Layer. A node in this Hidden Layer is activated if it detects a particular pattern in the image, with each node looking for a different pattern. As shown in the bottom half of the figure, with ConvNets, each of the Hidden Layer nodes is replaced by an Activation Map with multiple "sub-nodes". The activation value at each sub-node in an Activation Map is computed using a local filter which looks for the same pattern in different parts of the image. Hence in general we need as many Activation Maps in a ConvNet as there are nodes in a Hidden Layer of a Dense Feed Forward Network. This figure also illustrates that ConvNets reduce the number of weights in the model at the expense of increasing the number of nodes. The increase in nodes causes the cost of computation to go up, but this is a worthwhile tradeoff to make since the reduction in the parameters makes the model easier to train with a smaller number of training examples.

![](https://subirvarma.github.io/GeneralCognitics/images/cnn5.png)

*Figure 5*

So far we have only described the operation of the Input Layer and the first Hidden Layer of the ConvNet. However it is straightforward to extend this design to multiple Hidden Layers, as shown in Figure 5. Just as in Fully Connected Deep Feed Forward Networks, Activation Maps in the initial hidden layers detect simple shapes, which are then built upon in an hierarchical way by the later layers to detect more complex shapes. The following hyper-parameters have to be chosen with each additional layer:

- The number of Activation Maps to be used in the Hidden Layer
- The size of the Filter and the Stride size (defined below), to be used to compute the Activations.

In the example in Figure **cnn5**, we added a second Hidden Layer with 10 Activation Maps, that are generated using a filter of size $5\times 5\times 6$. Note that the depth of this filter is not a free variable since it has to equal to the number of Activation Maps in the previous layer.

![](https://subirvarma.github.io/GeneralCognitics/images/cnn22.png)

*Figure 6*

The computations carried out to generate an Activation Map are shown in greater detail in Parts (a) and (b) of Figure 6. Part (a) shows a Filter of size $2\times 2$, operating on an input of size $5\times 5$ (without the depth dimension). In order to generate the activations, the filter is moved by one pixel at a time, horizontally and vertically, which results in an Activation Map of size $4\times 4$. As we slide the $2\times 2$ patch across the Input Layer, we compute a dot product of the activations in the Local Receptive Field with the filter weights. An important parameter used in this process is called the **Stride**, denoted by $S$, and is defined as the number of pixels by which the filter is moved after each computation, either horizontally or vertically. Note that the example in Part (a) corresponds to $S = 1$ while Part(b) shows the case $S = 2$. Note that for the case $S=2$, the last column in the input feature map is not accessed (shown in red). In order to remedy this, we add a an extra column of zeroes to the right, which results in an output of size $2\times 3$. This is known as Zero Padding and is discussed further later in this chapter.

Assuming that the $r^{th}$ Hidden Layer is processed using a filter of size $L\times W\times D$, note that this filter requires $L \times W \times D + 1$ parameters. However, since the same filter is used for *all* the nodes in the Layer $r+1$ Activation Map,  it results in a huge reduction in the number of parameters needed to describe ConvNets. Since each Activation Map in Layer $r+1$ requires its own filter, so that if there are $C$ such Maps (i.e., Layer $r+1$ is of depth $C$), then the total number of parameters needed is given by $C \times (L \times W \times D + 1)$.

In order to appreciate the scale of the reduction in number of parameters due to shared filters, consider a ConvNet with Input Layer consisting of $32\times 32\times 3$ images and containing a Hidden Layer with 20 Activation Maps generated using $5 \times 5$ filters. Since each Activation Map requires $5 \times 5\times 3+1=76$ filter parameters, $76 \times 20 = 1520$ parameters are sufficient to generate the Hidden Layer. On the other hand, in a Fully Connected Deep Feed Forward architecture with $32\times 32\times 3 = 3072$ nodes in the Input Layer and 20 nodes in the Hidden Layer, a total of $3072\times 20+20 = 61,460$ parameters are needed.

## Pooling

![](https://subirvarma.github.io/GeneralCognitics/images/convnet6.png)

*Figure 7*

In addition to the Convolution operation described above, ConvNets also feature an operation called Pooling (see Figure 7). Pooling usually occurs after a Convolutional Layer, and can be described as condensing the information from that layer into a smaller number of activations. As shown in the figure, Pooling involves replacing a set of activations within a region of the Activation Map (which is just like a Local Receptive Field), by a single number. Usually the maximum of the activation values in the Local Receptive Field is used for pooling (called max-pooling), but other functions can also be used, such as the $L_1$ or $L_2$ norm. Unlike in Local Receptive Fields used in Convolutions, the corresponding fields used for the Pooling operation do not overlap. Note that the addition of Pooling does not introduce any new parameters to the ConvNet and the total number of parameters in the model are reduced considerably due to this operation.

In order to understand the Pooling operation, note that the numbers in an Activation Map that results from the Convolution operation, correspond to the likelihood of whether a particular shape or pattern is present in various locations in the previous layer. By doing Pooling right after Convolution, we throw away some of that information, which is the same as saying that the network does not care about the exact location of a pattern, it only needs to know whether the pattern is present or not. It should also be mentioned that as more processing power becomes available, some modern ConvNets, such as ResNet and the Google Inception Network, no longer incorporate Pooling in their design.

## Global Max Pooling

![](https://subirvarma.github.io/GeneralCognitics/images/convnet29.png)

*Figure 8*

The output of the last convolutional layer in a ConvNet is fed into a Dense Feed Forward network before being sent into the logit layer (see Figure 9 below for an example). The traditional way of doing this is by flattening the ConvNet tensor, which causes a huge increase in the number of parameters. Recall from Chapter **ImprovingModelGeneralization** that more parameters can cause overfitting, unless the size of the training dataset is also increased.

In order to reduce the number of parameters, more recently models have started using the Global Max Pooling operation for this interface, which is illustrated in Figure 8. As shown, each spatial layer of the ConvNet is converted into a single node in the Dense Feed Forward network by using the max operation (or alternatively the average operation). 

This design can be justified as follows: Each plane in the final ConvNet layer contains information about the presence of a pattern, and the nodes within the layer contain information the spatial location of the pattern. Since we are not interested in the spatial part of this information when doing classification, it makes sense to summarize the presence/absence information by using the maximum value of the nodes within the plane.

## A Complete ConvNet

![](https://subirvarma.github.io/GeneralCognitics/images/convnet7.png)

*Figure 9*

Figure 9 puts all the elements of a ConvNet together to come up with a network for the case when the input consists of $32\times 32\times 3$ pixel CIFAR-10 images. This network consist of the following:

- Five convolutional layers
- Two Max Pooling Layers, which occur after the second and fourth convolutional layers respectively.
- One Dense Feed Forward Layer, consisting of 1024 nodes, that is placed after the convolutional layers. Note that the output of the fifth convolutional layer is flattened, i.e., it is re-shaped from a 3D tensor of shape (3,3,64) to a 1D tensor of shape 576.
- An Output Logit Layer with 10 nodes, corresponding to the 10 categories that the input image can belong to.
- The Filters are all of spatial size (3x3).

At a high level, the convolution operation changes the representation of an image, starting from raw pixels at one end, to higher level representations using successive layers of filtering. In abstract space, as the system goes through multiple Convolutional Layers, it is basically performing non-linear transformations so that images with similar objects are clustered closer to each other in the higher level transform space. This enables the classification operation to happen using a simple linear classifier in the final layer of the network. The Fully Connected layer that is just prior to the Output Layer contains a 1024-dimensional representation of the input image. It is often used in other Deep Learning architectures that need a high level image representations. 

The following Keras code implements the model from Figure 9, with the CIFAR-10 dataset as input.


```python
import keras
keras.__version__
from keras import models
from keras import layers

from keras.datasets import cifar10

(train_images, train_labels), (test_images, test_labels) = cifar10.load_data()

train_images = train_images.astype('float32') / 255

test_images = test_images.astype('float32') / 255

from tensorflow.keras.utils import to_categorical

train_labels = to_categorical(train_labels)
test_labels = to_categorical(test_labels)
```

The first convolutional layer is invoked using *Conv2D(32,(3,3),activation='relu', input_shape=(32,32,3))*. Hence it accepts as input a 3D tensor of shape (32,32,3) and filters the input using 32 filters, each of which is of shape (3,3,3). Note that only the spatial dimensions (3,3) of the filters need be specified, since the depth dimension is automatically set to the depth of the incoming tensor. This layer transforms the input tensor shape (32,32,3) into an output tensor of shape (30,30,32), and these are also the dimensions of this layer. In the next section we will show how to compute the dimensions of the tensor output from a convolutional layer, given an input tensor. As expected the 2x2 MaxPooling layer halves the spatial dimensions of the incoming tensor, but leaves its depth unchanged. Note that there is no need to re-shape the 3D CIFAR-10 images into 1D vectors, since the convolutional network is able to process the 3D tensors in their native format.


```python
model = models.Sequential()
model.add(layers.Conv2D(32, (3, 3), activation='relu', input_shape=(32, 32, 3)))
model.add(layers.Conv2D(32, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))

model.add(layers.Flatten())
model.add(layers.Dense(1024, activation='relu'))
model.add(layers.Dense(10, activation='softmax'))
```


```python
model.summary()
```

    Model: "sequential"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    conv2d (Conv2D)              (None, 30, 30, 32)        896       
    _________________________________________________________________
    conv2d_1 (Conv2D)            (None, 28, 28, 32)        9248      
    _________________________________________________________________
    max_pooling2d (MaxPooling2D) (None, 14, 14, 32)        0         
    _________________________________________________________________
    conv2d_2 (Conv2D)            (None, 12, 12, 64)        18496     
    _________________________________________________________________
    conv2d_3 (Conv2D)            (None, 10, 10, 64)        36928     
    _________________________________________________________________
    max_pooling2d_1 (MaxPooling2 (None, 5, 5, 64)          0         
    _________________________________________________________________
    conv2d_4 (Conv2D)            (None, 3, 3, 64)          36928     
    _________________________________________________________________
    flatten (Flatten)            (None, 576)               0         
    _________________________________________________________________
    dense (Dense)                (None, 1024)              590848    
    _________________________________________________________________
    dense_1 (Dense)              (None, 10)                10250     
    =================================================================
    Total params: 703,594
    Trainable params: 703,594
    Non-trainable params: 0
    _________________________________________________________________



```python
model.compile(optimizer='rmsprop',
              loss='categorical_crossentropy',
              metrics=['accuracy'])
history = model.fit(train_images, train_labels, epochs=100, batch_size=128, validation_split=0.2, shuffle = True)
```

```python
scores = model.evaluate(test_images, test_labels)
print('Loss: %.3f' %scores[0])
print('Accuracy: %.3f' %scores[1])
```

    10000/10000 [==============================] - 11s 1ms/step
    Loss: 0.909
    Accuracy: 0.725



```python
history_dict.keys()
```
    dict_keys(['val_loss', 'val_acc', 'loss', 'acc'])

```python
import matplotlib.pyplot as plt

acc = history.history['acc']
val_acc = history.history['val_acc']
loss = history.history['loss']
val_loss = history.history['val_loss']

epochs = range(1, len(acc) + 1)
#epochs = range(1, len(loss) + 1)

# "bo" is for "blue dot"
plt.plot(epochs, loss, 'bo', label='Training loss')
# b is for "solid blue line"
plt.plot(epochs, val_loss, 'b', label='Validation loss')
plt.title('Training and validation loss')
plt.xlabel('Epochs')
plt.ylabel('Loss')
plt.legend()

plt.show()
```


![png](output_35_0.png)



```python
plt.clf()   # clear figure
acc_values = history_dict['acc']
val_acc_values = history_dict['val_acc']

plt.plot(epochs, acc, 'bo', label='Training acc')
plt.plot(epochs, val_acc, 'b', label='Validation acc')
plt.title('Training and validation accuracy')
plt.xlabel('Epochs')
plt.ylabel('Loss')
plt.legend()

plt.show()
```


![png](output_36_0.png)


Recall that in Chapter **NNDeepLearing** we classified the CIFAR-10 dataset using a Dense Feed Forward model and achieved a test  accuracy of about 45%. The above example shows a big jump in performance with the use of ConvNets.

Note that the execution time of the ConvNet model is about 4 ms/step (a step being the time to complete a forward pass followed by a backward pass for a single batch of data). In comparison the execution time for a two layer Dense Feed Forward model from Chapter **NNDeepLearning** was about 40 microsec/step. Hence the execution time for the ConvNet model has increased by almost 2 orders of magnitude, which means that these models will not run very well without specialized hardware. The following options can be used:

- Use a computer with GPUs specialized to run Deep Learning models
- Use cloud based services such as Google Cloud or Amazon AWS that provide GPU support. In addition there is a service called Google Colab that allows free use of GPUs for running Python notebooks
- The preferred option is to use a technique called Transfer Learning, which is discussed later in this chapter. This allows the use of large pre-trained ConvNet models, such that only the last few layers of the model need to be trained from scratch, thus reducing model training time

The model.summary() command shows that the model has 703,594 parameters, of which 590,848 or 84%, occur at the Dense Feed Forward layer. Hence Flattening the last convolutional layer and feeding it to a Fully Connected layer leads to an enormous increase in the number of parameters. If we replace Flatten by the "Global Max Pooling" operation, then the parameter count goes down to 179,306 shown below. The corresponding network is illustrated in Figure **convnet31**. If the model is executed then it can be shown that there is no appreciable decrease in the performance of the model. 


```python
#convnet31
nb_setup.images_hconcat(["DL_images/convnet31.png"], width=800)
```




![png](output_39_0.png)




```python
model = models.Sequential()
model.add(layers.Conv2D(32, (3, 3), activation='relu', input_shape=(32, 32, 3)))
model.add(layers.Conv2D(32, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))

model.add(layers.GlobalMaxPooling2D())
model.add(layers.Dense(1024, activation='relu'))
model.add(layers.Dense(10, activation='softmax'))
```


```python
model.summary()
```

    Model: "sequential_1"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    conv2d_5 (Conv2D)            (None, 30, 30, 32)        896       
    _________________________________________________________________
    conv2d_6 (Conv2D)            (None, 28, 28, 32)        9248      
    _________________________________________________________________
    max_pooling2d_2 (MaxPooling2 (None, 14, 14, 32)        0         
    _________________________________________________________________
    conv2d_7 (Conv2D)            (None, 12, 12, 64)        18496     
    _________________________________________________________________
    conv2d_8 (Conv2D)            (None, 10, 10, 64)        36928     
    _________________________________________________________________
    max_pooling2d_3 (MaxPooling2 (None, 5, 5, 64)          0         
    _________________________________________________________________
    conv2d_9 (Conv2D)            (None, 3, 3, 64)          36928     
    _________________________________________________________________
    global_max_pooling2d (Global (None, 64)                0         
    _________________________________________________________________
    dense_2 (Dense)              (None, 1024)              66560     
    _________________________________________________________________
    dense_3 (Dense)              (None, 10)                10250     
    =================================================================
    Total params: 179,306
    Trainable params: 179,306
    Non-trainable params: 0
    _________________________________________________________________


## Sizing ConvNets


```python
#convnet14
nb_setup.images_hconcat(["DL_images/convnet14.png"], width=600)
```




![png](output_43_0.png)



The size (or volume) of a Convolutional Layer in a ConvNet is related to the volume of the prior Convolutional Layer, as well as the size of the Filter used in the convolution operation, and in this section we give some simple expressions that can be used to connect the two. Before we launch into this topic, we introduce another important parameter used in ConvNet design, namely the **Zero-Padding** used during convolution, which we denote as $P$. Zero-Padding does the following: Instead of processing an input of size $L \times W$, we add one or more layers of zeroes around it, in both the dimensions. Hence if $P=1$ then only a single Zero-Padding layer is added, while two layers are added for the case $P=2$ (see Figure **convnet14** for an illustration of the case $P=2$).


### Sizing the Convolutional Layer


```python
#convnet20
nb_setup.images_hconcat(["DL_images/convnet20.png"], width=600)
```




![png](output_46_0.png)



We will use the following notation:

- $L_r$, $W_r$, $D_r$: Length, Width and Depth dimensions of the volume in layer $r$
- $F_r$:    Size of the Filter used when going from layer $r$ to $r+1$.
- $P_r$: Amount of Zero Padding used for layer $r$.
- $S_r$: The Stride size used in the layer $r$ to layer $r+1$ filter.

It can then be shown that
$$
W_{r+1} = \frac{W_r-F_r+2P_r}{S_r}+1
$$
and
$$
L_{r+1} = \frac{L_r-F_r+2P_r}{S_r}+1
$$

In order to gain insight into this formula, consider Figure **convnet20**:

- First consider the case $S_r = 1, P_r=0$: As shown in Part (a) of the figure, $W_r - F_r$ is the number of spaces by which the filter can be slid from left to right with a stride of 1. With the addition of $1$ to account for the final position of the filter, we get $W_{r+1} = W_r - F_r +1$. The presence of zero padding of size $P_r$ results in an increase of the size of the feature map by $2P_r$, so that $W_{r+1} = W_r - F_r + 2P_r + 1$
- If the stride $S_r > 0$, then the number of spaces by which the filter can be moved becomes $W_{r+1} = {{W_r - F_r + 2P_r}\over{S_r}} + 1$

In the presence of parameter sharing,  $F_r\times  F_r\times  D_r + 1$ filter weights are required per Activation Map in layer $r+1$, for a total of $D_{r+1}\times (F_r \times  F_r \times  D_r +1)$ weights and $D_{r+1}$ biases.

As an example of the application of this formula, consider the following example: $W_r=10, F_r= 3, S_r=2$ with no zero padding, so that $P_r=0$. Then applying the above formula it follows that $W_{r+1} = 4.5$, which being a non-integer implies that it is not possible to fit an integer number of nodes in layer $r+1$. We can change the stride to $S_r=1$ which leads to $W_{r+1}=5$, thus resulting in a valid architecture.

In modern ConvNet design, zero padding is used most often to ensure that the volume sizes remain unchanged as we move deeper into the network, in other words we would like that $W_{r+1}=W_r, L_{r+1}=L_r, D_{r+1}=D_r$. From the above equation, this can be ensured if the stride $S_r=1$ and the zero padding $P_r$ is chosen to be:

$$
P_r = \frac{F_r - 1}{2}
$$

The most common ConvNet filter sizes are $F_r = 3$ and $F_r = 5$, which results in $P_r = 1$ and $P_r = 2$ respectively. As we will see later in this chapter, some of the advanced ConvNet designs such as VGGNet and ResNet keep the size of the volumes fixed in their Convolutional Layers, which helps in producing networks with hundreds of layers. In the absence of this feature, the volume sizes progressively decrease as we move deeper in the network, thus limiting the number of Hidden Layers to much smaller values. Zero Padding is implemented in Keras using the command: *conv = model.add.layers.Conv2D(6, (3,3), strides=2, padding='same')*.

As we will see later, early ConvNet designs featured bigger Filters, such as $11\times 11$ or $7\times 7$, in their first few layers. However in more recent designs, it has been discovered that using smaller $3\times 3$ filters, even in the first layer, leads to better performance, as well as a reduction in the number of parameters. This aspect of ConvNet design is explored more fully in Section **SmallFilters**. The depth $D_r$ is usually chosen to be a power of $2$ for computational reasons: Numerical routines used in the calculations work more efficiently in this case.

### Sizing the Pooling Layer

If Layer $r+1$ is a Pooling Layer, then the following formulae hold (using the same notation as in the prior section):

$$
W_{r+1} = \frac{W_r-F_r}{S_r} + 1
$$

$$
H_{r+1} = \frac{H_r-F_r}{S_r} + 1
$$

$$
D_{r+1} = D_r
$$

Note the following:

* The Pooling Layer does not lead to the introduction of new parameters.

* It is not common to use Zero Padding as part of Pooling, hence the absence of the $P_r$ term in the above equations.

* Common numbers used for Pooling are $F_r = 2, S_r = 2$ or $F_r = 3, S_r = 2$.

### Computations during Convolutions

Using the same notation as above, the number of multiplications needed to generate all the activations in Layer $r+1$ is given by:

$$
Mult = F_r F_r D_r\times W_{r+1} H_{r+1}\times D_{r+1}
$$

This can be understood as the product of the following factors:

- The number of computations required to generate a single element of an Activation Map in layer $r+1$ = $F_r F_r D_r$
- The number of computations required to generate all the elements of a single Activation Map = $F_r F_r D_r \times W_{r+1} H_{r+1}$
- The number of computations required to generate all the $D_{r+1}$ Activation Maps in layer $r+1$ = $F_r F_r D_r \times W_{r+1} H_{r+1} \times D_{r+1}$

Earlier in this chapter we observed that a ConvNet Layer with $D$ Activation Maps is roughly equivalent to a Dense Feed Forward Network Layer with $D$ nodes. Given two Dense Feed Forward Layers with $D_r$ and $D_{r+1}$ nodes respectively, the number of computations required to generate the $D_{r+1}$ activations in layer $r+1$ is given by $D_r D_{r+1}$. It follows that the number of computations required to generate Layer $r+1$ in a ConvNet is greater than the corresponding number in a Dense Feed Forward Network by a multiplicative factor equal to $F_r F_r \times W_{r+1} H_{r+1}$, i.e., the size of the ConvNet Filter times the size of the Activation Map. This accounts for the large increase in computation time that we observed in the ConvNet model earlier in the chapter.

## One Dimensional ConvNets


```python
#convnet21
nb_setup.images_hconcat(["DL_images/convnet21.png"], width=600)
```




![png](output_52_0.png)



2D Convolutional Networks are ideal to do Image Processing, since they are able to process 3D image tensors in their native format. But there are important datasets that are either 1D or 2D tensors, examples include:

- Natural Language Processing: Sentences can be represented as a 2D tensor, with a row for each word and the columns with the feature representations for the corresponding word. We came across an example of this dataset in Chapter **NNDeepLearning**.
- Structured Tabular Datasets: These are the most common type of datasets, and can be either a 1D vector or a 2D matrix.

The idea of doing local filtering using convolutions can be extended to these types of datasets by used 1D Convolutions, as shown in Figure **convnet21**. The bottom part of the figure shows a 1D Convolution using a 2x1 filter with a depth of 4 (in blue). An Activation Map in this case is no longer a 2D matrix, but instead is a 1D vector. The 1D Convolutions acts on the 1D Input Activation Map, and converts into an output 1D Activation Map, as shown. If there are D such 1D filters, then each of them will generate its own output Activation Map, resulting an output of tensor shape (4,4) as shown.

The process of sliding (or convolving) the 2x1 filter across the input is illustrated in Figure **convnet22**. It is easy to see that the formula $ W_{r+1} = \frac{W_r-F_r+2P_r}{S_r}+1 $ that was derived for the size of the output Activation Map in 2D Convolutions continues to hold for this case as well.


```python
#convnet22
nb_setup.images_hconcat(["DL_images/convnet22.png"], width=600)
```




![png](output_54_0.png)



The following example, that is taken from Chollet Section 6.4, illustrates the application of 1D Convolutions to the IMDB Movie Review dataset. In Chapter **NNDeepLearning** we showed how to generate the input tensors when starting from raw text data. However this dataset is also available in tensorized form called *imdb*, and this is used for this example.

We start by loading the dataset, and restricting ourselves to the most frequently used 10,000 words in the vocabulary.


```python
from keras.datasets import imdb
from keras.preprocessing import sequence

max_features = 10000  # number of words to consider as features
max_len = 500  # cut texts after this number of words (among top max_features most common words)

print('Loading data...')
(x_train, y_train), (x_test, y_test) = imdb.load_data(num_words=max_features)
print(len(x_train), 'train sequences')
print(len(x_test), 'test sequences')
```

    Loading data...
    25000 train sequences
    25000 test sequences


We create the training and test tensors by cutting off all reviews to 500 words or less, and padding reviews that are smaller with zeroes.


```python
print('Pad sequences (samples x time)')
x_train = sequence.pad_sequences(x_train, maxlen=max_len)
x_test = sequence.pad_sequences(x_test, maxlen=max_len)
print('x_train shape:', x_train.shape)
print('x_test shape:', x_test.shape)
```

    Pad sequences (samples x time)
    x_train shape: (25000, 500)
    x_test shape: (25000, 500)



```python
#convnet24
nb_setup.images_hconcat(["DL_images/convnet24.png"], width=900)
```




![png](output_59_0.png)



The 1D Convolutional model to process the IMDB dataset is illustrated in Figure **convnet24**. The Embedding Layer converts each review from a 1D vector of integers of size 500, into a 2D matrix of shape (500,128), with rows representing words from the review in vector format. The 128 size vector representation for the words is learnt as part of the training.

Note that a Flatten Layer is no longer needed unlike for the case of Dense Feed Forward Networks, since the 1D ConvNet model is capable of processing the text input in its native 2D format.


```python
from keras.models import Sequential
from keras import layers
from tensorflow.keras.optimizers import RMSprop

model = Sequential()
model.add(layers.Embedding(max_features, 128, input_length=max_len))
model.add(layers.Conv1D(32, 7, activation='relu'))
model.add(layers.MaxPooling1D(5))
model.add(layers.Conv1D(32, 7, activation='relu'))
model.add(layers.GlobalMaxPooling1D())
model.add(layers.Dense(1))

model.summary()

model.compile(optimizer=RMSprop(learning_rate=1e-4),
              loss='binary_crossentropy',
              metrics=['acc'])
history = model.fit(x_train, y_train,
                    epochs=10,
                    batch_size=128,
                    validation_split=0.2)
```

    Model: "sequential_4"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    embedding_2 (Embedding)      (None, 500, 128)          1280000   
    _________________________________________________________________
    conv1d_4 (Conv1D)            (None, 494, 32)           28704     
    _________________________________________________________________
    max_pooling1d_2 (MaxPooling1 (None, 98, 32)            0         
    _________________________________________________________________
    conv1d_5 (Conv1D)            (None, 92, 32)            7200      
    _________________________________________________________________
    global_max_pooling1d_2 (Glob (None, 32)                0         
    _________________________________________________________________
    dense_6 (Dense)              (None, 1)                 33        
    =================================================================
    Total params: 1,315,937
    Trainable params: 1,315,937
    Non-trainable params: 0
    _________________________________________________________________
    Epoch 1/10
    157/157 [==============================] - 42s 259ms/step - loss: 0.7143 - acc: 0.5302 - val_loss: 0.6858 - val_acc: 0.5294
    Epoch 2/10
    157/157 [==============================] - 42s 265ms/step - loss: 0.6628 - acc: 0.6660 - val_loss: 0.6660 - val_acc: 0.5990
    Epoch 3/10
    157/157 [==============================] - 43s 274ms/step - loss: 0.6200 - acc: 0.7490 - val_loss: 0.6127 - val_acc: 0.7344
    Epoch 4/10
    157/157 [==============================] - 41s 263ms/step - loss: 0.5378 - acc: 0.7998 - val_loss: 0.5049 - val_acc: 0.7934
    Epoch 5/10
    157/157 [==============================] - 41s 261ms/step - loss: 0.4306 - acc: 0.8356 - val_loss: 0.4293 - val_acc: 0.8320
    Epoch 6/10
    157/157 [==============================] - 40s 253ms/step - loss: 0.3514 - acc: 0.8681 - val_loss: 0.4139 - val_acc: 0.8488
    Epoch 7/10
    157/157 [==============================] - 41s 260ms/step - loss: 0.3011 - acc: 0.8896 - val_loss: 0.4147 - val_acc: 0.8614
    Epoch 8/10
    157/157 [==============================] - 39s 251ms/step - loss: 0.2673 - acc: 0.9049 - val_loss: 0.4277 - val_acc: 0.8658
    Epoch 9/10
    157/157 [==============================] - 41s 260ms/step - loss: 0.2420 - acc: 0.9155 - val_loss: 0.4291 - val_acc: 0.8690
    Epoch 10/10
    157/157 [==============================] - 41s 258ms/step - loss: 0.2206 - acc: 0.9254 - val_loss: 0.4453 - val_acc: 0.8730



```python
history_dict = history.history
history_dict.keys()
```




    dict_keys(['loss', 'acc', 'val_loss', 'val_acc'])




```python
import matplotlib.pyplot as plt

acc = history.history['acc']
val_acc = history.history['val_acc']
loss = history.history['loss']
val_loss = history.history['val_loss']

epochs = range(1, len(acc) + 1)
#epochs = range(1, len(loss) + 1)

# "bo" is for "blue dot"
plt.plot(epochs, loss, 'bo', label='Training loss')
# b is for "solid blue line"
plt.plot(epochs, val_loss, 'b', label='Validation loss')
plt.title('Training and validation loss')
plt.xlabel('Epochs')
plt.ylabel('Loss')
plt.legend()

plt.show()
```


![png](output_63_0.png)



```python
plt.clf()   # clear figure
acc_values = history_dict['acc']
val_acc_values = history_dict['val_acc']

plt.plot(epochs, acc, 'bo', label='Training acc')
plt.plot(epochs, val_acc, 'b', label='Validation acc')
plt.title('Training and validation accuracy')
plt.xlabel('Epochs')
plt.ylabel('Loss')
plt.legend()

plt.show()
```


![png](output_64_0.png)


The model starts to overfit after about 6 epochs. It achieces a maximum accuracy of about 80% which is much better than the Dense Feed Forward model, and is comparable to that obtained by using Recurrent Neural Networks.

## Backprop for ConvNets

ConvNets can be trained using a modified version of the Backprop algorithm that was described in Chapter **TrainingNNsBackprop**. The modification, which is necessary due to the fact that multiple nodes now share the same weight parameters, is as follows:

- The forward pass of the Backprop algorithm is as before, during which we compute all the node activations.

- During the backward pass we compute the gradients $\delta_{jk}^{q}(r)$ for each node as before.

- The final computation of the gradient of the Loss Function with respect to the weight parameters is modified as follows: The gradient with respect to a weight parameter is computed as the sum of the gradients of all the connections that share the same weight.


```python
#convnet8
nb_setup.images_hconcat(["DL_images/convnet8.png"], width=600)
```




![png](output_67_0.png)



In order to justify the last rule, consider 1D Convnet in Figure **convnet8**: Focusing on the weight $w_1$, note that the gradient $\frac{\partial L}{\partial w_1}$ depends on $w_1$ through the pre-activations $a_1, a_2, a_3$ due to the parameter sharing property (this is in contrast to Fully Connected Networks where the dependence was only on $a_1$). As a result, using the chain rule we obtain:

$$
\frac{\partial L}{\partial w_1} = \frac{\partial L}{\partial a_1}\frac{\partial a_1}{\partial w_1} + \frac{\partial L}{\partial a_2}\frac{\partial a_2}{\partial w_1} + \frac{\partial L}{\partial a_3}\frac{\partial a_3}{\partial w_1}
$$

Noting that $\frac{\partial a_i}{\partial w_1}=z_i,i=1,2,3$ and $\frac{\partial L}{\partial a_i}=\delta_i$, we obtain

$$
\frac{\partial L}{\partial w_1} = z_1\delta_1 + z_2\delta_2 + z_3\delta_3
$$

The process of generating the gradients $\delta^{(r)}$ at layer $r$, from the gradients $\delta^{(r+1)}$ at layer $r+1$ was fairly straightforward in Fully Connected networks, and corresponded to a multiplication by the transpose $W^T$ of the weight matrix. In the case of ConvNets, the corresponding operation is a little more involved, and proceeds by multiplication by the transpose of the filter matrix. In order to do this efficiently using matrix multiplication, we have to pad the Activation Map (made up of gradients) by zeroes. The reader can verify this by running the operations in Figure **convnet8** backwards.

## Transfer Learning with ConvNets

When ConvNets are trained on image data, such as ImageNet, we have the luxury of having a database of millions of labeled images, which enables us to train fairly large networks with hundreds of layers to a high degree of accuracy. These networks, examples of which include ResNet, VGGNet, or Google InceptionNet, take multiple weeks to train, and involve huge amounts of advanced computing resources such as GPUs, to do so (the architecture of these networks is discussed in Chapter **ConvNetsPart2**)).

Practitioners often run into problems when there are not enough training examples to train such large networks, or if they don't have access to the necessary computing resources for the particular problem that they are trying to solve. 
Fortunately there is a technique called Transfer Learning that enables us to develop accurate models even without a lot of training data or computing resources. Transfer Learning enables us to transfer the parameters learnt from training a model for Problem 1, to be re-used in the model for another Problem 2, provided the training dataset for Problem 2 is similar to that used for Problem 1.


```python
#convnet9
nb_setup.images_hconcat(["DL_images/convnet9.png"], width=700)
```




![png](output_70_0.png)




In order to understand how Transfer Learning works, consider Figure **convnet9**. Part (a) of the figure shows a traditional ConvNet, say ConvNet 1, which has been trained on a large dataset such as ImageNet. It has a mixture of Convolutional and Maxpool layers, which is followed by Dense Feed Forward layers at the end of the network. In order to reuse the parameters learnt from this network, to another network, say Convnet 2, with a similar dataset which is much smaller in size, we do the following:

- As shown in Part (b) of Figure **convnet9**, we freeze the parameters of ALL the layers of ConvNet 1, except for the Logit Layer (called FC-1000), and then use these parameters as a Feature Extractor in ConvNet 2. The reader may recall from Chapter **LinearLearningModels** that ConvNet 2 (shown in Part(c)) corresponds to a simple Logistic Regression model with a Feature Extractor used in the Input Layer.

- In order to complete ConvNet 2, we only need to find the weights of the connections between the Feature Extractor outputs ${z_i}$ and the Output Layer ${y_i}$, as shown in Part (c) of Figure **convnet9**. Since the number of trainable weights are now much smaller, they can be estimated using the smaller dataset available for ConvNet 2 with smaller compute resources.

The Transfer Learning technique described above has been shown to be very effective in solving Image Processing problems, and has enabled the use of sophisticated ConvNet Models for a wider modeling community.


```python
#convnet10
nb_setup.images_hconcat(["DL_images/convnet10.png"], width=600)
```




![png](output_72_0.png)



If larger datasets are available for Problem 2 (but which are still smaller than ImageNet in size), then the technique that was explained above, can be extended to networks with additional layers, as shown in Figure **convnet10**). In this case we reduce the number of frozen layers from ConvNet 1, so that ConvNet 2 now has additional layers that need to be trained. Once again the frozen layers in ConvNet 1 act as a Feature Extractor whose outputs are fed into the rest of the convolutional network.

Why does Transfer Learning work so well? A ConvNet trained on a large dataset such as ImageNet, learns to recognize generic patterns and shapes that also occur in non-ImageNet data. In addition, even non-image data, such as audiowave signals, can be classified well with the patterns that are learnt with ImageNet. A general rule of thumb is that the earlier Hidden Layers in the ConvNet contain the more generic portion that can be re-used in other contexts, and the model becomes more and more specific to the particular dataset, as we go deeper into the network.

In practice, researchers can save a large amount of time (and money), by not starting from scratch, but instead use an appropriate pre-trained model, when they start working on a new model. A large number of ConvNet models pre-trained on ImageNet, including all the models discussed in this chapter, are available as part of the Model Library in Keras (https://keras.io/applications/#models-for-image-classification-with-weights-trained-on-imagenet).

The following example of Transfer Learning is taken from Chollet Section 5.3. It uses the Cats and Dogs dataset that we first encountered in Chapter **NNDeepLearning**. In that chapter we used a Dense Feed Forward Network to do the classification and obtained an accuracy of about 60%. We now solve this problem using Transfer Learning with ConvNets and obtain more than 97% accuracy.

We start by downloading a MobileNet model, whose parameters have been pre-trained on ImageNet (the design of MobileNet is discussed in Chapter **ConvNetsPart2**). Only the convolutional part of the network is downloaded into the tensor *conv_base*. The flag *include_top = false* ensures that the logit layer from MobileNet is not included in *conv_base*.


```python
from tensorflow.keras.applications import MobileNet

conv_base = MobileNet(weights='imagenet',
                  include_top=False,
                  input_shape=(160, 160, 3))
```

The summary of the downloaded model shows that it has a total of 3,206,976 trainable parameters. Also the final tensor in the model has shape (5,5,1024). 


```python
conv_base.summary()
```

    Model: "mobilenet_1.00_160"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    input_2 (InputLayer)         [(None, 160, 160, 3)]     0         
    _________________________________________________________________
    conv1 (Conv2D)               (None, 80, 80, 32)        864       
    _________________________________________________________________
    conv1_bn (BatchNormalization (None, 80, 80, 32)        128       
    _________________________________________________________________
    conv1_relu (ReLU)            (None, 80, 80, 32)        0         
    _________________________________________________________________
    conv_dw_1 (DepthwiseConv2D)  (None, 80, 80, 32)        288       
    _________________________________________________________________
    conv_dw_1_bn (BatchNormaliza (None, 80, 80, 32)        128       
    _________________________________________________________________
    conv_dw_1_relu (ReLU)        (None, 80, 80, 32)        0         
    _________________________________________________________________
    conv_pw_1 (Conv2D)           (None, 80, 80, 64)        2048      
    _________________________________________________________________
    conv_pw_1_bn (BatchNormaliza (None, 80, 80, 64)        256       
    _________________________________________________________________
    conv_pw_1_relu (ReLU)        (None, 80, 80, 64)        0         
    _________________________________________________________________
    conv_pad_2 (ZeroPadding2D)   (None, 81, 81, 64)        0         
    _________________________________________________________________
    conv_dw_2 (DepthwiseConv2D)  (None, 40, 40, 64)        576       
    _________________________________________________________________
    conv_dw_2_bn (BatchNormaliza (None, 40, 40, 64)        256       
    _________________________________________________________________
    conv_dw_2_relu (ReLU)        (None, 40, 40, 64)        0         
    _________________________________________________________________
    conv_pw_2 (Conv2D)           (None, 40, 40, 128)       8192      
    _________________________________________________________________
    conv_pw_2_bn (BatchNormaliza (None, 40, 40, 128)       512       
    _________________________________________________________________
    conv_pw_2_relu (ReLU)        (None, 40, 40, 128)       0         
    _________________________________________________________________
    conv_dw_3 (DepthwiseConv2D)  (None, 40, 40, 128)       1152      
    _________________________________________________________________
    conv_dw_3_bn (BatchNormaliza (None, 40, 40, 128)       512       
    _________________________________________________________________
    conv_dw_3_relu (ReLU)        (None, 40, 40, 128)       0         
    _________________________________________________________________
    conv_pw_3 (Conv2D)           (None, 40, 40, 128)       16384     
    _________________________________________________________________
    conv_pw_3_bn (BatchNormaliza (None, 40, 40, 128)       512       
    _________________________________________________________________
    conv_pw_3_relu (ReLU)        (None, 40, 40, 128)       0         
    _________________________________________________________________
    conv_pad_4 (ZeroPadding2D)   (None, 41, 41, 128)       0         
    _________________________________________________________________
    conv_dw_4 (DepthwiseConv2D)  (None, 20, 20, 128)       1152      
    _________________________________________________________________
    conv_dw_4_bn (BatchNormaliza (None, 20, 20, 128)       512       
    _________________________________________________________________
    conv_dw_4_relu (ReLU)        (None, 20, 20, 128)       0         
    _________________________________________________________________
    conv_pw_4 (Conv2D)           (None, 20, 20, 256)       32768     
    _________________________________________________________________
    conv_pw_4_bn (BatchNormaliza (None, 20, 20, 256)       1024      
    _________________________________________________________________
    conv_pw_4_relu (ReLU)        (None, 20, 20, 256)       0         
    _________________________________________________________________
    conv_dw_5 (DepthwiseConv2D)  (None, 20, 20, 256)       2304      
    _________________________________________________________________
    conv_dw_5_bn (BatchNormaliza (None, 20, 20, 256)       1024      
    _________________________________________________________________
    conv_dw_5_relu (ReLU)        (None, 20, 20, 256)       0         
    _________________________________________________________________
    conv_pw_5 (Conv2D)           (None, 20, 20, 256)       65536     
    _________________________________________________________________
    conv_pw_5_bn (BatchNormaliza (None, 20, 20, 256)       1024      
    _________________________________________________________________
    conv_pw_5_relu (ReLU)        (None, 20, 20, 256)       0         
    _________________________________________________________________
    conv_pad_6 (ZeroPadding2D)   (None, 21, 21, 256)       0         
    _________________________________________________________________
    conv_dw_6 (DepthwiseConv2D)  (None, 10, 10, 256)       2304      
    _________________________________________________________________
    conv_dw_6_bn (BatchNormaliza (None, 10, 10, 256)       1024      
    _________________________________________________________________
    conv_dw_6_relu (ReLU)        (None, 10, 10, 256)       0         
    _________________________________________________________________
    conv_pw_6 (Conv2D)           (None, 10, 10, 512)       131072    
    _________________________________________________________________
    conv_pw_6_bn (BatchNormaliza (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_pw_6_relu (ReLU)        (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_dw_7 (DepthwiseConv2D)  (None, 10, 10, 512)       4608      
    _________________________________________________________________
    conv_dw_7_bn (BatchNormaliza (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_dw_7_relu (ReLU)        (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_pw_7 (Conv2D)           (None, 10, 10, 512)       262144    
    _________________________________________________________________
    conv_pw_7_bn (BatchNormaliza (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_pw_7_relu (ReLU)        (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_dw_8 (DepthwiseConv2D)  (None, 10, 10, 512)       4608      
    _________________________________________________________________
    conv_dw_8_bn (BatchNormaliza (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_dw_8_relu (ReLU)        (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_pw_8 (Conv2D)           (None, 10, 10, 512)       262144    
    _________________________________________________________________
    conv_pw_8_bn (BatchNormaliza (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_pw_8_relu (ReLU)        (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_dw_9 (DepthwiseConv2D)  (None, 10, 10, 512)       4608      
    _________________________________________________________________
    conv_dw_9_bn (BatchNormaliza (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_dw_9_relu (ReLU)        (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_pw_9 (Conv2D)           (None, 10, 10, 512)       262144    
    _________________________________________________________________
    conv_pw_9_bn (BatchNormaliza (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_pw_9_relu (ReLU)        (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_dw_10 (DepthwiseConv2D) (None, 10, 10, 512)       4608      
    _________________________________________________________________
    conv_dw_10_bn (BatchNormaliz (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_dw_10_relu (ReLU)       (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_pw_10 (Conv2D)          (None, 10, 10, 512)       262144    
    _________________________________________________________________
    conv_pw_10_bn (BatchNormaliz (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_pw_10_relu (ReLU)       (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_dw_11 (DepthwiseConv2D) (None, 10, 10, 512)       4608      
    _________________________________________________________________
    conv_dw_11_bn (BatchNormaliz (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_dw_11_relu (ReLU)       (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_pw_11 (Conv2D)          (None, 10, 10, 512)       262144    
    _________________________________________________________________
    conv_pw_11_bn (BatchNormaliz (None, 10, 10, 512)       2048      
    _________________________________________________________________
    conv_pw_11_relu (ReLU)       (None, 10, 10, 512)       0         
    _________________________________________________________________
    conv_pad_12 (ZeroPadding2D)  (None, 11, 11, 512)       0         
    _________________________________________________________________
    conv_dw_12 (DepthwiseConv2D) (None, 5, 5, 512)         4608      
    _________________________________________________________________
    conv_dw_12_bn (BatchNormaliz (None, 5, 5, 512)         2048      
    _________________________________________________________________
    conv_dw_12_relu (ReLU)       (None, 5, 5, 512)         0         
    _________________________________________________________________
    conv_pw_12 (Conv2D)          (None, 5, 5, 1024)        524288    
    _________________________________________________________________
    conv_pw_12_bn (BatchNormaliz (None, 5, 5, 1024)        4096      
    _________________________________________________________________
    conv_pw_12_relu (ReLU)       (None, 5, 5, 1024)        0         
    _________________________________________________________________
    conv_dw_13 (DepthwiseConv2D) (None, 5, 5, 1024)        9216      
    _________________________________________________________________
    conv_dw_13_bn (BatchNormaliz (None, 5, 5, 1024)        4096      
    _________________________________________________________________
    conv_dw_13_relu (ReLU)       (None, 5, 5, 1024)        0         
    _________________________________________________________________
    conv_pw_13 (Conv2D)          (None, 5, 5, 1024)        1048576   
    _________________________________________________________________
    conv_pw_13_bn (BatchNormaliz (None, 5, 5, 1024)        4096      
    _________________________________________________________________
    conv_pw_13_relu (ReLU)       (None, 5, 5, 1024)        0         
    =================================================================
    Total params: 3,228,864
    Trainable params: 3,206,976
    Non-trainable params: 21,888
    _________________________________________________________________


There are two ways in which image features from the cats and dogs dataset can be extracted using the MobileNet *conv_base*:
    
1. All the images in the dataset (training, validation and test) are fed into *conv_base*, and the final tensors (of shape (5,5,1024)) is used as the new image representation. Note that the original images are no longer used in the rest of the model training and validation.
2. The model incorporates both the pre-trained *conv_base* as well as the trainable portion. Training is done using the image dataset, during which the weghts in the pre-trained portion are frozen.

Method 1 leads to faster training, since the images don't have to be processed by the large MobileNet model. However it precludes the use of data augmentation. Method 2 on the other hand is slower since each image passes through the *conv-base* in the forward pass, however it allows the user to create new images on the fly during training using data augmentation.

In this example we will use Method 1, please see Chollet Section 8.3 for an example of Method 2 as well as additional examples of Transfer Learning.


```python
import keras
import tensorflow
import numpy as np
import os, shutil, pathlib
from tensorflow.keras.utils import image_dataset_from_directory

train_dir = '/Users/subirvarma/handson-ml/datasets/cats_and_dogs_small/train'
validation_dir = '/Users/subirvarma/handson-ml/datasets/cats_and_dogs_small/validation'

train_cats_dir = '/Users/subirvarma/handson-ml/datasets/cats_and_dogs_small/train/cats'
train_dogs_dir = '/Users/subirvarma/handson-ml/datasets/cats_and_dogs_small/train/dogs'

validation_cats_dir = '/Users/subirvarma/handson-ml/datasets/cats_and_dogs_small/validation/cats'
validation_dogs_dir = '/Users/subirvarma/handson-ml/datasets/cats_and_dogs_small/validation/dogs'

new_base_dir = pathlib.Path("/Users/subirvarma/handson-ml/datasets/cats_and_dogs_small")

train_dataset = image_dataset_from_directory(
    new_base_dir / "train",
    image_size=(160, 160),
    batch_size=20)
validation_dataset = image_dataset_from_directory(
    new_base_dir / "validation",
    image_size=(160, 160),
    batch_size=20)

def get_features_and_labels(dataset):
    all_features = []
    all_labels = []
    for images, labels in dataset:
        preprocessed_images = tensorflow.keras.applications.mobilenet.preprocess_input(images)
        features = conv_base.predict(preprocessed_images)
        all_features.append(features)
        all_labels.append(labels)
    return np.concatenate(all_features), np.concatenate(all_labels)

train_features, train_labels =  get_features_and_labels(train_dataset)
val_features, val_labels =  get_features_and_labels(validation_dataset)
```

    Found 2000 files belonging to 2 classes.
    Found 1000 files belonging to 2 classes.



```python
#convnet32
nb_setup.images_hconcat(["DL_images/convnet32.png"], width=800)
```




![png](output_80_0.png)



The complete model is shown in Figure **convnet32**. During the pre-training phase, each image is passed through the MobileNet model, and its final output stored as the new training dataset. These extracted features are then converted into a vector using the Global Max Pooling operation and then sent through a simple Dense Feed Forward model with a single hidden layer with 256 nodes.


```python
inputs = keras.Input(shape=(5, 5, 1024))
x = layers.Flatten()(inputs)
x = layers.Dense(256)(x)
x = layers.Dropout(0.5)(x)
outputs = layers.Dense(1, activation="sigmoid")(x)
model = keras.Model(inputs, outputs)

model.compile(loss="binary_crossentropy",
              optimizer="rmsprop",
              metrics=["accuracy"])

history = model.fit(
    train_features, train_labels,
    epochs=100,
    validation_data=(val_features, val_labels)
    )
```

    Epoch 1/100
    63/63 [==============================] - 5s 71ms/step - loss: 6.4526 - accuracy: 0.9260 - val_loss: 1.1723 - val_accuracy: 0.9830
    Epoch 2/100
    63/63 [==============================] - 4s 67ms/step - loss: 1.1029 - accuracy: 0.9775 - val_loss: 2.1722 - val_accuracy: 0.9620
    Epoch 3/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.7706 - accuracy: 0.9855 - val_loss: 1.7282 - val_accuracy: 0.9750
    Epoch 4/100
    63/63 [==============================] - 4s 70ms/step - loss: 0.4023 - accuracy: 0.9905 - val_loss: 1.4568 - val_accuracy: 0.9780
    Epoch 5/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.3113 - accuracy: 0.9945 - val_loss: 3.8405 - val_accuracy: 0.9620
    Epoch 6/100
    63/63 [==============================] - 5s 74ms/step - loss: 0.1275 - accuracy: 0.9950 - val_loss: 2.8110 - val_accuracy: 0.9690
    Epoch 7/100
    63/63 [==============================] - 5s 78ms/step - loss: 0.1624 - accuracy: 0.9965 - val_loss: 4.2771 - val_accuracy: 0.9520
    Epoch 8/100
    63/63 [==============================] - 5s 72ms/step - loss: 0.0687 - accuracy: 0.9965 - val_loss: 1.5030 - val_accuracy: 0.9780
    Epoch 9/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.1062 - accuracy: 0.9975 - val_loss: 2.4101 - val_accuracy: 0.9670
    Epoch 10/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.1269 - accuracy: 0.9965 - val_loss: 1.5850 - val_accuracy: 0.9770
    Epoch 11/100
    63/63 [==============================] - 4s 69ms/step - loss: 2.5142e-05 - accuracy: 1.0000 - val_loss: 2.0085 - val_accuracy: 0.9740
    Epoch 12/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.0226 - accuracy: 0.9985 - val_loss: 1.7252 - val_accuracy: 0.9790
    Epoch 13/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.0062 - accuracy: 0.9995 - val_loss: 3.4487 - val_accuracy: 0.9600
    Epoch 14/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.1212 - accuracy: 0.9985 - val_loss: 1.6142 - val_accuracy: 0.9780
    Epoch 15/100
    63/63 [==============================] - 4s 68ms/step - loss: 3.4656e-11 - accuracy: 1.0000 - val_loss: 1.6149 - val_accuracy: 0.9780
    Epoch 16/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.0719 - accuracy: 0.9990 - val_loss: 1.6085 - val_accuracy: 0.9770
    Epoch 17/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.0257 - accuracy: 0.9990 - val_loss: 1.8507 - val_accuracy: 0.9750
    Epoch 18/100
    63/63 [==============================] - 4s 69ms/step - loss: 5.9659e-07 - accuracy: 1.0000 - val_loss: 2.0008 - val_accuracy: 0.9730
    Epoch 19/100
    63/63 [==============================] - 4s 69ms/step - loss: 3.2507e-08 - accuracy: 1.0000 - val_loss: 1.7860 - val_accuracy: 0.9760
    Epoch 20/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.0067 - accuracy: 0.9990 - val_loss: 2.2937 - val_accuracy: 0.9750
    Epoch 21/100
    63/63 [==============================] - 4s 67ms/step - loss: 0.0193 - accuracy: 0.9990 - val_loss: 2.4777 - val_accuracy: 0.9720
    Epoch 22/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.0597 - accuracy: 0.9985 - val_loss: 2.4879 - val_accuracy: 0.9730
    Epoch 23/100
    63/63 [==============================] - 4s 68ms/step - loss: 5.8182e-16 - accuracy: 1.0000 - val_loss: 2.4879 - val_accuracy: 0.9730
    Epoch 24/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.0132 - accuracy: 0.9990 - val_loss: 2.2678 - val_accuracy: 0.9720
    Epoch 25/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.0043 - accuracy: 0.9995 - val_loss: 2.4345 - val_accuracy: 0.9720
    Epoch 26/100
    63/63 [==============================] - 4s 70ms/step - loss: 0.0163 - accuracy: 0.9990 - val_loss: 2.2456 - val_accuracy: 0.9730
    Epoch 27/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.0231 - accuracy: 0.9990 - val_loss: 2.3544 - val_accuracy: 0.9720
    Epoch 28/100
    63/63 [==============================] - 4s 68ms/step - loss: 9.0298e-21 - accuracy: 1.0000 - val_loss: 2.3544 - val_accuracy: 0.9720
    Epoch 29/100
    63/63 [==============================] - 4s 69ms/step - loss: 3.3810e-20 - accuracy: 1.0000 - val_loss: 2.3544 - val_accuracy: 0.9720
    Epoch 30/100
    63/63 [==============================] - 4s 67ms/step - loss: 4.7015e-09 - accuracy: 1.0000 - val_loss: 2.7421 - val_accuracy: 0.9710
    Epoch 31/100
    63/63 [==============================] - 4s 68ms/step - loss: 2.0973e-11 - accuracy: 1.0000 - val_loss: 2.7532 - val_accuracy: 0.9710
    Epoch 32/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.0107 - accuracy: 0.9985 - val_loss: 3.2638 - val_accuracy: 0.9690
    Epoch 33/100
    63/63 [==============================] - 4s 70ms/step - loss: 8.5600e-04 - accuracy: 0.9995 - val_loss: 2.6681 - val_accuracy: 0.9710
    Epoch 34/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.0072 - accuracy: 0.9990 - val_loss: 2.4223 - val_accuracy: 0.9730
    Epoch 35/100
    63/63 [==============================] - 4s 69ms/step - loss: 1.0289e-22 - accuracy: 1.0000 - val_loss: 2.4223 - val_accuracy: 0.9730
    Epoch 36/100
    63/63 [==============================] - 4s 69ms/step - loss: 1.0772e-08 - accuracy: 1.0000 - val_loss: 2.5136 - val_accuracy: 0.9730
    Epoch 37/100
    63/63 [==============================] - 4s 68ms/step - loss: 1.4933e-33 - accuracy: 1.0000 - val_loss: 2.5136 - val_accuracy: 0.9730
    Epoch 38/100
    63/63 [==============================] - 4s 68ms/step - loss: 1.4144e-32 - accuracy: 1.0000 - val_loss: 2.5136 - val_accuracy: 0.9730
    Epoch 39/100
    63/63 [==============================] - 4s 68ms/step - loss: 5.3352e-12 - accuracy: 1.0000 - val_loss: 2.5136 - val_accuracy: 0.9730
    Epoch 40/100
    63/63 [==============================] - 4s 68ms/step - loss: 1.3947e-34 - accuracy: 1.0000 - val_loss: 2.5136 - val_accuracy: 0.9730
    Epoch 41/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.0177 - accuracy: 0.9990 - val_loss: 2.8212 - val_accuracy: 0.9690
    Epoch 42/100
    63/63 [==============================] - 4s 69ms/step - loss: 8.4908e-14 - accuracy: 1.0000 - val_loss: 2.8212 - val_accuracy: 0.9690
    Epoch 43/100
    63/63 [==============================] - 4s 68ms/step - loss: 7.3022e-20 - accuracy: 1.0000 - val_loss: 2.8212 - val_accuracy: 0.9690
    Epoch 44/100
    63/63 [==============================] - 4s 68ms/step - loss: 1.1595e-12 - accuracy: 1.0000 - val_loss: 2.8218 - val_accuracy: 0.9690
    Epoch 45/100
    63/63 [==============================] - 4s 69ms/step - loss: 6.2568e-29 - accuracy: 1.0000 - val_loss: 2.8218 - val_accuracy: 0.9690
    Epoch 46/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.0118 - accuracy: 0.9995 - val_loss: 2.6565 - val_accuracy: 0.9730
    Epoch 47/100
    63/63 [==============================] - 4s 68ms/step - loss: 9.1422e-11 - accuracy: 1.0000 - val_loss: 2.6847 - val_accuracy: 0.9720
    Epoch 48/100
    63/63 [==============================] - 4s 70ms/step - loss: 1.3599e-28 - accuracy: 1.0000 - val_loss: 2.6847 - val_accuracy: 0.9720
    Epoch 49/100
    63/63 [==============================] - 4s 69ms/step - loss: 1.9489e-18 - accuracy: 1.0000 - val_loss: 2.6847 - val_accuracy: 0.9720
    Epoch 50/100
    63/63 [==============================] - 4s 68ms/step - loss: 1.4235e-11 - accuracy: 1.0000 - val_loss: 2.6847 - val_accuracy: 0.9720
    Epoch 51/100
    63/63 [==============================] - 4s 69ms/step - loss: 0.0206 - accuracy: 0.9990 - val_loss: 2.4981 - val_accuracy: 0.9740
    Epoch 52/100
    63/63 [==============================] - 4s 67ms/step - loss: 0.0302 - accuracy: 0.9990 - val_loss: 3.5384 - val_accuracy: 0.9670
    Epoch 53/100
    63/63 [==============================] - 4s 67ms/step - loss: 0.0092 - accuracy: 0.9995 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 54/100
    63/63 [==============================] - 4s 67ms/step - loss: 1.2153e-20 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 55/100
    63/63 [==============================] - 4s 68ms/step - loss: 3.7367e-28 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 56/100
    63/63 [==============================] - 4s 67ms/step - loss: 8.1907e-29 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 57/100
    63/63 [==============================] - 4s 66ms/step - loss: 1.1880e-35 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 58/100
    63/63 [==============================] - 4s 66ms/step - loss: 1.1479e-23 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 59/100
    63/63 [==============================] - 4s 65ms/step - loss: 4.9519e-17 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 60/100
    63/63 [==============================] - 4s 66ms/step - loss: 2.9267e-28 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 61/100
    63/63 [==============================] - 4s 67ms/step - loss: 1.5136e-25 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 62/100
    63/63 [==============================] - 4s 67ms/step - loss: 1.8424e-15 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 63/100
    63/63 [==============================] - 4s 66ms/step - loss: 2.8300e-22 - accuracy: 1.0000 - val_loss: 2.2027 - val_accuracy: 0.9760
    Epoch 64/100
    63/63 [==============================] - 4s 66ms/step - loss: 1.8954e-13 - accuracy: 1.0000 - val_loss: 2.2028 - val_accuracy: 0.9760
    Epoch 65/100
    63/63 [==============================] - 4s 66ms/step - loss: 1.0088e-27 - accuracy: 1.0000 - val_loss: 2.2028 - val_accuracy: 0.9760
    Epoch 66/100
    63/63 [==============================] - 4s 66ms/step - loss: 1.9437e-15 - accuracy: 1.0000 - val_loss: 2.2028 - val_accuracy: 0.9760
    Epoch 67/100
    63/63 [==============================] - 4s 67ms/step - loss: 7.9112e-27 - accuracy: 1.0000 - val_loss: 2.2028 - val_accuracy: 0.9760
    Epoch 68/100
    63/63 [==============================] - 4s 67ms/step - loss: 6.2750e-24 - accuracy: 1.0000 - val_loss: 2.2028 - val_accuracy: 0.9760
    Epoch 69/100
    63/63 [==============================] - 4s 66ms/step - loss: 0.0299 - accuracy: 0.9990 - val_loss: 1.9472 - val_accuracy: 0.9800
    Epoch 70/100
    63/63 [==============================] - 4s 66ms/step - loss: 3.0759e-14 - accuracy: 1.0000 - val_loss: 1.9472 - val_accuracy: 0.9800
    Epoch 71/100
    63/63 [==============================] - 4s 67ms/step - loss: 1.9022e-21 - accuracy: 1.0000 - val_loss: 1.9472 - val_accuracy: 0.9800
    Epoch 72/100
    63/63 [==============================] - 4s 66ms/step - loss: 0.0110 - accuracy: 0.9990 - val_loss: 2.3311 - val_accuracy: 0.9780
    Epoch 73/100
    63/63 [==============================] - 4s 66ms/step - loss: 8.6561e-24 - accuracy: 1.0000 - val_loss: 2.3311 - val_accuracy: 0.9780
    Epoch 74/100
    63/63 [==============================] - 4s 67ms/step - loss: 2.6064e-12 - accuracy: 1.0000 - val_loss: 2.3311 - val_accuracy: 0.9780
    Epoch 75/100
    63/63 [==============================] - 4s 67ms/step - loss: 1.5843e-38 - accuracy: 1.0000 - val_loss: 2.3311 - val_accuracy: 0.9780
    Epoch 76/100
    63/63 [==============================] - 4s 67ms/step - loss: 1.2560e-25 - accuracy: 1.0000 - val_loss: 2.3311 - val_accuracy: 0.9780
    Epoch 77/100
    63/63 [==============================] - 4s 66ms/step - loss: 2.4363e-14 - accuracy: 1.0000 - val_loss: 2.3311 - val_accuracy: 0.9780
    Epoch 78/100
    63/63 [==============================] - 4s 66ms/step - loss: 8.9476e-24 - accuracy: 1.0000 - val_loss: 2.3311 - val_accuracy: 0.9780
    Epoch 79/100
    63/63 [==============================] - 4s 66ms/step - loss: 0.0017 - accuracy: 0.9995 - val_loss: 2.9306 - val_accuracy: 0.9690
    Epoch 80/100
    63/63 [==============================] - 4s 66ms/step - loss: 0.0049 - accuracy: 0.9995 - val_loss: 2.3392 - val_accuracy: 0.9770
    Epoch 81/100
    63/63 [==============================] - 4s 67ms/step - loss: 7.7401e-09 - accuracy: 1.0000 - val_loss: 2.1660 - val_accuracy: 0.9770
    Epoch 82/100
    63/63 [==============================] - 4s 67ms/step - loss: 7.2243e-04 - accuracy: 0.9995 - val_loss: 2.3938 - val_accuracy: 0.9710
    Epoch 83/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.0023 - accuracy: 0.9995 - val_loss: 2.7895 - val_accuracy: 0.9790
    Epoch 84/100
    63/63 [==============================] - 4s 68ms/step - loss: 1.1190e-11 - accuracy: 1.0000 - val_loss: 2.7895 - val_accuracy: 0.9790
    Epoch 85/100
    63/63 [==============================] - 4s 68ms/step - loss: 0.0123 - accuracy: 0.9995 - val_loss: 2.7567 - val_accuracy: 0.9750
    Epoch 86/100
    63/63 [==============================] - 4s 67ms/step - loss: 4.4465e-19 - accuracy: 1.0000 - val_loss: 2.7567 - val_accuracy: 0.9750
    Epoch 87/100
    63/63 [==============================] - 4s 68ms/step - loss: 5.3448e-17 - accuracy: 1.0000 - val_loss: 2.7567 - val_accuracy: 0.9750
    Epoch 88/100
    63/63 [==============================] - 4s 67ms/step - loss: 2.8541e-21 - accuracy: 1.0000 - val_loss: 2.7567 - val_accuracy: 0.9750
    Epoch 89/100
    63/63 [==============================] - 4s 66ms/step - loss: 1.1498e-04 - accuracy: 1.0000 - val_loss: 2.2622 - val_accuracy: 0.9710
    Epoch 90/100
    63/63 [==============================] - 4s 67ms/step - loss: 0.0021 - accuracy: 0.9995 - val_loss: 2.7563 - val_accuracy: 0.9770
    Epoch 91/100
    63/63 [==============================] - 4s 67ms/step - loss: 4.7979e-19 - accuracy: 1.0000 - val_loss: 2.7563 - val_accuracy: 0.9770
    Epoch 92/100
    63/63 [==============================] - 4s 67ms/step - loss: 1.1258e-25 - accuracy: 1.0000 - val_loss: 2.7563 - val_accuracy: 0.9770
    Epoch 93/100
    63/63 [==============================] - 4s 67ms/step - loss: 3.9783e-19 - accuracy: 1.0000 - val_loss: 2.7563 - val_accuracy: 0.9770
    Epoch 94/100
    63/63 [==============================] - 4s 67ms/step - loss: 8.4523e-27 - accuracy: 1.0000 - val_loss: 2.7563 - val_accuracy: 0.9770
    Epoch 95/100
    63/63 [==============================] - 4s 67ms/step - loss: 2.1673e-18 - accuracy: 1.0000 - val_loss: 2.7563 - val_accuracy: 0.9770
    Epoch 96/100
    63/63 [==============================] - 4s 66ms/step - loss: 1.0001e-23 - accuracy: 1.0000 - val_loss: 2.7563 - val_accuracy: 0.9770
    Epoch 97/100
    63/63 [==============================] - 4s 67ms/step - loss: 1.4477e-17 - accuracy: 1.0000 - val_loss: 2.7563 - val_accuracy: 0.9770
    Epoch 98/100
    63/63 [==============================] - 4s 67ms/step - loss: 4.4268e-09 - accuracy: 1.0000 - val_loss: 2.3248 - val_accuracy: 0.9760
    Epoch 99/100
    63/63 [==============================] - 4s 67ms/step - loss: 0.0000e+00 - accuracy: 1.0000 - val_loss: 2.3248 - val_accuracy: 0.9760
    Epoch 100/100
    63/63 [==============================] - 4s 67ms/step - loss: 2.5102e-23 - accuracy: 1.0000 - val_loss: 2.3248 - val_accuracy: 0.9760



```python
model.summary()
```

    Model: "model_2"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    input_5 (InputLayer)         [(None, 5, 5, 1024)]      0         
    _________________________________________________________________
    flatten_3 (Flatten)          (None, 25600)             0         
    _________________________________________________________________
    dense_11 (Dense)             (None, 256)               6553856   
    _________________________________________________________________
    dropout_2 (Dropout)          (None, 256)               0         
    _________________________________________________________________
    dense_12 (Dense)             (None, 1)                 257       
    =================================================================
    Total params: 6,554,113
    Trainable params: 6,554,113
    Non-trainable params: 0
    _________________________________________________________________



```python
history_dict = history.history
history_dict.keys()
```




    dict_keys(['loss', 'accuracy', 'val_loss', 'val_accuracy'])




```python
import matplotlib.pyplot as plt

acc = history.history['accuracy']
val_acc = history.history['val_accuracy']
loss = history.history['loss']
val_loss = history.history['val_loss']

epochs = range(1, len(acc) + 1)
#epochs = range(1, len(loss) + 1)

# "bo" is for "blue dot"
plt.plot(epochs, loss, 'bo', label='Training loss')
# b is for "solid blue line"
plt.plot(epochs, val_loss, 'b', label='Validation loss')
plt.title('Training and validation loss')
plt.xlabel('Epochs')
plt.ylabel('Loss')
plt.legend()

plt.show()
```


![png](output_85_0.png)



```python
plt.clf()   # clear figure
acc_values = history_dict['accuracy']
val_acc_values = history_dict['val_accuracy']

plt.plot(epochs, acc, 'bo', label='Training acc')
plt.plot(epochs, val_acc, 'b', label='Validation acc')
plt.title('Training and validation accuracy')
plt.xlabel('Epochs')
plt.ylabel('Loss')
plt.legend()

plt.show()
```


![png](output_86_0.png)


The Transfer Learning  model results in validation accuracy of about 97%, which is a big improvement on the 60% accuracy in the Dense Feed Forward model without feature extraction.

## References and Slides

- [Slides CNN1](https://drive.google.com/file/d/1uD01-lbUGGoPkR9ibbKyE7VzlZDu3h4W/view?usp=sharing)
- [Slides CNN2](https://drive.google.com/file/d/1pY_lAd3YiF3dwyIqjXfkO7-GuuMQF_Z-/view?usp=sharing)
