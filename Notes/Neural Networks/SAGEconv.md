https://arxiv.org/pdf/1706.02216.pdf
Instead of training individual embeddings for each node, we learn a function that generates embeddings by sampling and aggregating features from a node’s local neighborhood.

The key idea behind our approach is that we learn how to aggregate feature information from a node’s local neighborhood (e.g., the degrees or text attributes of nearby nodes).


### Mean aggregator. 
Our first candidate aggregator function is the mean operator, where we simply take the elementwise mean of the vectors in $\{{h^{k−1}_{u} ,\forall u \in N(v)}\}$. The mean aggregator is nearly equivalent to the convolutional propagation rule used in the transductive GCN framework.

In particular, we can derive an inductive variant of the GCN approach by replacing lines 4 and 5 in Algorithm 1 with the following:
$$ h^k_v ← σ(W · MEAN(\{{h^{k−1}_v }\} ∪ \{{h^{k−1}_u , ∀u ∈ N (v)}\}). $$
We call this modified mean-based aggregator convolutional since it is a rough, linear approximation of a localized spectral convolution. An important distinction between this convolutional aggregator and our other proposed aggregators is that it does not perform the concatenation operation in line 5 of Algorithm 1—i.e., the convolutional aggregator does concatenate the node’s previous layer representation h k−1 v with the aggregated neighborhood vector h k N(v) . This concatenation can be viewed as a simple form of a “skip connection” [13] between the different “search depths”, or “layers” of the GraphSAGE algorithm, and it leads to significant gains in performance.

### LSTM aggregator
Also examined LSTM aggregator. It has a larger expressive capability, but must introduce some ordering of the neighbours, as the inputs are given in a sequential manner. This issue is tackled by introducing the neighbours in a random permutation, but come on.

### Pooling aggregator
Both symmetric and trainable. Each neighbor’s vector is independently fed through a fully-connected neural network; following this transformation, an elementwise max-pooling operation is applied to aggregate information across the neighbor set.

$$ AGGREGATE^{pool}_k = max(\sigma(W_{pool}h^k_{u_i} + b), \forall u_i \in N(v)) $$
The function applied before the max pooling can be an arbitrarily deep multi-layer perceptron, but we focus on simple single-layer architectures in this work. Any symmetric vector function could be used in place of the max operator. We found no significant difference between max- and mean-pooling in developments test and thus focused on max-pooling for the rest of our experiments

