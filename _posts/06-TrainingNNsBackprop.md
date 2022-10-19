
# The Backprop Algorithm 


```python
from ipypublish import nb_setup
```

## Vast Scale of Gradient Descent in DLNs

In Chapter **LinearLearningModels** we formulated the parameter estimation (or learning) problem for Linear Systems and showed that it could be solved using an optimization procedure based on the Gradient Descent algorithm. We now extend this framework to Dense Feed Forward Networks. Indeed all the arguments in Chapter **LinearLearningModels** for Linear Systems continue to hold for Dense Feed Forward Networks, the only difference being that we can no longer use the simple gradient calculation

$$
\frac{\partial \mathcal L}{\partial w_{ki}} = x_i(y_k - t_k)
$$

The gradients are instead computed by an algorithm called Backprop, which is probably the single most important algorithm in all of Deep Learning. Backprop was discovered in the mid-1980s, and since then the base algorithm hasn't changed and it is still the most efficient technique that we know of to compute gradients in DLN systems.

In order to give an idea of the magnitude of the problem, consider a multi-layer Dense Learning model of the type discussed in Chapter **NNDeepLearning**. Models of this type can have millions of parameters: For example consider the case when the input is a 224x224x3 color image, and the model has a single Hidden Layer with 100 nodes. The number of weights in just the first layer of connections between the Input and the Hidden Layer is given by 224x224x3x100 = 15,082,800! In order to estimate these weights from the training dataset, the gradients $\frac{\partial\mathcal L}{\partial w_{ij}}$ with respect each one of these weights need to be calculated. This is a fairly daunting task, and a lack of solution stymied progress in DLN system until the mid-1980s. The logjam was finally broken with the discovery of the Backprop algorithm, see for example [Montavon, Orr, and Müller (2012)](https://www.springer.com/gp/book/9783642352881). Our objective is to derive this algorithm as well provide some intuition into the subject of Gradient Flows in general. Most of the advances in DLN Architecture in the last few
years have been made with the objective of improving Gradient Flows within the network.

## Optimization Problem

We start by stating the optimization problem for Dense Feed Forward Networks. The system parameters are estimated by solving the following optimization problem: Find the model parameters that minimize the Loss Function $L$ given by:

\begin{equation}
L = {1\over M} \sum_{m=1}^M{\mathcal L}(m), \quad \quad   (**trainNN**)
\end{equation}

where the Cross Entropy Function $\mathcal L$ for a single training sample is given by

$$
\mathcal L = -\sum_{k=1}^K t_k\log y_k
$$

In this equation $(t_1,...,t_K)$ is the Label or Ground Truth vector and $(y_1,...,y_K)$ is the vector of classification probabilities, given by

$$
y_k = \frac{\exp(a_k)}{\sum_{j=1}^K\exp(a_j)},\ \ 1\le k\le K
$$

The numbers $(a_1,...,a_K)$ are the logits and are computed using a scoring function $h_k$, so that

$$
a_k = h_k(W, b),\ \ 1\le k\le K
$$

The numbers $(W,b)$ represent the parameters that are used to specify the model. For Linear Systems the scoring functions were fairly simple:

$$
a_k = \sum_{i=1}^N w_{ki}x_i + b_k,\ \ 1\le k\le K
$$

For Dense Feed Forward Networks, these functions are much more complex. For example for a network with a single Hidden Layer the equations are

$$
a_k = \sum_{i=1}^P w_{ki}^{(2)}z_i + b_k^{(2)},\ \ 1\le k\le K\,\ \ \mbox{where}\ \ z_i = f(\sum_{j=1}^N w_{ij}^{(1)}x_j + b_{i}^{(1)}),\ \ 1\le i\le P
$$

where $f$ is the Activation Function. 

## Gradient Descent

This optimization problem is solved by using the Gradient Descent Algorithm, according to which the optimal parameters $(W,b)$ are estimated iteratively using the following equations:

$$
w_{ij} \leftarrow w_{ij} - \frac{\eta}{M}\sum_{m=1}^M \frac{\partial\mathcal L(m)}{\partial w_{ij}} 
$$

$$
b_i \leftarrow b_i - \frac{\eta}{M}\sum_{m=1}^M \frac{\partial{\mathcal L}(m)}{\partial b_i}
$$

As was discussed in Chapter **LinearLearningModels**, there are two other Optimization Algorithms that are used in practice, since they converge faster than Gradient Descent, namely Stochastic Gradient Descent (SGD), given by

$$
w_{ij} \leftarrow w_{ij} - \eta \frac{\partial{\mathcal L}(m)}{\partial w_{ij}} 
$$

$$
b_i \leftarrow b_i - \eta \frac{\partial{\mathcal L}(m)}{\partial b_i}  
$$

and Batch Stochastic Gradient Descent (B-SGD) with batch size $B$, given by:

$$
w_{ij} \leftarrow w_{ij} - \frac{\eta}{B}\sum_{m=1}^{B} \frac{\partial{\mathcal L}(m)}{\partial w_{ij}}
$$

$$
b_i \leftarrow b_i - \frac{\eta}{B}\sum_{m=1}^{B} \frac{\partial{\mathcal L}(m)}{\partial b_i}
$$

In the absence of an explicit formula for $\frac{\partial{\mathcal L}}{\partial w_{ij}}$, how do we proceed forward? A brute force approach to estimating these gradients is the following: 

Do a couple of forward passes through the network to compute $\mathcal L(w_{11},...,w_{ij},..,w_{MN})$ and $\mathcal L(w_{11},...,w_{ij} + \epsilon,..,w_{MN})$, where $\epsilon$ is a small increment. Using these numbers the gradient with respect to $w_{ij}$ can be estimated

$$
\frac{\partial {\mathcal L}}{\partial w_{ij}} = \frac{ {\mathcal L}(w_{11},...,w_{ij} + \epsilon,..,w_{MN}) - {\mathcal L}(w_{11},...,w_{ij},..,w_{MN})}{\epsilon}
$$
The reader can see that there is a problem with this scheme: If the network has a million parameters, then this requires a million and one forward passes through the network! **The Backprop algorithm on the other hand, only requires just two passes through the network, irrespective of the number of parameters!** As Figure **backprop1** shows, Backprop requires a forward pass during which all the activations in the network are computed, and this is followed by a backward pass to the compute the gradients.


```python
#backprop1
nb_setup.images_hconcat(["DL_images/backprop1.png"], width=600)
```




![png](output_6_0.png)



## The Chain Rule of Derivatives

The fundamental difficult in computing $\frac{\partial {\mathcal L}}{\partial w_{ij}}$ arises from the 
following: The function $\mathcal L$ can written as a nested composition of multiple sub-functions $f, g, h$ etc, such that
the weight $w_{ij}$ is buried several layers deep into it, i.e. $\mathcal L$ can be written as $\mathcal L = f(w_{.}..g(w_{.}..h(w_{ij}..))$. In the case of Neural Networks, each of these functions $f, g, h$ by themselves are
fairly simple, such as additions, max or multiplication by a constant, but after composition, 
the resulting function $f(g(h(...)))$ assumes a very complex form, which
makes computation of $\frac{\partial {\mathcal L}}{\partial w_{ij}}$ by direct differentiation difficult. 


```python
#BP1
nb_setup.images_hconcat(["DL_images/BP1.png"], width=600)
```




![png](output_9_0.png)



Fortunately there is a result from Differential Calculus called the Chain Rule of Derivatives which can be used
to simplify this computation. Indeed the Backprop algorithm can be considered to be an application of this rule.

In order to understand the Chain Rule, consider Part (a) of Figure **BP1**, which shows the computation of $L$
as a composition of the functions $g$, $f$ and $h$ in series. The Chain Rule says that the end-to-end dervative
${{\partial L}\over{\partial x}}$ can be expressed as product of the derivatives across each one of the functions, i.e.

$$
{{\partial L}\over{\partial x}} = {{\partial L}\over{\partial y}}{{\partial y}\over{\partial a}}{{\partial a}\over{\partial x}}
$$

An example of the application of this rule is shown on Part (b) of Figure **BP1**, which we actually encountered
in the chapter on Linear Models.

There is an important extension to the Chain Rule which is also used extensively in Backprop. As shown in 
**backprop3**, this arises for the case in which the output $L$ is a function of multiple inputs $(y_1,...,y_K)$,
and each of these are in turn functions of their own inputs $(a_1,...,a_N)$.


```python
#backprop3
nb_setup.images_hconcat(["DL_images/backprop3.png"], width=600)
```




![png](output_11_0.png)



In this case, the Chain Rule of Differentiation leads to the following rule:

$$
\frac{\partial{\mathcal L}}{\partial a_i} = \sum_{k=1}^K \frac{\partial{\mathcal L}}{\partial y_k} \frac{\partial{y_k}}{\partial a_i}
$$

An important application of this rule is at the output of the Dense Feed Forward Network:

$$
\mathcal L = -\sum_{j=1}^K t_j\log y_j,\ \ \mbox{and}\ \ y_j = \frac{\exp(a_j)}{\sum_{k=1}^K \exp(a_k)},\ \  1\le j\le K
$$

Since these equations are also applicable to the output of Linear Models, the computation of $\frac{\partial{\mathcal L}}{\partial a_i}$ was actually carried in Chapter **LinearLearningModels** where we showed that (see Section
**Multiclass Logistic Regression** in that chapter)

$$
\frac{\partial{\mathcal L}}{\partial a_i} = y_i - t_i,\ \  1\le i\le K
$$

## Gradient Flow Calculus


```python
#backprop2
nb_setup.images_hconcat(["DL_images/backprop2.png"], width=600)
```




![png](output_14_0.png)



Gradient Flow Calculus is the set of rules used by the Backprop algorithm to compute gradients (this also accounts for the use of the term "flow" in tools such as Tensor Flow). Backprop works by first computing the gradients
$\frac{\partial{\mathcal L}}{\partial y_{k}}, i\le k\le K$ at the output of the network (which can be computed using an explicit formula), then propagating or flowing these gradients back into the network. In this section we derive the rules that govern this backward flow of gradients.

Figure **backprop2** shows a node with inputs $(x,y)$ and output $z = h(x,y)$, where $h$ represents the function performed at the node. Lets assume that the gradient $\frac{\partial{\mathcal L}}{\partial z}$ is known. Using the Chain Rule of Differentiation, the gradients $\frac{\partial{\mathcal L}}{\partial x}$ and $\frac{\partial{\mathcal L}}{\partial y}$ can be computed as:

$$
\frac{\partial{\mathcal L}}{\partial x} = \frac{\partial{\mathcal L}}{\partial z}\frac{\partial{z}}{\partial x}
$$

$$
\frac{\partial{\mathcal L}}{\partial y} = \frac{\partial{\mathcal L}}{\partial z}\frac{\partial{z}}{\partial y}
$$


```python
#BP4
nb_setup.images_hconcat(["DL_images/BP4.png"], width=600)
```




![png](output_16_0.png)



This rule can be used to compute the effect of the node on the gradients flowing back from right to left. We apply these equations to the following cases (also shown in Figure **BP4**):

**1. Rule 1: Addition**

$$z = x+y $$

In this case

$$
\frac{\partial{\mathcal L}}{\partial x} = \frac{\partial{\mathcal L}}{\partial y} = \frac{\partial{\mathcal L}}{\partial z}
$$

Hence the addition operation broadcasts the incoming gradient $\frac{\partial{\mathcal L}}{\partial z}$ backwards to all its input branches, without any modification. This is a simple result, but quite important in DLN architecture.

**2. Rule 2: Multiplication by a Constant**

$$z = kx $$

which results in

$$
\frac{\partial{\mathcal L}}{\partial x} = k\frac{\partial{\mathcal L}}{\partial z}
$$

i.e., the multiplication operation in the forward direction results in an identical multiplication of the gradients flowing back.

**3. Rule 3: Multiplication**

$$  z = xy $$

In this case

$$
\frac{\partial{\mathcal L}}{\partial x} = y\frac{\partial{\mathcal L}}{\partial z}, \ \ \mbox{and}\ \ \frac{\partial{\mathcal L}}{\partial y} = x\frac{\partial{\mathcal L}}{\partial z}
$$

Hence the multiplication operation also passes on the incoming gradient, but after multiplying it with the value from the other input branch.

**4. Rule 4: The Max Operation**

$$ z = \max(x, y) $$

$$
\frac{\partial{\mathcal L}}{\partial x} = \frac{\partial{\mathcal L}}{\partial z}\ \ if\ \ x > y\ \ \mbox{and}\ \ 0\ \ \mbox{otherwise}
$$

This shows that the max operation acts like a switch, so that the incoming gradient is switched to the input branch that is larger, while the other branch gets a zero gradient.

**5. Rule 5: The Sigmoid Function**

$$ z = \sigma(x) = \frac{1}{1+\exp(-x)}  $$

In this case

$$
\frac{\partial{\mathcal L}}{\partial x} = z(1-z)\frac{\partial{\mathcal L}}{\partial z}
$$

This equation has some very interesting implications for gradient flows for the case when the sigmoid is used as the Activation Function in DLNs. It implies that if the input value $x$ is very large or very small, then the corresponding gradient $\frac{\partial{\mathcal L}}{\partial x}$ goes to zero (to see why, see Figure **sigmoid** in Chapter **Linear Learning Models**). We will see in the next chapter that this behavior held back progress in DLNs for almost two decades, even after the discovery of the Backprop algorithm.


```python
#backprop4
nb_setup.images_hconcat(["DL_images/backprop4.png"], width=600)
```




![png](output_18_0.png)



Figure **backprop4** illustrates an application of the Gradient Flow rules to a simple neural network. The numbers in green represent the forward flow of activations, while the red numbers represent the backward flow of gradients.

## Backprop


```python
#BP3
nb_setup.images_hconcat(["DL_images/BP3.png"], width=600)
```




![png](output_21_0.png)



In order to gain some intuition, we will first derive the Backprop equations for the special case of a Dense Feedforward Network with a single hidden layer (see Figure **BP3**), and then extend it to the more general case.
Our objective is to compute $\frac{\partial{\mathcal L}}{\partial w}$ and $\frac{\partial{\mathcal L}}{\partial b}$
for all the weights and biases in the network. In the following discussion we use the convention that $z^0_i = x_i,\ 1\le i\le N$.

We first note the following:

$$
\frac{\partial{\mathcal L}}{\partial w^{(r)}_{ji}} = \frac{\partial{\mathcal L}}{\partial a^{(r)}_j}\frac{\partial a^{(r)}_j}{\partial w^{(r)}_{ji}},\ \ {\rm and}\ \  
\frac{\partial{\mathcal L}}{\partial b^{(r)}_{j}} = \frac{\partial{\mathcal L}}{\partial a^{(r)}_j}\frac{\partial a^{(r)}_j}{\partial b^{(r)}_{j}}
\ \ r = 1,2
$$

This follows from the fact that $a^{(r)}_j = \sum_{i} w^{(r)}_{ji}z^{(r-1)}_i + b^{(r)}_j$, so that any change in $\mathcal L$
due to a changing $w^{(r)}_{ji}$ or $b^{(r)}_{j}$ can be entirely captured by measuring how $\mathcal L$ varies with $a^{(r)}_j$ instead.
Also from this equation, $\frac{\partial a^{(r})_j}{\partial w^{(r)}_{ji}} = z^{(r-1)}_i$ and $\frac{\partial a^{(r})_j}{\partial b^{(r)}_{j}} = 1$ from which it follows that

$$
\frac{\partial{\mathcal L}}{\partial w^{(r)}_{ji}} = z^{(r-1)}_i\frac{\partial{\mathcal L}}{\partial a^{(r)}_j}
\ \ {\rm and}\ \ 
\frac{\partial{\mathcal L}}{\partial b^{(r)}_{j}} = \frac{\partial{\mathcal L}}{\partial a^{(r)}_j}
\ \ r = 1,2
$$

Define the gradient $\delta^{(r)}_j$ at the $j^{th}$ node in the $r^{th}$ layer as
$
\frac{\partial{\mathcal L}}{\partial a^{(r)}_j} = \delta^{(r)}_j
$ so that  there is a $\delta^{(r)}_j$ value associated with every node in the network. Substituting this into the prior equation, we get:

$$
\frac{\partial{\mathcal L}}{\partial w^{(r)}_{ji}} = z^{(r-1)}_i \delta^{(r)}_j\ \ {\rm and}\ \ 
\frac{\partial{\mathcal L}}{\partial b^{(r)}_{j}} =  \delta^{(r)}_j, 
\ \ r = 1,2
$$

There is a simple mnemonic device that can be used to remember this formula: Consider an arrow from node $i$ in
layer $r-1$ to node $j$ in layer $r$, such that link weight associated with this arrow is $w^{(r)}_{ji}$. Then the
gradient of $\mathcal L$ with respect to $w^{(r)}_{ji}$ is given by the product of the activation $z^{(r-1)}_i$ at the tail
of the arrow, and the gradient $\delta^{(r)}_j$ at the head of the arrow.

These equations can also be compactly represented using matrix notation: For the $r^{th}$ layer, define ${\partial L\over\partial W^{(r)}}$ be a matrix whose $(ji)^{th}$ element is given by
${\partial L\over{\partial w^{(r)}_{ji}}}$, let ${\partial L\over\partial B^{(r)}}$ be a vector whose $(j)^{th}$ element is given by ${\partial L\over{\partial b^{(r)}_{j}}}$ and define the vector $\Delta^{(r)}$ as
$\Delta^{(r)} = (\delta^{(r)}_1,...,\delta^{(r)}_K)$

$$
{\partial L\over\partial W^{(r)}} = \Delta^{(r)}(Z^{(r-1)})^T \ \ {\rm and}\ \ 
{\partial L\over\partial B^{(r)}} = \Delta^{(r)},
\ \ 1\le r\le R+1\ \ with\ \ Z^{(0)} = X
$$

Since the values $Z^{(r)}$ are known from the Forward Pass, it follows that
in order to compute the gradients of $\mathcal L$ with respect to the parameters $W^{(r)}$ and $B^{(r)}$,
it is sufficient to compute the $\Delta^{(r)}$ values. It turns out that these gradients can be computed by means of a backwards recursion formula (called the Backwards Pass), which is derived next.

### The Backwards Pass

We start with the following equation that was derived in Section **Gradient Flow Calculus** for the gradients of $\mathcal L$ with respect to the output Logits:

$$
\frac{\partial{\mathcal L}}{\partial a^{(2)}_k} = \delta^{(2)}_k =  y_k - t_k,\ \  1\le k\le K
$$

Using matrix notation the above equation can be written as

$$
\Delta^{(2)} = Y - T 
$$

Hence we only need to compute the gradients for the hidden layer $\delta^{(1)}_i, 1\le i\le M$. In order to do so
consider the following figure:


```python
#BP2
nb_setup.images_hconcat(["DL_images/BP2.png"], width=600)
```




![png](output_23_0.png)



In Figure **BP2** we focus on the link between the node 2 of the Hiddel Layer, and the $K$ nodes in the Output Layer
(this node is outlined in red in Figure **BP3**). Our objective is to compute the gradient $\delta^{(1)}_2$, and in
order to do so, we invoke the Gradient Flow Rules derived earlier in this chapter. 

- We start the computation on the RHS of the figure, where we already know the gradients $(\delta^{(2)}_1,...,\delta^{(2)}_K)$ at the $K$ output nodes.

- When these gradients flow back over the links with weights $(w^{(2)}_{12},...,w^{(2)}_{K2})$, an application of
Gradient Flow Rule 2 changes their values to $(w^{(2)}_{12}\delta^{(2)}_1,...,w^{(2)}_{K2}\delta^{(2)}_K)$. 

- Since all of the $K$ gradients meet at a single point, their values add up, so that the resulting gradient is given by $\sum_{k=1}^K w^{(2)}_{k2}\delta^{(2)}_k$.

- The gradient next flows back across the Activation Function $f$, and another application of the Gradient Flow Rules shows that the resulting gradient is $f'(a^{(1)}_2)\sum_{k=1}^K w^{(2)}_{k2}\delta^{(2)}_k$. Since the flow is now at node 2 of the Hidden Layer, it follows that
$$
\delta^{(1)}_2 = f'(a^{(1)}_2)\sum_{k=1}^K w^{(2)}_{k2}\delta^{(2)}_k
$$

The complete set of gradients at the hidden layer $(\delta^{(1)}_1,...,\delta^{(1)}_M)$ can be computed in a similar way using the formula:

$$
\delta^{(1)}_i = f'(a^{(1)}_i)\sum_{k=1}^K w^{(2)}_{ki}\delta^{(2)}_k
$$

Using matrix notation, this equation can be written as

$$
\Delta^{(1)} = f'(A^{(1)})\odot (W^{(2)})^T \Delta^{(2)}
$$

In this equation $\odot$ is the elementwise product between the vectors $ f'(A^{(1)}) $ and $ (W^{(2)})^T \Delta^{(2)} $ (also called the Haddamard Product) and $f'(A^{(1)})$ is the column vector 
$(f'(a^{(1)}_1), f'(a^{(1)}_1), ...,f'(a^{(1)}_M))$.

By looking at the structure of these equations, we can write down the backwards recursion for Dense Feed Forward Network with $R$ hidden layers, as follows:

For the Logit Layer:
$$
\Delta^{(R+1)} = Y - T 
$$
For the internal layers:
$$
\Delta^{(r)} = f'(A^{(r)})\odot (W^{(r+1)})^T \Delta^{(r+1)},\ \ 1\le r\le R
$$

This computation completes the Backward Pass of the Backprop algorithm, since we now have the $\delta$ gradients for
all the nodes in the Neural Network. These can now be combined with the activation values $z$ from the Forward Pass, to compute the ${\partial\mathcal L}\over{\partial w}$ for all the weights in the network.

## The Complete Training Algorithm


```python
#backprop5
nb_setup.images_hconcat(["DL_images/backprop5.png"], width=600)
```




![png](output_26_0.png)



The complete Backprop based Batch Stochastic Gradient Descent algorithm for Dense Feed Forward Networks is shown in Figure **backprop5**. The detailed steps are as follows:

**Step 1**:	Initialize all the weight and bias parameters $(W^{(r},B^{(r)}), 1\le r\le R+1$  (this is a critical step, see Chapter **GradientDescentTechniques** on how to do this).

**Step 2**: Repeat the following Step 3, E times

**Step 3**:	Split up the training data $((X(1),T(1)),...,(X(M),T(M)))$ into $M\over B$ batches, and for each batch repeat the following steps (a) - (d):

   **(a) Forward Pass:** The data $X$ belonging to the batch are input into the model in sequence. The model activations and output are computed using the following formulae (with $Z^{(0)}=X$):

$$
A^{(r)} = W^{(r)}Z^{(r-1)} + B^{(r)},\ \ Z^{(r)} = f(A^{(r)}),\ \ 1\le r\le R
$$

$$
A^{(R+1)} = W^{(R+1)}Z^{(R)} + B^{(R+1)},\ \ Y = h(A^{(R+1)})
$$

   **(b) Backward Pass:** Evaluate the gradients $\Delta^{(R+1)}$ for the logit layer nodes using

$$
\Delta^{(R+1)} = Y - T 
$$

   Back-propagate $\Delta^{(R+1)}$s using the following equation to obtain the $\Delta^{(r)}, 1 \leq r \leq R$  for each hidden layers in the network.
$$
\Delta^{(r)} = f'(A^{(r)})\odot (W^{(r+1)})^T \Delta^{(r+1)},\ \ 1\le r\le R
$$

   **(c)** Compute the gradients of the Cross Entropy Function $\mathcal L$ with respect to all the weight and bias parameters using the following equation.
$$
{\partial L\over\partial W^{(r)}} = \Delta^{(r)}(Z^{(r-1)})^T \ \ {\rm and}\ \ 
{\partial L\over\partial B^{(r)}} = \Delta^{(r)},
\ \ 1\le r\le R+1\ \ with\ \ Z^{(0)} = X
$$

   **(d)** For all the layers $1\le r\le R+1$, Change the model weights according to the formula
$$
w_{ij}^{(r)} \leftarrow w_{ij}^{(r)} - \frac{\eta}{B}\sum_{m=1}^{B} \frac{\partial\mathcal L}{\partial w_{ij}^{(r)}},
$$
$$
b_i^{(r)} \leftarrow b_i^{(r)} - \frac{\eta}{B}\sum_{m=1}^{B} \frac{\partial{\mathcal L}}{\partial b_i^{(r)}},
$$

**Step 4**:  Compute the Loss Function $L$ over the Validation Dataset given by
$$
L = -{1\over V}\sum_{m=1}^V\sum_{k=1}^K t_k{(m)} \log y_k{(m)}
$$
If $L$ has dropped below some threshold, then stop. Otherwise go back to Step 2.

## Issues with Backprop

Even though the algorithm described above was known by the mid-1980s, it took about two more decades before we had the Deep Learning Renaissance. The next two chapters go into reasons for this delay. Specifically, there are a number of additional considerations involved in using the Backprop algorithm that were discovered later, including:

- Choosing a good Activation Function: This is a critical choice, we will examine various alternatives in Chapter **GradientDescentTechniques**.

- Regularization: In our description of Backprop we left out an important detail, i.e., the topic of *Regularization*. It determines how well the model is able to generalize its learning from the training data, to be able to accurately classify test data that it has not seen before. Since this is a fairly big topic in itself, we devote all of Chapter **ImprovingModelGeneralization** to it.

-	Choosing Hyper-Parameter values: So far we have come across the following hyper-parameters: The Learning Rate $\eta$, the number of Hidden Layers $R$ and the number of nodes per Hidden Layer $P^r$, and in the following chapters we will add Regularization related parameters to this list. Part of the training process is choosing good values for them.

-	Initializing the weight parameters: All the weight and bias parameters have to be initialized at the start of the algorithm. If not done properly, it leads to the Vanishing Gradient Problem, which terminates the training process.

-	The stopping problem: This is the problem of when to stop the optimization process and conclude that further training won’t help improve the accuracy of the model.

## Why does Gradient Descent work so well for DLNs? 

Gradient based optimization algorithms are guaranteed to find the minimum if the Loss Function is strictly convex with a global minimum. In reality, the Loss Function in DLNs is highly complex and possesses multiple minima, so that there is a danger that the optimization will get stuck in one of them. In practice this does not seem to matter since the algorithm nevertheless works very well, and it is not clear why this is the case. A theory that has been put forward to explain this is that the stochastic gradient descent technique, introduces randomness into the algorithm, so that occasionally the algorithm may move in non-optimal directions. This increases the probability that if it enters a non-optimum local minima, then it may pop out of it. In all likelihood the algorithm does not settle into the global minima, however it does not seem to make much difference to its efficacy if it finds it way to a local minima. Another explanation that has been put forward to explain the unreasonable effectiveness of Gradient Descent is the following: For smaller models the Loss function exhibits minima that vary in size, so that finding the global minima is important. However models with millions of parameters have a fundamentally different distribution of Loss Function minima. Indeed as the model grows larger, all the minima seem to converge to similar values, so it does not matter which minima the algorithm ends up in.

## References and Slides

- [Slides on DNNs](https://drive.google.com/file/d/1VKHLv4sdX1jZNAg0wbYq1F_LNOHC0Cp9/view?usp=sharing)
- [Slides on BackProp](https://drive.google.com/file/d/1XmeygGr1EqLUHiTu8BrGfMWcr4N3il1c/view?usp=sharing)
