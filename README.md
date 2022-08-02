# Anonymous-Upload
Here, we upload images for Neurips 2022 submission of Spectral Graph Contrastive learning for reviewer ttS5 and D78f.

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
