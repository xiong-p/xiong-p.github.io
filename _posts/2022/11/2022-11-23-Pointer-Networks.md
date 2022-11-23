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

Uses a parametric model $p(C^\mathcal{P}|\mathcal{P}:\theta)$ to estimate the conditional probability, which can be decomposed using chain rule as $p(C^\mathcal{P}|\mathcal{P}:\theta) = \Pi_{i=1}^{m(\mathcal{P})}p_\theta(C_i|C_1, \cdots, C_{i-1}, \mathcal{P}:\theta)$, and the parameter is chosen to be the one that maximize the 


$$

$$
























