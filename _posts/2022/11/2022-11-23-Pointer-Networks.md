---

layout: post

title: "Pointer Networks"

subtitle: ""

author: "XJX"

header-img: "img/home-bg-art.jpg"

header-mask: 0.2

published: true

tags:

- Readings

---

# Pointer Networks

by Oriol Vinyals et al, 2017

## Introduction

Considering the following classical combinational problems:

- Convex Hull: Finding convex hull of a finite number of points (Figure 2. (a))
- Delaunay triangulation: Find a triangulation of the set of points such that each circumcircle of every triangle is empty, that is, there is not point in its interior.
- Travelling salesman problem (TSP): Given a list of cities, find the shortest possible route that veisits each city exactly once and returns to the starting point.

![examples](https://github.com/xjx-xiong/xjx-xiong.github.io/raw/master/_posts/2022/11/example.png)

All the three problems share the following characteristics:

1. The output is a discrete sequence, with elements take values from the input.

2. The output size is depent on the input size and the input size for different problems are different.

The first characteristic leads us to consider some sequence-to-sequence models, however, we encounter challenges for the second one. As for previous known models working with sequences require the size of the output dictionary to be fixed a priori, which are unknown in this case. 

Therefore, the author introduced a new architecture of neural network to tackle the problems with variable output size.

## Models

$$
\begin{align*}
\mathcal{P} &= \{P_1, \cdots, P_n\}: \text{the input of $n$ vectors} \\
m(\mathcal{P}) &= \text{the size of the output for $\mathcal{P}$} \\
C^{\mathcal{P}} &= \{C_1, \cdots, C_{m(\mathcal{P}})\} \text{ the output vector}
\end{align*}
$$

### RNN

Uses a parametric model 

$$p(C^\mathcal{P}|\mathcal{P}:\theta)$$ 

to estimate the conditional probability, which can be decomposed using chain rule as 

$$p(C^\mathcal{P}|\mathcal{P}:\theta) = \Pi_{i=1}^{m(\mathcal{P})}p_\theta(C_i|C_1, \cdots, C_{i-1}, \mathcal{P}:\theta)$$

, and the parameter is chosen to be the one that maximize the conditional probability.

Note that the history is encoded into a single vector for the encoder. The fact show that models like RNN constraints the amount of information and computation that can flow through to the generative model.

### Attention

Let $$(e_1, \cdots, e_n)$$ be the encoder and $$(d_1, \cdots, d_{m(\mathcal{P})})$$ be the decoder hidden state. Then, instead of keep only one single state, the attention mechanism 

- maintains all encoded input sequences visible for the decoder

- compute the attention vector at each output time $$i$$ for the input sequence $$j$$ as 
  $$
  \begin{align*}
  u^i_j &= v^T + \tanh(W_1 e_j + W_2d_i) \\
  a_j^i &= softmax(u^i_j) \\ 
  \end{align*}
  $$
  $$v, W_1, W_2$$ are learnable parameters.

- get the decoder hidden state as the weighted some of the encoder vector
  $$
  d_j' = \sum_{j=1}^n a_j^ie_j
  $$



### Pointer Networks (Ptr-Net)

Basically, combined the previous two ideas. Instead of using a parametric way to model the conditional probability, Prt-Net borrow the idea from Attention Mechanism, which directly point to the input sequence. The idea naturally solved the problems we proposed in the very beginning, that is, it is suitable for **problems whose outputs are discrete and correspond to position in the input.** (The starting token can be regarded as a learnable variable, generate untill encounter the stopping token. For the TSP problem, the author suggests to use beam search as the result may not be invalid, which is constriant).

![examples](https://github.com/xjx-xiong/xjx-xiong.github.io/raw/master/_posts/2022/11/PtrNet.png)

## Problems

1. The network is trained in a supervised way, in which the label for the training data are generated from some existing exact or approximate algorithms. For the exact method, it may be too expensive to get a result for large problem. For the approximate algorithms, the performance of the network is connected to the results for the existing models. 

# References

Pointer Networks <https://arxiv.org/pdf/1506.03134.pdf>





















