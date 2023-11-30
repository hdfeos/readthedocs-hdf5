FAQ
====

.. toctree::
   spack

What's the minimum CMake version for HDF5 1.14.0?
-------------------------------------------------
3.18. Ubuntu 20.04 has CMake 3.16 and can't build it.

Why does ``README.md`` starts with a version number?
----------------------------------------------------
``configure.ac`` parses the file to set version for library settings.

Running ``./autogen.sh`` fails with ``libtool not found`` error.
----------------------------------------------------------------
Install ``libtool`` using package manager and
try ``export HDF5_LIBTOOL=/usr/local/bin/libtool``.

Will reading a dataset be slower if your file contains many datasets?
---------------------------------------------------------------------
Yes.

Accessing a dataset in a file with many datasets *will* be slower
than accessing it from a file with just that dataset. 
However, the drop in performance will not be evident
until there are closer to 1 million datasets in the file
(maybe around 700,000 datasets),
where all datasets are stored at one level (in one group).

The issue is that HDF5 uses B-tree to store the data. 
The time to search a B-tree structure to find a node is log(n) speed where
*n* is the number of datasets.

Performance can be alleviated by not storing as many datasets in a group. 
For example, if you have 1,000,000 datasets, performance will be better 
if you store 1,000 datasets in 1,000 separate groups
rather than storing them all in one group.

Why does the file size grow exponentially in Single-Writer-Multiple-Reader?
---------------------------------------------------------------------------
Single-Writer-Multiple-Reader (SWMR) mode grows file size exponentially
because it doesn't allow file space recycling.
Thus, the size of a file modified by a SWMR writer may be larger
than a file modified by a non-SWMR writer.
It will grow even if you use compression.

Why doesn't Spack set ``HDF5_VOL_CONNECTOR`` environment variable?
------------------------------------------------------------------
``HDF5_VOL_CONNECTOR`` is a runtime choice of HDF5 applicatoin.
It is possible to have multiple Virtual Object Layers (VOLs)
activated in the same environment.
If Spack VOL packages set it, they will overwrite user's
HDF5_VOL_CONNECTOR configuration silently.

Why does `H5Dget_space_status()` return incorrect space allocation status?
------------------------------------------------------------------------
Before HDF5 1.13.1, 1.12.2, and 1.10.9,
`H5Dget_space_status()` could return incorrect space allocation status values
for datasets with filters applied.
This was because `H5Dget_space_status()` calculated the space allocation status
by comparing the sum of the sizes of all the allocated chunks in the dataset
to the total data size of the dataset.
However, if the dataset had any compression filters applied and
the chunks were successfully compressed,
the sum of the sizes of the allocated chunks would always be less than
the total data size of the dataset.
As a result, `H5Dget_space_status()` would never return
`H5D_SPACE_STATUS_ALLOCATED`.

What is number in the subfile name created by subfiling virtual file driver?
------------------------------------------------------------------------
It is UNIX inode number.
It should match the `ls -i` output of stub file.
