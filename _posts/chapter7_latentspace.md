# Latent Spaces: Capturing Structure in Complex Systems

## 1.0 Introduction

A few years ago, the late physicist Freeman Dyson wrote an interesting essay titled ["Why is Maxwell's theory so difficult to understand?"](https://www.damtp.cam.ac.uk/user/tong/em/dyson.pdf), in which he made the interesting observation that theory of Electro-Magnetism theory presents a picture of the world that has two layers. The first layer, which consists of the Electric and Magnetic fields that make up the theory, is entirely described using mathematical equations that govern these fields, how they interact with each other and how they evolve over time. The quantitities in this layer, namely the aformentioned fields, are abstract in nature and not accessible to our senses. The second layer on the other hand, consists of quantities such as charges, current, energy and forces that we can directly measure, and are a part of our world. 
This two layer structure is useful since it turns out that a mathematical description of the second layer by itself is intractable, but the second layer quantities can be computed from the abstract first layer quantities. Furthermore, the first layer lends itself to a mathematical description (the Maxwell's Equations of Electro-Magnetic Theory), which though complex, is still tractable. 
Dyson further observed that Quantum Mechanics, whose equations were discovered about 60 years after Maxwell's Equations, also shares this two layer structure. In this case the first layer consists of quantities such as the Schrodinger Wave Function or Quantum Fields that are once again inaccessible to our senses and measuring instruments, but nevertheless lend themselves to a mathematical description. The second layer consists of predictions about the structure of atoms, molecules and atomic processes which can be computed using the equations of Quantum Mechanics and verified using experiments. Once again a direct mathematical description at the atomic level of the second layer using quantities that we can measure, such as position and momentum, is intractable.

For both Electro-Magnetism and Quantum Mechanics, the fundamental physical processes happen in their respective first layers and are hidden from us. Scientists have tried to create a understandable model of the first layer in terms of processes and objects that are familiar to us. For example Electro-Magnetic Fields were initially modeled using a mechanical model consisting of springs while attempts have been made to model Quantum Mechanics using familiar objects such as particles and waves. However, in both cases the attempts have been unsuccessful. Dyson makes the point that the first layer is an entirely mathematical construction, and it doesn't make sense to try to reduce it to descriptions that make sense in the macro world that we live in since our language was not designed to describe the layer one processes. The main utility of the first layer is to provide a mathematically tractable model from which predictions about events in the real world can be made with a high degree of accuracy. The process by which the real world in the second layer manifests itself from the processes happening in the first layer remains largely mysterious, and in the context of Quantum Mechanics goes by names such as  Quantum Wave Collpase or Quantum Decoherence. 

My objective in this essay to explore the existence of the two layer structure as a common organizing principle that is used to structure other complex systems as well, in particular we will look at two broad domains, namely Biology and Deep Learning systems. In Biology, the DNA can be considered to the first layer structure, which by itself is fairly simple to describe, but when expressed in the language of proteins and cells by using the Genetic Code, it results in the complex second layer structure and multiplicity of living things that we find around us. The cellular machinery used to translate the layer one structures in the DNA into layer 2 structures of animals and plants is beginning to be understood thanks to the progress in Biology over the last 70 years. The patterns in the DNA itself is subject to change over time, using the Law of Natural Selection as first discovered by Charles Darwin. These laws are reasonably simple, hence are comprehensible to us, and yet they result in complex Biological structures whose origin was completely mysterious before Darwin came along.
 
In this essay I will argue that modern Deep Learning systems also obey the two layer design principle for complex systems. In this case the first layer typically goes by the name of Latent Variables. Once again these live in multi-dimensional spaces called Latent Spaces that consist of hundreds of dimensions and are not comprehensible to our senses, but they capture the structure present in objects in the real world, such as images and language, which form the second layer of the structure. The Neural Network serves as a system to translate the abstract first layer latent variables into concrete objects such as images and language that we can comprehend. 
These Neural Networks, that go by names such as Convolutional Neural Networks and Transformers, were originally inspired by models of how the human brain functions, even though the underlying mechanisms are very different in the two cases. By modifying Latent Variables we are able to carry out complex manipulations of images and text that was not possible before. Moreover we can solve the difficult problem of translating between dissimilar datasets by establishing a correspondence between their Latent Spaces, an example of which is generating an image by describing it in words.

This also raises the interesting question of whether the brain itself is organized according to the two layer design principle. It could be that information is organized in the brain in multi-dimensional layer one structures, which are then converted into the three dimensional space that we perceive and words that we understand, using the brain's Neural Network. 

The rest of this essay is organized as follows: In Section 2.0 I discuss what we know about Latent Variables in the context of images, the Neural Network Architectures used to generate them, and how they are utilized in practice. Section 3.0 is on the topic of Latent Variables in Natural Language Processing (NLP), and also the connection between Image and NLP Latent Variables. In Section 4.0 we cast the DNA and Genes in Biological Cells into the language of Latent Variables, and describe how these get expressed into the living structures that we see around us. In Section 5.0 we discuss Latent Variables in the contexts of Physics, and finally in Section 6.0 we end the essay with some remarks on the role Latent Variables play in the operation of the brain.

## Why the Big Deal over Latent Vectors and Latent Spaces

As we will see in the next section, Neural Networks map images or text into a n-dimensional Latent Vector (x_1, x_2,...,x_n), and the set of all such points from the dataset form a manifold. The Latent Vector by itself is not that interesting, the magic happens when it is used to various things such as:

- Latent Vectors can be used to do classification
- Latent Vectors can be fed back into the Neural Network to generate new images or text (so called Generative AI)
- Latent Vectors can be used for control
- Latent Vectors can be used to do optimization

These are just some of the uses that have been found so far, and I am sure there are many more that will be unearthed in the coming years. Latent Vectors by themselves are just points in n-dimensional space, and require Neural Networks to generate them, and also to translated them back into the world of images or text. Hence one can argue that the real intelligence to do these tasks resides in the Neural Network, which is true. The real power of the Latent Space lies in the fact that it is able to capture structure in the input datasets. This structure is hidden from our comprehension, whether in images or in language, but becomes apparant when the data is translated into Latent Vectors. This structure is often tied to the semantic content in the datasets, which is something that was not possible to do before.

For example one of the early observations in Deep Learning is that images that are similar to each other or text that has similar meaning result in Latent Vectors that lie close to each other, which makes is easier to do classification. Moreover by establishing a correspondence between Latent Spaces from two different datasets, for example images and text, it is possible to translate from one dataset to another. This property drives models such as DALLE 2 that generate images from text descriptions. The use of Latent Vectors for control also relies on the property that input states with similar control signals cluster together.

The most fascinating aspect of Latent Spaces that has been discovered, is that Latent Spaces for Images and Text are the same in a very fundamental way. In other words one can start from a Latent Vector and translate it into an image or piece of text which are semantiacelly equivalent. The trainig process process can be considered to be taking two Latent Spaces and superimposing them on each other until they match. This would not possible unless they are topologically similar (or isomorphis).

The Encoder Neural Network in some sense extracts everything that there is to know about a dataset, and then compresses it down to its essentials, and this representation is the Latent Space. Until now datasets were represented by statistics like the average or standard deviation, or if more ambitious its moments. But clearly we now have a better way of doing this. Once we have this representation we can do things that were impossible to do before, including generating new samples similar to the ones in the original dataset (which goes back to Feynman's quote "I truly don't understant something unless I am able to make it myself"). Such a representation was not possible before, and its implications are still percolating through Science and Engineering. In addition to text and images, there are other complex systems over whom we have limited control since our understanding is limites, things like the Economy, Financial markets etc 

## Latent Space for Images 

Due to the advances in Deep Learning in the last decade, we now have the technology to be able to conjure up images by simply describing them in words, or manipulate an image by using simple numerical rules. But how did we get to this point? Not so long ago, the only way to manipulate images was by modifying the hundreds of thousands of color pixels that make up an image, which is an extremely difficult undertaking. Clearly images have a lot of underlying structure, which should help in manipulating them, but we had no way to discover this structure. Examples of such structures would be: A car image is made up of a chassis, which is turn has components such as doors, windows, seats etc or a human image is made up limbs, head, face, etc the face in turn has eyes, lips, nodse etc and limbs have joints, toes and fingers. Thus what was missing was a semantic level understaing of images, which would allow us to find similar images or manipulate the objects of an image in a simple way.

![](https://subirvarma.github.io/GeneralCognitics/images/lat1.png) 

Figure 1: Mapping between images and their Latent Vectors

Fig. 1 shows a mapping between images and their latent vector representations. The image itself is described by three 2D planes of red, green abd blue pixels, each picel can take values from 0 to 255. The latent representation on the other is just a N dimensional vector. The magic lies in the neural networks that convert an image to its corresponding latent vector, and more importantly, are also able to convert a latent vector back into an image. Using the terminology from the Introduction, the latent vector is the Layer 1 representation of images. As we show later is this section, this representation can be used to carry out several image manipulation tasks that were impossible to accomplish before the advent of Deep Learning. 

![](https://subirvarma.github.io/GeneralCognitics/images/lat27.png) 

Figure 2: Generating Latent Vectors for images 

Figure 2 shows a block diagram of how a Neural Network is trained to generate Latent Vectors. Part (a) of the figure shows the training process. In general there are two Neural Networks involved, the Encoder network takes an image and converts in into a vector, while the Decoder network does the reverse operation in a such a way such that the original image is recovered. Once the Encoder and Decoder have been fully trained (using a training dataset with millions of images), the Decoder by itself can be used to generate new images, as shown in Part (b) of the diagram. From this description it is clear fundamental to the operation of this system is the idea of compression, since the Encoder is taking an image consisting of hundreds of thousands of pixels and converting it into a vector with a few hundred dimensions. In order to do so the Encoder has to capture the essence of the image, both the semantics (the various shapes of the objects in the image) and the texture (colors etc), and do it in such a way that all extranuous information is filtered out. 

Over the course of the last decade, the Encoder and Decoder networks have become more sophisticated resulting in better images. Initially they were just Dense Feed Forward Networks, the use of Convolutional Networks (CNNS) led to big jump in performance. The latest systems employ a technique called Diffusion Models for the Decoder which has led to the creation of State of the Art systems like DALLE 2. 

What is the theoretical basis for believing that an invertible Latent Vector representation for images is even possible? The crux of the matter is that the system is able to capture the probability distribution of the pixels in the images. This is an extremely complex function, which we were unable to capture before the advent of Neural Networks, and even now its parameters are stored in the hundreds of millions of weights in the Neural Network, i.e. the network itself is the representation for the Distribution Function. The Decoder then inverts this Distribution Function in order to sample from it, which results in the generation of new images. An Neural Networks have improved and become more sophisticated, they have been able to capture more complex Functions and as a result the quality of images that they are able to generate has become better.

![](https://subirvarma.github.io/GeneralCognitics/images/lat2.png) 

Figure 3: Visualization of a Latent Space manifold

A manifold is defined as a surface in N dimensional space that can be locally approximated by Euclidean space. Moreover, given two points on a manifold, they can be connected by a linear segment all of whose points also lie on the manifold.
The Latent Space forms a complicated manifold in N dimensional space which doesn't lend itself to easy visualization. If the Latent Vector has only three dimensions, the the manifold can be visualized, and once such manifold is shown in Fig. 3.

There is a technique that sometimes helps in visualizing Latent Space manifolds in higher dimensions, and this is discussed next.

![](https://subirvarma.github.io/GeneralCognitics/images/lat28.png) 

Figure 4: Projection of the MNIST Latent Variable manifold on to 2D space

The MNIST image dataset consists of handwritten digits from 0 to 9 and has been extensively used from the earliest days of Deep Learning. Some samples from this dataset are shown in the LHS of Fig. 4. Latent Variables for this dataset were obtained using a technique called VAE (Variational Auto Encoders), and then these were projected onto 2 dimensions using a technique called T-SNE as shown on the RHS of Fig. 4. 
The figure shows why Latent Space representaions are useful: Note that the Latent Variables occur in ten distinct clusters, and indeed images from each distinct digit gets mapped to its own cluster. This shows that the system has managed to figure out that there are ten distinct types of shapes in the dataset.
This representation makes it much easier to classify digits by separating out each cluster using simple hiper-plane separators.

![](https://subirvarma.github.io/GeneralCognitics/images/lat29.png) 

Figure: Interpolation between two images 

![](https://subirvarma.github.io/GeneralCognitics/images/lat30.png) 

Figure: Manipulation of images by doing vector arithemetic in Latent Space


## Latent Space for Text

![](https://subirvarma.github.io/GeneralCognitics/images/lat31.png) 

Figure 5: Text generation using a Language Model

Just as for images, textual data can also be transformed into its Latent Vector representation as shown in Fig. 5. Each word in the Input can be converted into its corresponding Latent Vector, and a Latent Vector for the entire Input can then be obtained by further transforming this sequence of vectors using a Dense Feed Forward network. The best current way of computing Text Latent Vectors is by means of Neural Networks called Transformers. 

New text is generated by a combination of Encoder and Decoder in an Autoregressive manner, i.e., words are generated one at a time, and the newly generated word is fed back into the decoder in order to generate the next word. Typical applications of this system are to generate summaries of input text, or to generate answers to questions. It is also possible to combine the Encoder and Decoder into the same system, in which case the resulting system is called a Language Model. These systems are trained using next word prediction, while the decoding is once again in an autoregressive fashion.

![](https://subirvarma.github.io/GeneralCognitics/images/lat18.png) 

Figure 6: T-SNE projections for word Latent Vectors

Latent Vectors for text are mapped as a function of their semantic content. This is illustrated in Fig 6, which shows latent space representations for single words. We can see that words which are close in meaning have latent vectors that are close to each other.

## Translation between Datasets

One of the most fascinating discoveries of the Deep Learning era is the realization that we can map between very dissimilar datasets by connecting their Latent Spaces together. Indeed the training process works such that literally the datasets share a common Latent Space, i.e., it is possible to generate a sample from either Dataset 1 or Dataset 2, depending upon the Neural Network deployed as the decoder. In translation applications a sample from dataset 1 is converted into its Latent Vector, which is then directly used to generate a sample from Dataset 2. 

The power of the latent space formulation is most evident when we try to solve the problem of translating between two datasets that are very different from each other at the surface level. However it turns out that if they share a similar structure at the deeper Latent Space level, then it is possible to 'translate' an object in dataset 1 to a corresponding object in dataset 2 in a way that makes sense to us. The most common example of this translating a piece of text to an image that is described by the text. Other examples include:

- Translating from image to text, also known as captioning
- Translating text from Language 1 to Language 2
- Translating from Image Class 1 to Image Class 2: For example converting satellite photos into road maps
- Converting a piece of text to its summary
- Answering a question (tranlating between the question and the answer)

These problems, which also go under the name of Generative AI, have been very difficult to solve using older methods. 

![](https://subirvarma.github.io/GeneralCognitics/images/lat35.png) 

Figure: Establishing a 1-1 mapping between two Latent Spaces

Fig. 9a summarizes the main idea behind this technique as applied to text and image datasets: Each of these datasets has its own Latent Space. During the training process, we establish a correspondence between points of the two Latent Spaces. This is done explicitly using algorithmd such as CLIP, or implicitly as part of the training process that is used to convert from text to images. The Latent Spaces themselves have some complex topological structure about which we know very little, but the fact that the two of them can be put into one-to-one correspondence seems to imply that at the very deep level they are identical. This is plausible when two datasets are from two different languages, and this fact is used to do lnaguage translation. However the fact that images and text are also deeply connected at the Latent Space level is, in my opinion, one of the important discoveries that we have made thanks to Deep Learning, and it has implications in the study of how information is stored in the brain. 

This technique of establishing congruences between datasets, and thus converting between them, is juest getting started, and can be extended in a number of exciting directions. One possible extension is translating between a digital dataset and objects in the real world. In a later section I will argure that living things are an example of such a translation, between the Latent Space of DNA and our bodies and organs.

![](https://subirvarma.github.io/GeneralCognitics/images/lat38.png) 

Figure: A Latent Vector used to generate either text or an image



![](https://subirvarma.github.io/GeneralCognitics/images/lat36.png) 

Figure: Converting a piece of text to an image

Once this is done, translation from a sample from one of the datasets to a sample in the other can be done by generating the Latent Vector 1 for the Dataset 1 sample, and then using this to generate the corresponding Latent Vector 2 for Dataset 2 that is closest to it (in practice this is done automatically by the generating Neural Network). Latent Vector 2 can then be used to generate the sample we are looking for in Dataset 2. Before the advent of modern Neural Networks, it was not thought possible to translate from a Latent Vector representation to full fledged image or a piece of text that is semantically coherent due to the complexity of the mathematical transformation required. Deep Learning has s hown us a way of learning these fantastically complex functions, and as result we are able to generate samples from datasets which was previously the domain of human level intelligence.

![](https://subirvarma.github.io/GeneralCognitics/images/lat37.png) 

Figure: Translating between languages

If the two Datasets have the same modality (for example image to image or text to text), then this procedure establishes a correspondence between two versions of the same Latent Vector space.

##  Control in Latent Space

In the previous section we showed how we can solve the difficult problem of translating between dissimilar datasets by establishing a correspondence between their Latent Spaces. There are other intractable problems whose solution is simplified by operating in their Latent Spaces, and in this section we will consider the problem of Control. 

One way of formulating the problem of Optimal Control is as a multistep problem, where an Agent tries to maximize an objective, usually called a Reward. At each step the Agent has access to the state S of the world in which it operating, and has to decide to take one of several Actions A that are available to it. Furthermore the Agent's Action causes the state S of the world to change in an unpredictable way. The Agent's Action A can be formulated as a function f of its current state S, so that $A = f(S)$, for a class of problems called Markov Decision Processes.

![](https://subirvarma.github.io/GeneralCognitics/images/lat40.png) 

Figure: Using Latent Variables for Control

For the case when the control actions are based on visual information from the real world, the state S can be simply considered to be the images being fed to the controller from a camera, susch a setup is appropriate for robotic control for exampele. Before the advent of Deep Learning it was not possible to feed such a complex state into the controller, usually the information in the image was condensed into a few numbers that the controller could handle. Deep Learning systems on the other hand are able to process the hundreds of thousands of pixels in images, and derive control information from them. This is shown in the figure above. Once again the Latent Space plays a critical role by serving as the condensed representation of the structure present in the images, as specialized to the task of control. the control actions can be directly mapped to the Latent Space, such that images that have the same control action are clustered together.

![](https://subirvarma.github.io/GeneralCognitics/images/lat25.png) 

Figure: The Latent Space for Screens Shots for the Atari game of Space Invaders

An example of this Latent Space for the Atari game of Space Invaders in shown in Fig. (after being mapped into 2D space using the T-SNE method). Each point in the graph corresponds to a Latent Variable representation of one of the Game Screens, while the its color corresponds to something called a Value Function, which is the system's estimate of the Reward that it may get during the game. This graph clearly shows that the Neural Network has been able to find a structure in the game screens as a function of the 'Reward that the screen generates', which has enabled it to map them such that screens that have similar Rewards cluster together in the Latent Space. 

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














