https://arxiv.org/pdf/2004.05718.pdf



Using twelve operations per kernel will require the usage of additional weights per input feature in the U function, which could seem to be just quantitatively—not qualitatively—more powerful than an ordinary MPNN with a single aggregator. However, the overall increase in parameters in the GNN model is modest and, as per our theoretical analysis above, a limiting factor of GNNs is likely their usage of a single aggregation. 

This is comparable to convolutional neural networks (CNN) where a simple 3 × 3 convolutional kernel requires 9 weights per feature (1 weight per neighbour). Using a CNN with a single weight per 3 × 3 kernel will reduce the computational capacity since the feedforward network won’t be able to compute derivatives or the Laplacian operator. Hence, it is intuitive that the GNNs should also require multiple weights per node,