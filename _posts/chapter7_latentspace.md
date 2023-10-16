# Latent Spaces: Capturing Structure in Complex Systems

## 1.0 Introduction

A few years ago, the late physicist Freeman Dyson wrote an interesting essay titled ["Why is Maxwell's theory so difficult to understand?"](https://www.damtp.cam.ac.uk/user/tong/em/dyson.pdf), in which he made the interesting observation that theory of Electro-Magnetism theory presents a picture of the world that has two layers. The first layer, which consists of the Electric and Magnetic fields that make up the theory, is entirely described using mathematical equations that govern these fields, how they interact with each other and how they evolve over time. The quantitities in this layer, namely the aformentioned fields, are abstract in nature and not accessible to our senses. The second layer on the other hand, consists of quantities such as charges, current, energy and forces that we can directly measure, and are a part of our world. 
This two layer structure is useful since it turns out that a mathematical description of the second layer by itself is intractable, but the second layer quantities can be computed from the abstract first layer quantities. Furthermore, the first layer lends itself to a mathematical description (the Maxwell's Equations of Electro-Magnetic Theory), which though complex, is still tractable. 
Dyson further observed that Quantum Mechanics, whose equations were discovered about 60 years after Maxwell's Equations, also shares this two layer structure. In this case the first layer consists of quantities such as the Schrodinger Wave Function or Quantum Fields that are once again inaccessible to our senses and measuring instruments, but nevertheless lend themselves to a mathematical description. The second layer consists of predictions about the structure of atoms, molecules and atomic processes which can be computed using the equations of Quantum Mechanics and verified using experiments. Once again a direct mathematical description at the atomic level of the second layer using quantities that we can measure, such as position and momentum, is intractable.

For both Electro-Magnetism and Quantum Mechanics, the fundamental physical processes happen in their respective first layers and are hidden from us. Scientists have tried to create a understandable model of the first layer in terms of processes and objects that are familiar to us. For example Electro-Magnetic Fields were initially modeled using a mechanical model consisting of springs while attempts have been made to model Quantum Mechanics using familiar objects such as particles and waves. However, in both cases the attempts have been unsuccessful. Dyson makes the point that the first layer is an entirely mathematical construction, and it doesn't make sense to try to reduce it to descriptions that make sense in the macro world that we live in since our language was not designed to describe the layer one processes. The main utility of the first layer is to provide a mathematically tractable model from which predictions about events in the real world can be made with a high degree of accuracy. The process by which the real world in the second layer manifests itself from the processes happening in the first layer remains largely mysterious, and in the context of Quantum Mechanics goes by names such as  Quantum Wave Collpase or Quantum Decoherence. 

My objective in this essay to explore the existence of the two layer structure as a common organizing principle that is used to structure other complex systems as well, in particular we will look at two broad domains, namely Biology and Deep Learning systems. In Biology, the DNA can be considered to the first layer structure, which by itself is fairly simple to describe, but when expressed in the language of proteins and cells by using the Genetic Code, it results in the complex second layer structure and multiplicity of living things that we find around us. The cellular machinery used to translate the layer one structures in the DNA into layer 2 structures of animals and plants is largely understood thanks to the progress in Biology over the last 70 years. The patterns in the DNA itself is subject to change over time, using the Law of Natural Selection as first discovered by Charles Darwin. These laws are reasonably simple, hence are comprehensible to us, and yet they result in complex Biological structures whose origin was completely mysterious before Darwin came along.
 
In this essay I will argue that modern Deep Learning systems also obey the two layer design principle for complex systems. In this case the first layer typically goes by the name of Latent Variables. Once again these live in multi-dimensional spaces called Latent Spaces that consist of hundreds of dimensions and are not comprehensible to our senses, but they capture the structure present in objects in the real world, such as images and language, which form the second layer of the structure. The Neural Network serves as a system to convert the abstract first layer latent variables into concrete objects such as images and language that we can comprehend. 
These Neural Network, that go by names such as Convolutional Neural Networks and Transformers, were originally inspired by models of how the human brain functions, even though the underlying mechanisms are very different in the two cases. By manipulating the Latent Variables that these models create, we are able to carry out complex transformations of images that was not possible before. Moreover by connecting the the Latent Spaces of images and language, we can generate new images by describing them in words.

This also raises the interesting question of whether the brain itself is organized according to the two layer design principle. It could be that information is organized in the brain in multi-dimensional layer one structures, which are then converted into the three dimensional space that we perceive and words that we understand, using the brain's Neural Network. 

The rest of this essay is organized as follows: In Section 2.0 I discuss what we know about Latent Variables in the context of images, the Neural Network Architectures used to generate them, and how they are utilized in practice. Section 3.0 is on the topic of Latent Variables in Natural Language Processing (NLP), and also the connection between Image and NLP Latent Variables. In Section 4.0 we cast the DNA and Genes in Biological Cells into the language of Latent Variables, and describe how these get expressed into the living structures that we see around us. In Section 5.0 we discuss Latent Variables in the contexts of Physics, and finally in Section 6.0 we end the essay with some remarks on the role Latent Variables play in the operation of the brain.

## Latent Space for Images and Text

Due to the advances in Deep Learning in the last decade, we now have the technology to be able to conjure up images by simply describing them in words, or manipulate an image by using simple numerical rules. But how did we get to this point? Not so long ago, the only way to operate on images was by modifying the hundreds of thousands of color pixels that make up an image, which is an extremely difficult undertaking. Clearly images have a lot of underlying structure, which should help in manipulating them, but we had no way to discover this structure. Examples of such structures would be: A car image is made up of a chassis, which is turn has components such as doors, windows, seats etc or a human image is made up limbs, head, face, etc the face in turn has eyes, lips, nodse etc and limbs have joints, toes and fingers. Thus what was missing was a semantic level understaing of images, which would allow us to find similar images or manipulate the objects of an image in a simple way.

- Use example of MNIST images
- How latent spaces were discovered by solving the classification problem
- Latent spaces to reproduce images, Auto-Encoders
- Engineering latent spaces by using VAE, well behaved latent spaces, image manipulation
- latent spaces for language
- Isomorphism between language and image latent spaces
- Generating images by describing them in words

![](https://subirvarma.github.io/GeneralCognitics/images/lat1.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/lat2.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/lat3.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/lat4.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/lat5.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/lat6.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/lat7.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/lat8.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/lat9.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/lat10.png) 


## Latent Space for Language









## Latent Space in Biological Systems





## Latent Spaces in Brains





## Latent Spaces in Physics












