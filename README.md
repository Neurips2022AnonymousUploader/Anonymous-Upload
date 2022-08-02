# Anonymous-Upload
Here, we upload images for Neurips 2022 submission of Spectral Graph Contrastive learning.

# Example of negative transfer on IMDB-BINARY

We can see here some example histograms, with mean and standard deviation noted, and an overall Gaussian spread of outcomes for GCC frozen transfers on IMDB-BINARY with DBLP as the pretrain bench. Contrary to what is desired, the performance is worse as the number of epochs increases. It becomes worse from 5 to 10 to 20.

This is an example of negative transfer. It is in fact commonplace in Graph pre-training. (https://openreview.net/forum?id=HJlWWJSFDH), and the primary reason frozen pre-training is beaten out by unsupervised methods.

[]{imdb-binary_10.jpg}
