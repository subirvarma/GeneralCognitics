# Latent Spaces: Capturing Structure in Complex Systems

## 1.0 Introduction

A few years ago, the late physicist Freeman Dyson wrote an interesting essay titled ["Why is Maxwell's theory so difficult to understand?"](https://www.damtp.cam.ac.uk/user/tong/em/dyson.pdf), in which he made the interesting observation that theory of Electro-Magnetism theory presents a picture of the world that has two layers. The first layer, which consists of the Electric and Magnetic fields that make up the theory, is entirely described using mathematical equations that govern these fields, how they interact with each other and how they evolve over time. The quantitities in this layer, namely the aformentioned fields, are abstract in nature and not accessible to our senses. The second layer on the other hand, consists of quantities such as charges, current, energy and forces that we can directly measure, and are a part of our world. 
This two layer structure is useful since it turns out that a mathematical description of the second layer by itself is intractable, but the second layer quantities can be computed from the abstract first layer quantities. Furthermore, the first layer lends itself to a mathematical description (the Maxwell's Equations of Electro-Magnetic Theory), which though complex, is still tractable. 
Dyson further observed that Quantum Mechanics, whose equations were discovered about 60 years after Maxwell's Equations, also shares this two layer structure. In this case the first layer consists of quantities such as the Schrodinger Wave Function or Quantum Fields that are once again inaccessible to our senses and measuring instruments, but nevertheless lend themselves to a mathematical description. The second layer consists of predictions about the structure of atoms, molecules and atomic processes which can be computed using the equations of Quantum Mechanics and verified using experiments. Once again a direct mathematical description at the atomic level of the second layer using quantities that we can measure, such as position and momentum, is intractable.

For both Electro-Magnetism and Quantum Mechanics, the fundamental physical processes happen in their respective first layers and are hidden from us. Scientists have tried to create a understandable model of the first layer in terms of processes and objects that are familiar to us. For example Electro-Magnetic Fields were initially modeled using a mechanical model consisting of springs while attempts have been made to model Quantum Mechanics using familiar objects such as particles and waves. However, in both cases the attempts have been unsuccessful. Dyson makes the point that the first layer is an entirely mathematical construction, and it doesn't make sense to try to reduce it to descriptions that make sense in the macro world that we live in since our language was not designed to describe the layer one processes. The main utility of the first layer is to provide a mathematically tractable model from which predictions about events in the real world can be made with a high degree of accuracy. The process by which the real world in the second layer manifests itself from the processes happening in the first layer remains largely mysterious, and in the context of Quantum Mechanics goes by names such as  Quantum Wave Collpase or Quantum Decoherence. 

My objective in this essay to explore the existence of the two layer structure as a common organizing principle that is used to structure other complex systems as well, in particular we will look at two broad domains, namely Biology and Deep Learning systems. In Biology, the DNA can be considered to the first layer structure, which by itself is fairly simple to describe, but when expressed in the language of proteins and cells by using the Genetic Code, it results in the complex second layer structure and multiplicity of living things that we find around us. The cellular machinery used to translate the layer one structures in the DNA into layer 2 structures of animals and plants is beginning to be understood thanks to the progress in Biology over the last 70 years. The patterns in the DNA itself is subject to change over time, using the Law of Natural Selection as first discovered by Charles Darwin. These laws are reasonably simple, hence are comprehensible to us, and yet they result in complex Biological structures whose origin was completely mysterious before Darwin came along.
 
In this essay I will argue that modern Deep Learning systems also obey the two layer design principle for complex systems. In this case the first layer typically goes by the name of Latent Variables. Once again these live in multi-dimensional spaces called Latent Spaces that consist of hundreds of dimensions and are not comprehensible to our senses, but they capture the structure present in objects in the real world, such as images and language, which form the second layer of the structure. The Neural Network serves as a system to convert the abstract first layer latent variables into concrete objects such as images and language that we can comprehend. 
These Neural Networks, that go by names such as Convolutional Neural Networks and Transformers, were originally inspired by models of how the human brain functions, even though the underlying mechanisms are very different in the two cases. By manipulating the Latent Variables that these models create, we are able to carry out complex transformations of images that was not possible before. Moreover by connecting the the Latent Spaces of images and language, we can generate new images by describing them in words.

This also raises the interesting question of whether the brain itself is organized according to the two layer design principle. It could be that information is organized in the brain in multi-dimensional layer one structures, which are then converted into the three dimensional space that we perceive and words that we understand, using the brain's Neural Network. 

The rest of this essay is organized as follows: In Section 2.0 I discuss what we know about Latent Variables in the context of images, the Neural Network Architectures used to generate them, and how they are utilized in practice. Section 3.0 is on the topic of Latent Variables in Natural Language Processing (NLP), and also the connection between Image and NLP Latent Variables. In Section 4.0 we cast the DNA and Genes in Biological Cells into the language of Latent Variables, and describe how these get expressed into the living structures that we see around us. In Section 5.0 we discuss Latent Variables in the contexts of Physics, and finally in Section 6.0 we end the essay with some remarks on the role Latent Variables play in the operation of the brain.

## Latent Space for Images 

Due to the advances in Deep Learning in the last decade, we now have the technology to be able to conjure up images by simply describing them in words, or manipulate an image by using simple numerical rules. But how did we get to this point? Not so long ago, the only way to manipulate images was by modifying the hundreds of thousands of color pixels that make up an image, which is an extremely difficult undertaking. Clearly images have a lot of underlying structure, which should help in manipulating them, but we had no way to discover this structure. Examples of such structures would be: A car image is made up of a chassis, which is turn has components such as doors, windows, seats etc or a human image is made up limbs, head, face, etc the face in turn has eyes, lips, nodse etc and limbs have joints, toes and fingers. Thus what was missing was a semantic level understaing of images, which would allow us to find similar images or manipulate the objects of an image in a simple way.

![](https://subirvarma.github.io/GeneralCognitics/images/lat1.png) 

Figure 1: Mapping between images and their Latent Vectors

Fig. 1 shows a mapping between images and their latent vector representations. The image itself is described by three 2D planes of red, green abd blue pixels, each picel can take values from 0 to 255. The latent representation on the other is just a N dimensional vector. The magic lies in the neural networks that convert an image to its corresponding latent vector, and more importantly, are also able to convert a latent vector back into an image. The latent vector is the layer 1 representation of images, using the terminology we used in the Introduction. As we show later is this section, this representation can be used to carry out several image manipulation tasks that were impossible to accomplish before the advent of Deep Learning. 

What is the theoretical basis for believing that an invertible latent vector representation for images is even possible?

![](https://subirvarma.github.io/GeneralCognitics/images/lat17.png) 

Figure 2: Theory underlying generation of images using their Latent Vector representations 

The theory behind these representations is summarized in Fig. 2. Assuming we have a collection of images, and we would like to generate new images that look they also belong to this group. One way of doing this is by estimating the distribution q(X) for the image data, and then sampling from q(X). However in general q(X) is an extremely complicated function, and so far it is difficult to estimate it directly. However it is easier to estimate the conditional probability q(X|Z) where Z is the Latent Variable. Indeed q(X|Z) can be approximated by a Gaussian Distribution whose mean can be estimated using a Neural Network.
Finally using the fact that q(X,Z) = q(X|Z) q(Z), we can use Ancestral Sampling to sample from q(X,Z) (and thereby generating an image) by first sampling from q(Z) and then using the sampled value of Z to sample from q(X|Z). The theory I have just described underlies popular image generation models such as DALLE 2 and Stable Diffusion.

![](https://subirvarma.github.io/GeneralCognitics/images/lat2.png) 

Figure 3: Visualization of a Latent Space manifold

The Latent Space forms a complicated manifold in N dimensional space which doesn't leand itself to visualization. Fig. 3 show a Latent Space manifold for N = 3.
A manifold is defined as a surface in N dimensional space that can be locally approximated by Euclidean space. Moreover, given two points on a manifold, they can be connected by a linear segment all of whose points also lie on the manifold.

There is a technque that sometimes helps in visualizing Latent Space manifolds, and this is discussed next.

![](https://subirvarma.github.io/GeneralCognitics/images/lat3.png) 

Figure 4: Projection of the MNIST Latent Variable manifold on to 2D space

The MNIST image dataset consists of handwritten digits from 0 to 9 and has been extensively used from the earliest days of Deep Learning. Latent Variables for this dataset was obtained using a technique called VAE (Variational Auto Encoders), and then these were projected onto 2 dimensions using a technique called T-SNE. 

This figure also shows why Latent Space representaions are useful: Note that the Latent Variables occur in ten distinct clusters, and indeed images from each distinct digit gets mapped to its own cluster. This is a very useful property since it is now much easier to classify digits by separating out each cluster using simple hiper-plane separators.

Insert: Manipulation of images by direct vector operations

![](https://subirvarma.github.io/GeneralCognitics/images/lat9.png) 

Figure: Generation of multiple images with similar semantic content

![](https://subirvarma.github.io/GeneralCognitics/images/lat10.png) 

Figure: Interpolation between two images

## Latent Space for Text

![](https://subirvarma.github.io/GeneralCognitics/images/lat4.png) 

Figure 5: Latent Vector representations for text

Just as for images, textual data can also be transformed into its Latent Vector representation as shown in Fig. 5, and in the other direction, Latent Vector representations can be transformed back into text.

![](https://subirvarma.github.io/GeneralCognitics/images/lat18.png) 

Figure 6: T-SNE projections for word Latent Vectors

Latent Vectors for text are mapped as a function of their semantic content. This is illustrated in Fig 6, which shows latent space representations for single words. We can see that words which are close in meaning have latent vectors that are close to each other.


![](https://subirvarma.github.io/GeneralCognitics/images/lat19.png) 

Figure 7: An Encoder tor Text

The best encoders for text are based on the Transformer architecture (see Fig. 7). After being initially encoded using an word based text encoder such as Word2Vector, the text to be encoded is fed into the Transformer model. The Transformers's architecture enables the vector representation of each word to be modified as a function of the other words in the text to which it is connected semantically (there can be more than one such connection per word to multiple other words). This process is repeated multiple times in order to get the final representation. Unlike the Word2Vector representation that we started out with, the final representation of each word takes the context of the surrounding text into account.

![](https://subirvarma.github.io/GeneralCognitics/images/lat20.png) 

Figure 8: An Encoder and Decoder for Text

The decoder is also based on the Transformer model, and it generates its output on a word by word basis, which is known as auto-regressive generation. In order to generate the output, the decoder is usually suppled with a context, which in this case is another sentence that has also been encoded using a Transformer. This enables this system to perform a number of useful tasks such as Translation, Summarization, Question-Answering etc.

## Translation between Datasets

![](https://subirvarma.github.io/GeneralCognitics/images/lat24.png) 

Figire 9a: Mapping between two Datasets

The power of the latent space formulation is most evident when we try to solve the problem of translating between two datasets that are very different from each other at the surface level. However it turns out that if they share a similar structure at the deeper Latent Space level, then it is possible to 'translate' an object in dataset 1 to a corresponding object in dataset 2 in a way that makes sense to us. The most common example of this translating a piece of text to an image that is described by the text. Other examples include:

- Translating from image to text, also known as captioning
- Translating text from Language 1 to Language 2
- Translating from Image Class 1 to Image Class 2: For example converting satellite photos into road maps
- Converting a piece of text to its summary
- Answering a question (tranlating between the question and the answer)

These problems, which also go under the name of Generative AI, have been very difficult to solve using older methods. Fig. 9a summarizes the main idea behind this technique: There are two datasets each of which has its own Latent Space. During the training process, we establish a correspondence between points of the two Latent Spaces. Once this is done, translation from a sample from one of the datasets to a sample in the other can be done by generating the Latent Vector 1 for the Dataset 1 sample, and then using this to generate the corresponding Latent Vector 2 for Dataset 2 that is closest to it (in practice this is done automatically by the generating Neural Network). Latent Vector 2 can then be used to generate the sample we are looking for in Dataset 2. Before the advent of modern Neural Networks, it was not thought possible to translate from a Latent Vector representation to full fledged image or a piece of text that is semantically coherent dur to the complexity of the mathematical transformation required. Deep Learning has s hown us a way of learning these fantastically complex functions, and as result we are able to generate samples from datasets which was previously the domain of human level intelligence.


If the two Datasets have the same modality (for example image to image or text to text), then this procedure establishes a correspondence between two versions of the same Latent Vector space.

![](https://subirvarma.github.io/GeneralCognitics/images/lat5.png) 

Figure 9b: Mapping between image and text Latent Spaces to enable text to image models

Text to image models such as DALLE 2 and Stable Diffusion were released towards the end of 2022. In order to function, these models have to connect the Latent Spaces for text and images so that the semantic content in the text is reflected in the corresponding image. 

![](https://subirvarma.github.io/GeneralCognitics/images/lat7.png) 

Figure 10: Operation of the CLIP model for joint image and text Latent Variable generation

It is possible to establish a correspondence between the image and text Latent Spaces. The main idea for this is illustrated in Fig. 10 (for 2D projections). This can be accomplished using a model called CLIP. At the start of the training, the corresponding Latent Vectors are not near each other, but as the training progresses they move loser as shown in the RHS of the figure. As a result of this procedure images and text are embedded on to the same latent space, whic is very convenient is we want to convert from one space to another. 

![](https://subirvarma.github.io/GeneralCognitics/images/lat8.png) 

Figure 11: Generation of images from text in DALLE 2

Fig. 11 shows how images are generated from text in DALLE 2. The text is first converted into its latent vector representation using the CLIP encoder. Another model is used to find the corresponding CLIP atent vector representation for the image such that the two latent vectors are close to each other. Finally the image latent vector is fed into a Diffusion model that converts it into a full scale image.
Sme of the other text to image models such as Imagen and Stable Diffusion feed the text latent vector directly into the Diffusion model that produces the image. this avoiding the extra step of estimating the image Latent Vector. However the model used to generate the text latent vector is not the CLIP model, but much larger models such as BERT that have been trained on much text training datasets. 


##  Control in Latent Space

In the previous section we showed how we can solve the difficult problem of translating between dissimilar datasets by establishing a correspondence between their Latent Spaces. There are other intractable problems whose solution is simplified by operating in their Latent Spaces, and in this section we will consider the problem of Optimal Control.

One way of formulating the problem of Optimal Control is as a multistep problem, where an Ageent tries to maximize an objective, usually called a Reward. At each step the Agent has access to the state S of the world in which it operating, and has to decide to take one of several Actions A that are available to it. Furthermore the Agent's Action causes the state S of the world to change in an unpredictable way. The Agent's Action A can be formulated as a function f of its current state S, so that $A = f(S)$, for a class of problems called Markov Decision Processes.

![](https://subirvarma.github.io/GeneralCognitics/images/lat25.png) 

Figure: The Latent Space for Screens Shots for the Atari game of Space Invaders

Consider the problem owhere the Agent is tasked with playing a video game. The State S that it has access to consists of current and perhaps the past few screens of the game, while the Actions correspond to manipulations of the game controller. Given that the number of possible States is some uncountably large number, before that advent of Deep Learning the solution to this problem was intractable. A few years ago the company Deep Mind came up with a system they called DQN (for Deep Q Networks) that actually solved this problem for case of Atari games. Their solution involved training a Neural Network to implement the control function f. The input into the Neural Network was the last 4 screens of the game, while its output was a prediction of the Game Controller A. Once again this network processed the input image and converted its hundreds of thousands of pixels into a vector in Latent Space, which was then mapped onto one of the control Actions. An example of this Latent Space for the game of Space Invaders in shown in Fig. (after being mapped into 2D space using the T-SNE method). Each point in the graph corresponds to a Latent Variable representation of one of the Game Screens, while the its color corresponds to something called a Value Function, which is the system's estimate of the Reward that it may get during the game. This graph clearly shows that the Neural Network has been able to find a structure in the game screens as a function of the 'Reward that the screen generates', which has enabled it to map them such that screens that have similar Rewards cluster together in the Latent Space. This is clearly a very property of the Latent Space, and enables the Neural Network to generate control Actions for complex State Spaces.

## Optimization in Latent Space

![](https://subirvarma.github.io/GeneralCognitics/images/lat26.png) 

Figure: Optimization in Latent Space



## Is the Quantum Wave Vector a Latent Variable?

![](https://subirvarma.github.io/GeneralCognitics/images/lat21.png) 

Figure 14: Possible locations for an electron in the crystal lattice



![](https://subirvarma.github.io/GeneralCognitics/images/lat22.png) 

Figure 15: Interpretation of the Quantum State as a Latent Vector



![](https://subirvarma.github.io/GeneralCognitics/images/lat23.png) 

Figure 16: Decoding real world information from the Quantum State




## DNA: Latent Variable for Life?

![](https://subirvarma.github.io/GeneralCognitics/images/lat13.png) 



![](https://subirvarma.github.io/GeneralCognitics/images/lat14.png) 



![](https://subirvarma.github.io/GeneralCognitics/images/lat15.png) 




## Latent Spaces in Brains














