
FAQ
====

What's the minimum CMake version for HDF5 1.14.0?
----
3.18. Ubuntu 20.04 has CMake 3.16 and can't build it.

Why does ``README.md`` starts with a version number?
----
``configure.ac`` parses the file to set version for library settings.

Running ``./autogen.sh`` fails with ``libtool not found`` error.
----
Install ``libtool`` using package manager and try ``export HDF5_LIBTOOL=/usr/local/bin/libtool``.

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

Why does the file size grow exponentially in Single-Writer-Multiple-Reader (SWMR) mode even if compression is used?
----
  File space recycling is not allowed. Thus, the size of a file modified by a SWMR writer may be larger than a file modified by a non-SWMR writer.
