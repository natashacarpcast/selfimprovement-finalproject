# Moralization of Self Improvement

## Environment

Some of these notebooks are written to be implemented on a Spark ecosystem, while other ones can be run on a standard Python Jupyter notebook. 

## Get the data

The reddit data is available on [Academic Torrents](https://academictorrents.com/). Under "View popular", the user can look at "Subreddit comments/submissions 2005-06 to 2023-12". The website also offers a [tutorial](https://academictorrents.com/docs/downloading.html) on how to download the data. 

Following those instructions, the user will download zst files that can be transformed to CSV files with the [script](https://github.com/Watchful1/PushshiftDumps/blob/master/scripts/to_csv.py) provided by Watchful1, the user who created the reddit dataset. 

With the CSV files, the first notebook in this repository can be run to get clean data. Some of the notebooks will create new CSV or parquet files that are used in subsequent notebooks. 
