# Moralization of Self Improvement

## Get the data

The reddit data is available on [Academic Torrents](https://academictorrents.com/). Under "View popular", the user can look at "Subreddit comments/submissions 2005-06 to 2023-12". The website also offers a [tutorial](https://academictorrents.com/docs/downloading.html) on how to download the data. For this project, the selected files to download from the torrent were the selfimprovement_submissions, selfimprovements_comments and investing_submissions, investing_comments for comparison. 

Following those instructions, the user will download zst files that can be transformed to CSV files with the [script](https://github.com/Watchful1/PushshiftDumps/blob/master/scripts/to_csv.py) provided by Watchful1, the user who created the reddit dataset. 

With the CSV files, the first notebook in this repository can be run to get clean data. Some of the notebooks will create new CSV or parquet files that are used in subsequent notebooks. 

## Notebooks

- [00-cleaning_notebook](00-cleaning_notebook.ipynb): This notebook takes the reddit data csv files (for both the self improvement and the investing subreddits) and does standard cleaning and preprocessing such as removing missing data, short entries, links in text, etc. The outputs of this notebook are then passed through the [LIWC Software](https://www.liwc.app/).  
- [01-morality-assessment](01-morality-assessment.ipynb): With the output of the LIWC software, morality scores for both subreddits are compared. Additionally, documents from the self improvement reddit are separated by morality scores.  
- [02-topic-modeling](02-topic-modeling.ipynb): Spark LDA topic modeling 
- [03-topics-human-validation](03-topics-human-validation.ipynb): This notebook shows the first 20 documents with the highest probability for each found topic, for validating coherence with the topic words and labeling. 
- [04-create-attributes-and-ARM](04-create-attributes-and-ARM.ipynb): This notebook converts topic probabilities and LIWC scores into "attributes" or "tags". In other words, it selects the relevant topics and liwc scores for each document and treats them as "items" of each document. Furthermore, documents are treated as transactions with items for association rule mining. 
- [05-topics-by-morality](05-topics-by-morality.ipynb): This notebook looks at the relationship of topics and moral scores, by testing different visualizations. 
- [06-expand-liwc-method](06-expand-liwc-method.ipynb): This notebook expands on the LIWC dictionary method by finding words that are closely related with morality language by co-occurrence with morality words. It is technically creating a network that was intended to be used for node2vec. Although node2vec did not work, the idea of expanding the LIWC method remains as a methodological contribution and the top words related to morality language (apart from the LIWC words themselves) were used for the remaining two notebooks. 
- [07-topic-and-morality-words-network](07-topic-and-morality-words-network.ipynb): This notebook creates a text network from the selfimprovement corpus, where words are nodes and co-occurrence in the same document are edges. It is reduced to only each topic's 20 top words, the words from the LIWC's morality dimension + the top 20 words from the [expanded liwc method](06-expand-liwc-method.ipynb). 
- [08-community_detection](08-community_detection.ipynb): This notebook takes the text network from [notebook 7](07-topic-and-morality-words-network.ipynb) and performs Louvain community detection. It aims for a more detailed analysis on how morality-related words are being used in the context of different self-improvement themes. 
