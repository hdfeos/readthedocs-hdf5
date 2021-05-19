
FAQ
====

Will accessing or reading a dataset be slower if your file contains many datasets?
----
Yes.

Accessing a dataset in a file with many datasets *will* be slower than accessing it from a file with just that dataset. 
However, the drop in performance will not be evident until there are closer to 1 million datasets in the file (maybe around 700,000 datasets), 
where all datasets are stored at one level (in one group).

The issue is that HDF5 uses btrees to store the data. 
The time to search a btree structure to find a node is log(n) speed where *n8 is the number of datasets.

Performance can be alleviated by not storing as many datasets in a group. 
For example, if you have 1,000,000 datasets, performance will be better 
if you store 1,000 datasets in 1,000 separate groups rather than storing them all in one group.
