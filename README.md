The dataset for Taxonomy-based Regression Model (TBRM)

# Overview
  This site distributes the ontology-based multi-domain sentiment dataset to support research on cross-domain sentiment classification. The idea of using Amazon product review data is originated from the <a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">multi-domain sentiment dataset</a> distributed by John Blitzer et al. The tree-structure of the Amazon shopping website is adopted in our dataset. A collection of product reviews from three different domains in Amazon, i.e., electronics, books and kitchen, were downloaded and a three-level tree structured for each domain is adopted. 

  The root is in level one (L1), with child nodes in level two (L2), and the leaf nodes are in level three (L3). Each domain tree is built from the leaf nodes. Each L3 node contains 1,000 positive reviews and 1,000 negative ones. For each node in L2, we randomly extract 1,000 positive and 1,000 negative reviews from its child nodes. We randomly fetch 1,000 positive and 1,000 negative reviews for the root from the leaf nodes.
  
  Each downloaded review instance contains a review data written by some user with a sentiment value (i.e., number of stars) ranging from 1 to 5. Reviews with 1-2 stars are regarded as negative reviews (files ended with .NEGreviews in our dataset) while those with 4-5 stars are regarded as positive ones (POSreviews). 

# Download the dataset
The <a href="https://drive.google.com/file/d/1Px0kiard3jqB3HjrBJK9jglOFiMT5AXx/view?usp=sharing">Ontology-based Multi-Domain Sentiment Dataset</a> (size 798 MB, tar.bz2 format) contains three folders. Each line in every [NEGreviews/POSreviews] file of the dataset is a product review instance. The files <a href="https://github.com/eric890006/TBRM/blob/master/Kitchen_TreeInfo.csv">Kitchen_TreeInfo.csv</a>, <a href="https://github.com/eric890006/TBRM/blob/master/Electronics_TreeInfo.csv">Electronics_TreeInfo.csv</a> and <a href="https://github.com/eric890006/TBRM/blob/master/Book_TreeInfo.csv">Book_TreeInfo.csv</a> describes the tree-structured node meta-data of domains kitchen, electronics and book. Each row represents one L3 node and its corresponding L2 and L1 nodes. The original positive and negative review amounts of each L3 node are also listed in the last two columns. Three folders are in the tar.bz2 file:

* original bottom nodes:

  The original collection downloaded from Amazon shopping website.
    
  Each file is named according to the following rules: [Domain].[Level].[NodeID].[NEGreviews|POSreviews]. The third-level of Amazon shopping website is where we downloaded the original reviews from, so all the [Level] in the folder is L3.

* balanced tree nodes:

  Use the bottom-up approach to build whole tree nodes from the L3 nodes. Each node contains 1,000 positive and 1,000 negative reviews. So each L3 node contains 1,000 positive reviews and 1,000 negative ones which randomly selected from the original bottom nodes. For each node in L2, we randomly extract 1,000 positive and 1,000 negative reviews from its child nodes. The L1 node randomly fetches 1,000 positive and 1,000 negative reviews from its grandchild nodes.
  
  Each file is named according to the following rules: [Domain].[NodeID].[Level].Balanced.[POSreviews|NEGreviews].

* in-domain subordinate relation dataset:

  When the source and target nodes are in the same domain tree, one situation that has to exclude is the “inside test”, which happened when the source and target nodes are in the ancestor/descendant relationship, i.e., parent-child or grandparent-grandchild relationship. In order to prevent such situation, the training data of the source node must exclude the target node first and then extract reviews from other lower-level nodes. The files in the folder are the reviews that specifically extracted for source and target nodes have ancestor/descendant relationship. Each file contains 1,000 positive and 1,000 negative reviews.
For example, node A has three child nodes B, C and D. In the original bottom-up approach, node A is supposed to randomly fetch 1,000 positive and 1,000 negative reviews from B, C and D. However, when A is the source and B is the target node or, B is the source node and A is the target node. Such condition may result in the “inside test” situation. In this case, only the reviews in C and D were randomly fetched to build node A’, and then we can safely use A’ as the source node and make prediction on B or B as the source and make prediction on A’.

  Each file is named according to the following rules: [Domain].[HighLevel]-[LowLevel].[HighNodeID]-[LowNodeID].[POSreviews|NEGreviews].

# References:
This sentiment dataset was introduced in Cong-Kai Lin, Yang-Yin Lee, Chi-Hsin Yu and Hsin-Hsi Chen. Taxonomy-based Regression Model for Cross-Domain Sentiment Classification. ACM International Conference on Information and Knowledge Management (CIKM), 2013.
