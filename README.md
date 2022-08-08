# Anonymous-Upload
Here, we upload images for Neurips 2022 submission of Spectral Graph Contrastive learning for reviewer ttS5 and D78f.

Edit, Aug 8 : We also add alignment literature for better illustration for reviewer hB1i.

# ttS5 - Example of how time complexity of spectral methods scales with datasets

We recall that these are the statistics of datasets available to pre train our networks : 

![](./datasetdetails.png)

As such we observe that the size of the ego graph generally scales with the size of the overall graph, but somewhat slower than linearly, even on a log scale. Further the degree scaling is inconsistent, possibly due to the NetRep dataset.

![](./sizeofview.png)
![](./egographanddegree.png)

Similar to the ego graph case, the time per graph is also widely varying with degree. However, if NetRep can be excluded, an overall trend of the time increasing with higher degree is obvious, as is the trend of increasing time with overall pretrain graph size.

![](./timeversusnode.png)
![](./timeversusdegree.png)

However, quite importantly, the scaling is at best linear vs the log of the size of the graph, and hence manageable, and the ego graph does not come close to approaching 256 in average size. In short, the scaling is not untenable with the growth, and neither is SGCL particularly costly - it is close to GraphCL and all methods except MVGRL (computed with the heat variant).

# D78f - Example of negative transfer on IMDB-BINARY

We can see here some example histograms, with mean and standard deviation noted, and an overall Gaussian spread of outcomes for GCC frozen transfers on IMDB-BINARY with DBLP as the pretrain bench. Contrary to what is desired, the performance is worse as the number of epochs increases. It becomes worse from 5 to 10 to 20.

This is an example of negative transfer. It is in fact commonplace in Graph pre-training. (https://openreview.net/forum?id=HJlWWJSFDH), and the primary reason frozen pre-training is beaten out by unsupervised methods. This phenomenon is not specific to GCC.


![](./imdb-binary_5.jpg)
![](./imdb-binary_10.jpg)
![](./imdb-binary_20.jpg)

# hB1i - Alignment

Here, we provide two illustrative figures that respectively demonstrate :

1) The case where the global graph, after a random walk, can yield two views, which after Laplacian eigendecomposition end up with inconsistent embeddings for the same node, and thus requires alignment.

2) The Wasserstein-Procrustes alignment process which is used as a subprocess to correct the inconsistent embeddings.

Representative papers that explain the Wasserstein Procrustes method include CONE-ALIGN (https://dl.acm.org/doi/pdf/10.1145/3340531.3412136) - especially in figures 1 and 2 and section 4.2, as well as REGAL (https://arxiv.org/abs/1802.06257) and G-CREWE (https://arxiv.org/pdf/2007.16208.pdf). The latter two include discussions on the Nystrom method which is similar to ours.

![](./alignment_take2.jpg)
![](./Alignment_edited_page-0001.jpg)
