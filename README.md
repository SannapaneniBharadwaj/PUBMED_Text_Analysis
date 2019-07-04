# PUBMED_Text_Analysis

## Visualizing PUBMED abstracts LDA, using Tensor Board

We are using Embedding Projector, a built-in Tensorboard visualizer to interact and analyze the high dimensional data. To visualize, we use Document-topic distribution as the embedding vector which means each topic is treated as a dimension and each point represents the proportion of that topic in the document. 

For visualizing these high dimensional embedding vectors, we should reduce the dimensionality to 2 or 3 dimensions while preserving most of the original information. We use Principal Component Analysis and T-SNE which are inbuilt TensorBoard dimensionality reduction methods.

We upload Embedding vectors file [ download from here] and Metadata file [ download from here] to  TensorBoard. Embedding vectors are Document Topic distributions and Metadata consists of Article Titles and Journal Titles.

Interactive Visualizations of PCA and t-SNE are here https://projector.tensorflow.org/?config=https://dl.dropboxusercontent.com/s/8c939vndmkog6uc/40doc_LDA.json?dl=0


### Using PCA:

PCA helps us understand the Global structure of the data. Although it distorts the local structure, it tends to highlight the large scale structure. 

Tensorboard reduces the Embedding vector dimensions to 10 principal components and allows us to choose 3 out of 10 Principal components in the left panel menu. Each point in the visualization represents a article and these articles are colored according to their Journal Titles. 

From PCA, the visualization looks like a Tetrahedron with a dense clustering at corners and edges. We can say that articles at corners belong to a single topic because each topic is a dimension and these corner articles have large weight in one dimension and almost zero in other dimensions. 

In the visualization we can actually click at each point and see their topics with their probability in a given article, along with the article name. For example, the figure shows the point which represents the article titled ‘Mu, delta, and kappa opioid receptor agonists induce peripheral antinociception by activation of endogenous noradrenergic system’. This article belongs to topics 32, 10, 18, 22 and 30  with probabilities 0.94, 0.19, 0.014, 0.007 and 0.007 respectively. 

### Using T-SNE:

t-SNE in contrast to PCA preserves the local neighborhood information while often distorting the global data structure. We can adjust the hyperparameters, Perplexity and Learning rate in the left menu. Perplexity indirectly balances the local and global aspects of the data. Intuitively it defines the number of closest neighbors each point has. Typically ideal perplexity varies between 5 to 50. However larger and denser dataset requires larger perplexity values. Different hyperparameters values leads to different T-SNE visualizations. 

From the figures in the visualizations We can see that it has formed clusters of articles that belong to same topic and that cluster positions varies significantly based on hyper parameters.  Again we can click at each point and see their topics with their probability in a given article, along with the article title and journal title. 

### Visualizing PUBMED abstracts LDA, using heatmaps and Dendrograms

Dendrograms are used to analyze hierarchical clustering of data. Using dendrograms in visualizing topic clusters helps us understand how topics are connected in a sequence of successive divisions or fusions that occurs during clustering. Jensen-Shannon Metric is used to calculate the inter-topic distances.

The x-axis of the dendrogram represents the topic numbers and y-axis represents the distance between topics. Lower they merge closer the topics are. For example topic 7 is far from the rest of the topics cluster. Topic 10 and topic 20 are very close.

To see interactive plot open here https://plot.ly/create/?fid=bharadwajsannapaneni8021:9

![Dendrogram to visualize topic clusters](https://drive.google.com/open?id=1Nj3QT8nFvhAq8QUyNZXqOO88hYBKRo1q)


The difference between topics can be visualized using topic difference heatmaps. X and y axes of the heat are topic numbers, and z axis is the difference between topics. We can hover around the plot and see the x, y and z coordinates along with +++ which indicates the intersection terms and -- which indicates non-intersection terms between the topics. 

The figure in the visualization shows the combined plot of dendrograms and heat map. It helps us see both the difference between two topics and their similarity at the same time in the same plot.  

To see the interactive plot click here https://plot.ly/create/?fid=bharadwajsannapaneni8021:11


Visualizing PUBMED abstracts LDA, using Topic Networks

Topic Networks helps us to understand the relationship between topics. We can understand how the topics are connected and how closely they are connected. We can also understand the most influential topics by looking at the number of connections the topic make.

Hovering on the nodes with mouse shows us the topic number along with its top words and hovering over edges shows us the common and different words between two topics. 

To see the interactive plot, click here https://plot.ly/create/?fid=bharadwajsannapaneni8021:13


Till now topic ids are taken directly from Lda using show command. In next section, pyLDAvis has numbers shown on circles that are ranked according to topic prevalence in document. 


### Visualizing PUBMED abstracts LDA, using pyLDAvis

Using pyLDAvis:

pyLDAvis provides another useful visualization. As shown in figure, it has two panels. Left panel shows Intertopic Distance Map while the right panel has the Top 30 Most Relevant terms for the Topic selected in right panel. 

Left panel consists of circles which represents topics in the model. Bigger the circle more prevalent the topic is in corpus and these circles are numbered according to their ranks. The most prevalent topic is numbered one and the least existing topic is numbered 40. We can also make interpretations from the positioning of topics. Looking at the distance between two topics we can understand how close those topics are related. 

Right panel on the other hand shows different terms that are related to the topic selected in the left panel. So we can understand the theme of a topic by observing the relevant terms. Varying relevance metric ƛ gives different relevant terms for the topic. ƛ varies between 0 to 1, ƛ=1 means terms are ranked solely based on their probability in the topic while ƛ=0 means they are ranked after normalizing with the probability of their overall occurrence in corpus, in other words ƛ=0 ranks words that are exclusively higher in selected topic. A recommended value for ƛ is 0.6. Figure below shows the pyLDAvis Intertopic Distance Map along with relevant terms for Topic 5

##### To see the interactive plots in jupyter notebook, click here http://nbviewer.jupyter.org/github/SannapaneniBharadwaj/PUBMED_Text_Analysis/blob/master/LDA_TensorBoard_Visualizations.ipynb#topic=5&lambda=1&term=

### Dynamic Topic Modelling

25 topic - Dynamic Topic Modelling is performed on PubMed abstracts. DTM helps us to understand how the topics have varied over time. In this I have plotted figures for Topic 1 and Topic 2. Figures in visualizations shows several word probabilities as a function of years. Looking these word probabilities we can infer how the topics have changed over the period of time [1949-2017]

Topic 1 Interactive plot
https://plot.ly/~bharadwajsannapaneni8021/1/

Selected Words interactive plot to understand how few terms in research are varied over time
https://plot.ly/create/?fid=bharadwajsannapaneni8021:7

Selected words are plotted with their probabilities throughout the years. Single topic dynamic modeling is performed, so that all the words belong to a single topic.

