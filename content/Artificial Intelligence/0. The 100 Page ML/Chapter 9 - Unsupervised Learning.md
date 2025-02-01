# Unsupervised Learning
### Density Estimation
It is a problem of modeling the pdf of the unknown probability distribution from which the dataset has been drawn.
### Clustering
Clustering is a problem of learning to assign a label to examples by leveraging an unlabeled dataset. Because the dataset is completely unlabeled, deciding on whether the learned model is optimal is much more complicated than in supervised learning. There is a variety of clustering algorithms, and, unfortunately, it’s hard to tell which one is better in quality for your dataset. Usually, the performance of each algorithm depends on the unknown properties of the probability distribution the dataset was drawn from.
#### K-means
The k-means clustering algorithm works as follows. First, the analyst has to choose k — the number of classes (or clusters). Then we randomly put k feature vectors, called centroids to the feature space1. We then compute the distance from each example x to each centroid c using some metric, like the Euclidean distance. Then we assign the closest centroid to each example (like if we labeled each example with a centroid id as the label). For each centroid, we calculate the average feature vector of the examples labeled with it. These average feature vectors become the new locations of the centroids.
We recompute the distance from each example to each centroid, modify the assignment and repeat the procedure until the assignments don’t change after the centroid locations were recomputed
#### DBSCAN and HDBSCAN
While k-means and similar algorithms are centroid-based, DBSCAN is a density-based clustering algorithm. Instead of guessing how many clusters you need, by using DBSCAN, you define two hyperparameters: ‘ and n. You start by picking an example x from your dataset at random and assign it to cluster 1. Then you count how many examples have the distance from x less than or equal to ‘. If this quantity is greater than or equal to n, then you put all these ‘-neighbors to the same cluster 1. You then examine each member of cluster 1 and find their respective ‘-neighbors. If some member of cluster 1 has n or more ‘-neighbors, you expand cluster 1 by putting those ‘-neighbors to the cluster. You continue expanding cluster 1 until there are no more examples to put in it. In the latter case, you pick from the dataset another example not belonging to any cluster and put it to cluster 2. You continue like this until all examples either belong to some cluster or are marked as outliers. An outlier is an example whose ‘-neighborhood contains less than n examples.

HDBSCAN is the clustering algorithm that keeps the advantages of DBSCAN, by removing the need to decide on the value of ‘. The algorithm is capable of building clusters of varying density. HDBSCAN is an ingenious combination of multiple ideas and describing the algorithm in full is out of the scope of this book. HDBSCAN only has one important hyperparameter: n, that is the minimum number of examples to put in a cluster. This hyperparameter is relatively simple to choose by intuition. HDBSCAN has very fast implementations: it can deal with millions of examples e
#### Determining the Number of Clusters
#### Other Clustering Algorithms
DBSCAN and k-means compute so-called hard clustering, in which each example can belong to only one cluster. Gaussian mixture model (GMM) allow each example to be a member of several clusters with different membership score (HDBSCAN allows that too, by the way). Computing a GMM is very similar to doing model-based density estimation. In GMM, instead of having just one multivariate normal distribution (MND), we have a weighted sum of several MNDs: 
$$
f_{\text{x}} = \sum_{j=1}^ k {\phi_{j}f_{\mu_{j} , \sum_{j}}}
$$
where $f_{\mu_{j}, \sum_{j}}$ is a MND $j$ and $\phi_{j}$ is its weights in the sum.
### Dimensionality Reduction
Many modern machine learning algorithms, such as ensemble algorithms and neural networks handle well very high-dimensional examples, up to millions of features. With modern computers and graphical processing units (GPUs), dimensionality reduction techniques are used much less in practice than in the past. The most frequent use case for dimensionality reduction is data visualization: humans can only interpret on a plot the maximum of three dimensions.
The three most widely used techniques of dimensionality reduction are principal component analysis (PCA), uniform manifold approximation and projection (UMAP).
#### PCA
Principal component analysis or PCA is one of the oldest methods.

![[PCA.png]]

Consider a two-dimensional data as shown in fig. 6a. Principal components are vectors that define a new coordinate system in which the first axis goes in the direction of the highest variance in the data. The second axis is orthogonal to the first one and goes in the direction of the second highest variance in the data. If our data was three-dimensional, the third axis would be orthogonal to both the first and the second axes and go in the direction of the third highest variance, and so on. In fig. 6b, the two principal components are shown as arrows. The length of the arrow reflects the variance in this direction. Now, if we want to reduce the dimensionality of our data to $D_{new} < D$, we pick $D_{new}$ largest principal components and project our data points on them
#### UMAP
In UMAP, this similarity metric $w$ is defined as follows,
$$
w(x_{i}, w_{j}) \stackrel {def} {=} w_{i}(x_{i}, x_{j}) + w_{j}(x_{j}, x_{i}) - w_{i}(x_{i}, x_{j}) w_{j}(x_{j}, x_{i}).
$$
The function $w_{i}(x_{i}, x_{j})$ is defined as,
$$
w_{i(x_{i}, x_{j})} \stackrel {def} {=} \exp\left( - \frac{d(x_{i}, x_{j}) - \rho_{i}}{\sigma_{i}} \right) \qquad\qquad (5)
$$
where $d(x_{i}, x_{j})$ is the Euclidean distance between two examples, $\rho_{i}$ is the distance from $x_{i}$ to its closest neighbor, and $\sigma _i$ is the distance from $x_{i}$ to its $k^{th}$ closest neighbor ($k$ is a hyperparameter of the algorithm).

It can be shown that the metric in eq. 5 varies in the range from 0 to 1 and is symmetric, which means that $w(x_{i}, w_{j}) = w(x_{j}, x_{i})$.

Let $w$ denote the similarity of two examples in the original high dimensional space and let $w'$   be the similarity given by the same eq. 5 in the new low-dimensional space. Because the values of $w$ and $w'$ lie in the range between 0 and 1, we can see them as two probability distributions. A widely used metric of similarity between two probability distributions is cross-entropy: 
$$
C(w, w') = \sum_{i=1}^{N} \sum_{j=1}^{N} w(x_{i},x_{j} \ln \left( \frac{w(x_{i}, x_{j})}{w' (x'_{i}, x'_{j})} \right) + (1 - w(x_{i}x_{j})) \ln \left( \frac{1 - w(w_{i}, w_{j})}{1 - w' (x'_{i}, x'_{j})} \right) \qquad\qquad(6)
$$

where $x'$ is the low-dimensional “version” of the original high-dimensional example $x$. 

As you can see from eq. 6, when $w(x_{i}, x_{j})$ is similar to $w'(w'_{i}, w'_{j})$, for all pairs $(i, j)$, then $C(w, w')$ is minimized. And this is precisely what we want: for any two examples $x_i$ and $x_j$ , we want their similarity metric in the original and the lower-dimensional spaces to be as similar as possible. 

In eq. 6 the unknown parameters are $x'_i$ (for all $i = 1,...,N$) and we can compute them by gradient descent by minimizing $C(w, w')$.
___
### Outlier Detection
Outlier detection is the problem of detecting in the dataset the examples that are very different from what a typical example in the dataset looks like.
Techniques to solve this :
- Autoencoder
- one-class classifier learning
___