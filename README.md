# Anonymous-Upload
Here, we upload images for Neurips 2022 submission of Spectral Graph Contrastive learning for reviewer ttS5 and D78f.

Edit, Aug 8 : We also add alignment literature for better illustration for reviewer hB1i.

Edit, Aug 14 : We received a late review from reviewer Gxij. Since we cannot respond on openreview, we would like to point out that SUGRL and MERIT are papers from AAAI 2022 and IJCAI 2022 respectively, and one (MERIT) has to do with temporal graphs (not our area). Further, the code upload for SUGRL (AAAI 22) was only finished in April, which is hardly enough time for us to attend to this baseline. For MERIT, we could not even find code, and it is even unlikely this paper was out in any form before the neurips deadline, as IJCAI 2022 had a camera ready deadline in May itself. We view these two demands for comparison as unreasonable.

Regarding the other demands of the reviewer, we (from our initial version itself) put sections in our appendix regarding run time, ablation study (the contribution per heuristic). The demand for the standard deviation is also there in the appendix along with confidence intervals on top of it. We also urge that our comments to reviewers be taken into account which go over these points. Some of the popular data sets demanded for experiment have already been addressed in the appendix and reviewer comments (cora, citeseer), but more importantly these are not even our focus - as we make clear in our comments to reviewers, we are aiming to learn a method for node attribute free cases, which these do not fall under.

# ttS5 - Example of how time complexity of spectral methods scales with datasets

We recall that these are the statistics of datasets available to pre train our networks : 

![](./datasetdetails.png)

As such we observe that the size of the ego graph generally scales with the size of the overall graph, but somewhat slower than linearly, even on a log scale. Further the degree scaling is inconsistent, possibly due to the NetRep dataset.

![](./egoversussize_labeled_fixed.png)
![](./egographanddegree_labeled.png)

Similar to the ego graph case, the time per graph is also widely varying with degree. However, if NetRep can be excluded, an overall trend of the time increasing with higher degree is obvious, as is the trend of increasing time with overall pretrain graph size.

![](./timeversusnode.png)
![](./timeversusdegree.png)

However, quite importantly, the scaling is at best linear vs the log of the size of the graph, and hence manageable, and the ego graph does not come close to approaching 256 in average size. In short, the scaling is not untenable with the growth, and neither is SGCL particularly costly - it is close to GraphCL and all methods except MVGRL (computed with the heat variant).

# D78f - Example of negative transfer on IMDB-BINARY

We can see here some example histograms, with mean and standard deviation noted, and an overall Gaussian spread of outcomes for GCC[1] frozen transfers on IMDB-BINARY with DBLP as the pretrain bench. Contrary to what is desired, the performance is worse as the number of epochs increases. It becomes worse from 5 to 10 to 20.

This is an example of negative transfer (a form of overfitting) and is noted in section 4.3 of GCC as due to domain shift. It is in fact commonplace in Graph pre-training [2], and the primary reason frozen pre-training is beaten out by unsupervised methods. This phenomenon is not specific to GCC.

Below, all three figures are histograms of different random runs initialized from the same core model, with y-axis representing counts of the occurrence, and x-axis representing accuracy. The x-label indicates mean accuracy and standard deviation, and the mean accuracy falls with more training.

![](./imdb-binary_5.jpg)
![](./imdb-binary_10.jpg)
![](./imdb-binary_20.jpg)

[1] Qiu, Jiezhong, et al. "GCC: Graph contrastive coding for graph neural network pre-training." KDD 2020.

[2] Hu, Weihua, et al. "Strategies for pre-training graph neural networks."  ICLR 2020.

# hB1i - Alignment

Here, we provide two illustrative figures we make that respectively demonstrate:
1.	The case where the global graph, after a random walk, can yield two views, which after Laplacian eigendecomposition end up with inconsistent embeddings for the same node, and thus requires alignment.
2.	The Wasserstein-Procrustes alignment process which is used as a subprocess to correct the inconsistent embeddings.
If the reader hope to know more details about the network embedding alignment, representative papers that explain the Wasserstein Procrustes method include CONE-ALIGN [2]- especially in figures 1 and 2 and section 4.2, as well as REGAL [3] and G-CREWE [4]. 

![](./alignment_take2.jpg)
![](./Alignment_edited_page-0001.jpg)

[1] Hu, Weihua, et al. "Strategies for pre-training graph neural networks."  ICLR 2020.

[2] Chen, Xiyuan, et al. "Cone-align: Consistent network alignment with proximity-preserving node embedding." CIKM 2020. https://dl.acm.org/doi/pdf/10.1145/3340531.3412136

[3] Heimann, Mark, et al. "Regal: Representation learning-based graph alignment." CIKM 2018. https://dl.acm.org/doi/pdf/10.1145/3269206.3271788

[4] Qin, Kyle K., et al. "G-crewe: Graph compression with embedding for network alignment." CIKM 2020. https://arxiv.org/pdf/2007.16208.pdf
