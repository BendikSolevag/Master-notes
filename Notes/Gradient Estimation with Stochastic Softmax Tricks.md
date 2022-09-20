https://arxiv.org/pdf/2006.08063.pdf

# Stochastic Softmax Tricks

The latent variable of a variational autoencoder is a vector of continuous variables. This is fine for problems where the only aim encode some input, and to recreate some output. In some cases, however, we wish to infer something in our latent space. In these cases, we often want our latent variable to be one hot or categorical. To achieve this, we will often take the softmax of our output variables. 

[The Gumbel Max trick](https://medium.com/swlh/on-the-gumbel-max-trick-5e340edd1e01) was introduced as an alternative to the softmax, as it solves a few issues. 
1. Notably, the Gumbel Max trick operates mainly in the log space, avoiding potential numerical over-/underflow errors, and thereby incorrect sampling behaviour. 
2. The Gumbel Max trick circumvents the need for [marginalisation](https://towardsdatascience.com/probability-concepts-explained-marginalisation-2296846344fc), saving computation time. 

