---
layout: post
title: Clustering via Non-Parametric Bayes
---

**unfinished..**

### Introduction

clustering is a popular topic in statistics and machine learning, with various applications to many industries. otably, the [k-means](http://en.wikipedia.org/wiki/K-means_clustering) clustering algorithm is an effective clustering algorithm with a rather easy implementation. however, properly utilizing the k-means algorithm requires one to know the value of *k* (the number of clusters) beforehand, which is unknown in many cases. to move around this obstacle, there are various [bayesian](http://en.wikipedia.org/wiki/Bayes'_theorem) approaches to clustering that provide a sensible alternative. 

### Dirichlet Processes

the crux of the bayesian non-parametrics (meaning that nothing is parametrized) is the [dirichlet process](http://en.wikipedia.org/wiki/Dirichlet_process). in layman's terms, the dirichlet process or DP creates a discrete probability measure from a continuous distribution. the DP also exhibits interesting features, including clustering and exchangeability. in turn, we can look to examine the chinese restaurant process (crp) and the stick-breaking process. 

### Stick-Breaking Process

the stick-breaking process ... 

{% highlight r %}
## stick-breaking construction
n    	  <- 100
alpha 	  <- 3
base 	  <- function( num ) { rnorm(num, 47, 5) }
beta      <- rbeta(n, 1, alpha)
betaprod  <- c(1, cumprod(1 - beta))[1:n]
pis  	  <- betaprod * beta
y   	  <- base(n)
theta	  <- sample(y, prob = pis, replace = TRUE)

{% endhighlight %}

![stick]({{ site.baseurl }}public/assets/stick.png)


### Infinite Dimensional Clustering

if we infuse the dirichlet process with the k-means algorithm, we obtain the DP-means algorithm, outlined in [this paper](http://www.cs.berkeley.edu/~jordan/papers/kulis-jordan-icml12.pdf) by jordan and kulis. in essence, this algorithm is parameterized by *α*, the concentration parameter, which controls how far apart each cluster should be. as alpha indirectly determines the number of clusters (if alpha is small, each observation could be it's own cluster, but if alpha is large, we would only have 1 or 2 clusters), we see that properly selecting the right alpha can be difficult. therefore it is clear that the problem of choosing the right alpha for the infinite mixture model is as difficult as choosing the correct *k* value for the k-means algorithm. to counteract this, we can use a gibbs sampler for the dirichlet process with hyper-priors on the alpha value. this will be the topic of my next blog post!


an implementation of the algorithm outlined in the above paper can be found in this gist. **more to come...**