I would like to *explicitely* mention that although I have implemented the paper, I am _not_ related to any of the paper's authors.

# Symmetry Teleportation for Accelerated Optimization

I implement* the https://arxiv.org/abs/2205.10637 paper (Symmetry Teleportation for Accelerated Optimization) in Tensorflow, and find fruitful results using a slightly alternate teleportation scheme in application with the Fashion-MNIST dataset. The image provided shows general (paper) training results as a result of teleportation for highly non-convex functions.


![ho ho ho ya filthy animal](fig2_frompaper.png)
##### A personal synopsis:

The loss function with respect to weight layers in deep neural-nets contain symmetries, these symmetries can be exploited via group invariant (equi-energy contour preserving) actions under specific conditions. These priorly unexploited symmetries allow for the model to improve convergence speeds by effectively teleporting its weights in a way as to maintain it's output, yet get itself out of non-optimal troughs and poorly learnable environments, hence improving the speed at which it learns. The paper focuses on using lie groups to allow for gradient ascent for optimising teleportations, however I go a different way by samplying suitable teleports randomly and choosing the best one.

In my tests with a small Fashion-MNIST dataset and feed-forward neural net of size 64, 64, 10, I saw ~10% leaps in training improvement for each teleport; and further vastly improving the convergence. Due to not using gradient ascent, the paper's analysis on achieving 2nd order convergence speeds does not directly apply here - however as I choose a maximal gradient amongst the ones sampled anyways, by numerical observation I do see increased convergence speed. (No guarantee on similarities to second order schemes can be made here). 

The main advantage I see to using teleportation instead of simply having more epochs in training is in the ability to get out of highly non-convex environments, as well as leaps in accuracies where things aren't optimal in some sense.

##### Further comments/questions

1) If the contour is non-convex, how would gradient ascent work in the paper? I find the random sampling followed by gradients ascent (possibly quite a bit more computationally heavy) to be more fruitful.
2) Tests show teleports one after the other aren't particularly effective, instead just one every many epochs is what works. I'm not sure how to deal with potentially unbounded gradients along the contoured path when considering varying actions. This wasn't explored in the paper, and is something I'd like to find out about!
3) Since the result on invariances with bijective activations works with any GL(n) element, why is there a need to consider special non-convex loss functions?
