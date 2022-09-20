
# Predicting Gene Expression Through Causal Structure

Master thesis by Bendik Solevåg
Supervisors: Ramin Hasibi & Tom Michoel 

## Introduction, background and goals

Graphs are data structures conveying information about a set of objects, called vertices, and the relationships between them, called edges. They are widely used to illustrate social networks, interactions, data flow, molecules, etc. Essential to the nature of graphs is the fact that the structure in which they are drawn conveys no information about the nodes or edges. Only the nodes and edges themselves convey this information. Due to their usefulness, it is reasonable to want to model graphs using neural networks, in order to perform tasks on them. This poses an interesting challenge, as giving a graph as input to any network necessarily implies some ordering of the input data. This violates the rules of graphs, as any graph can be drawn in a number of ways, and its data has no natural order.

The problem has spawned a new family of neural networks known as graph neural networks, requiring that any operation on the graph must be permutation invariant/equivariant. Graph Neural Networks have proven to be useful, having for example been applied in Google Maps’ traffic prediction system (Lange & Perez, 2020).

In 2021, Zečević et al. introduced a paper that provided a theoretical framework connecting graph neural networks to structural causal models, through their directed acyclic graph representations (Zečević et al., 2021). 

There are publically available datasets containing genes, their related eQTL values, and their expression values. It is known that these activity levels are influenced by their related eQTL values, as well as other genome expression levels. One must then necessarily be able to fit a structural causal model, with its related DAG, to the interaction between genome expression levels. Such a network can be represented using a graph neural network. Representing the graph allows us to reason about possible missing node feature values, representing genome expression values. Such a network may even discover wrongly assumed causality, or causal relationships previously unknown. 
  

The thesis will explore various Graph Neural Network architectures trained to predict missing node features, and to reason about the causal relationships within the graph. In my work I will benchmark various architectures against various methods, from basic linear methods, to the current state-of-the-art .


  

### References

Lange, O., & Perez, L. (2020, September 3). Traffic prediction with advanced Graph Neural Networks. DeepMind. Retrieved August 25, 2022, from https://www.deepmind.com/blog/traffic-prediction-with-advanced-graph-neural-networks

Zečević, M., Dhami, D. S., Veličković, P., & Kersting, K. (2021, September 9). Relating Graph Neural Networks to Structural Causal Models. DeepMind. Retrieved August 25, 2022, from https://www.deepmind.com/publications/relating-graph-neural-networks-to-structural-causal-models
